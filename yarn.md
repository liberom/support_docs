### Install and Configure ESLint using npm

Source: https://yarnpkg.com/package/eslint

This command initializes ESLint and sets up its configuration, guiding the user through the process.

```bash
npm init @eslint/config@latest

```

--------------------------------

### Yarn Install Output Example

Source: https://yarnpkg.com/blog/release/4

Illustrates the output of the 'yarn install' command in Yarn 4.0.0, showing resolution and fetch steps, packages added, and completion time. It highlights improvements in conveying information and reducing peer dependency warnings.

```shell
➤ YN0000: · Yarn 4.0.0
➤ YN0000: ┌ Resolution step
➤ YN0085: │ + next@npm:13.5.4, react-dom@npm:18.2.0, and 24 more.
➤ YN0000: └ Completed in 0s 280ms
➤ YN0000: ┌ Fetch step
➤ YN0013: │ 22 packages were added to the project (+ 177.72 MiB).
➤ YN0000: └ Completed in 3s 723ms
➤ YN0000: ┌ Link step
➤ YN0000: └ Completed
➤ YN0000: · Done with warnings in 4s 123ms
```

--------------------------------

### Yarn DLX Example: Scaffolding a Vite Project

Source: https://yarnpkg.com/cli/dlx

This example illustrates a practical application of 'yarn dlx' for project initialization. It uses 'create-vite' to scaffold a new Vite project. The command downloads and runs 'create-vite' in a temporary environment, setting up a new project structure without permanent installation.

```bash
yarn dlx create-vite
```

--------------------------------

### Configure Yarn Installation

Source: https://yarnpkg.com/migration/guide

Enables Corepack for Yarn management and sets the Yarn version to 'berry' for the project. This is a one-time setup command.

```shell
corepack enable
yarn set version berry
```

--------------------------------

### Example: Clone Monorepo and Build Specific Package (JavaScript)

Source: https://yarnpkg.com/api/plugin-exec

This JavaScript snippet demonstrates a more complex use case of the `exec:` protocol: cloning a monorepo, installing its dependencies, packing a specific workspace, and then moving the packed content into the build directory. It utilizes Node.js's `child_process.execFileSync` to run git, yarn, and tar commands. This example highlights the power of the `exec:` protocol for custom package fetching from complex sources.

```javascript
const pathToRepo = path.join(execEnv.tempDir, 'repo');
const pathToArchive = path.join(execEnv.tempDir, 'archive.tgz');
const pathToSubpackage = path.join(pathToRepo, 'packages/foobar');

// Clone the repository
child_process.execFileSync(`git`, [`clone`, `git@github.com:foo/bar`, pathToRepo]);

// Install the dependencies
child_process.execFileSync(`yarn`, [`install`], {cwd: pathToRepo});

// Pack a specific workspace
child_process.execFileSync(`yarn`, [`pack`, `--out`, pathToArchive], {cwd: pathToSubpackage});

// Send the package content into the build directory
child_process.execFileSync(`tar`, [`-x`, `-z`, `--strip-components=1`, `-f`, pathToArchive, `-C`, execEnv.buildDir]);
```

--------------------------------

### Make Installer - Linker Method

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Linker

The `makeInstaller` method is responsible for creating and returning an `Installer` object. This object encapsulates the logic for how packages are installed onto the filesystem. The specifics of the `Installer` design can be found in its dedicated file.

```TypeScript
/**
 * @param {LinkOptions} opts The link options.
 * @returns {Installer} An installer object for managing package installations.
 */
__makeInstaller(opts: LinkOptions): Installer
```

--------------------------------

### Install and Configure ESLint

Source: https://yarnpkg.com/package_name=eslint

This command installs and configures ESLint globally on your project. It prompts for configuration details and sets up the necessary files.

```bash
npm init @eslint/config@latest
```

--------------------------------

### Make Installer with PnpLinker

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpLinker

Instantiates and returns an Installer object responsible for deploying packages to the filesystem. This method defines how packages are physically installed based on the linker's configuration and the provided options.

```typescript
__makeInstaller(opts: LinkOptions): PnpInstaller
```

--------------------------------

### Install Package in PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Installs a package to the disk. This method determines if a package needs installation steps and returns build request information or null if no steps are required. It is called before dependencies are attached and not in a specific order.

```typescript
__installPackage(pkg: Package, fetchResult: FetchResult, api: InstallPackageExtraApi): Promise<{ buildRequest: null | BuildRequest; packageLocation: PortablePath }>
```

--------------------------------

### Yarn Info Example: Lodash Package

Source: https://yarnpkg.com/cli/info

This example demonstrates how to use 'yarn info' to get specific information about the 'lodash' package. It's a straightforward application of the command to a known package.

```bash
yarn info lodash
```

--------------------------------

### installPackage Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Installs a package onto the disk. It determines if the package has install steps and returns build request information or the package location.

```APIDOC
## installPackage Method

### Description
Installs a package on the disk. This method should return `null` if the package has no install steps, or an object describing the various scripts that need to be run otherwise. It is guaranteed to be called for all packages before dependencies start to be attached.

### Method
__installPackage

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **pkg** (Package) - Required - The package being installed.
- **fetchResult** (FetchResult) - Required - The fetched information about the package.
- **api** (InstallPackageExtraApi) - Required - An additional API for interacting with the core installation process.

### Request Example
```json
{
  "pkg": { ... Package ... },
  "fetchResult": { ... FetchResult ... },
  "api": { ... InstallPackageExtraApi ... }
}
```

### Response
#### Success Response (200)
Promise<{ buildRequest: null | BuildRequest; packageLocation: PortablePath }>

#### Response Example
```json
{
  "buildRequest": {
    "script": "build",
    "args": ["--force"]
  },
  "packageLocation": "/path/to/package"
}
```
```

--------------------------------

### POST /setup

Source: https://yarnpkg.com/api/yarnpkg-core/class/LegacyMigrationResolver

Sets up the project with the given report. This is an internal function for project setup procedures.

```APIDOC
## POST /setup

### Description
Sets up the project with the provided report. This function is part of the internal project initialization or configuration process.

### Method
POST

### Endpoint
/setup

### Parameters
#### Request Body
- **project** (Project) - Required - The project instance to set up.
- **report** (Report) - Required - The report object to be used during setup.

### Response
#### Success Response (200)
- **void** - Indicates successful completion of the setup process.

#### Response Example
(No response body for void return type)
```

--------------------------------

### Make Installer

Source: https://yarnpkg.com/api/plugin-nm/class/NodeModulesLinker

Instantiates and returns an Installer object responsible for the process of installing packages onto the file system. This method is central to defining the installation strategy.

```typescript
__makeInstaller(opts: LinkOptions): NodeModulesInstaller
```

--------------------------------

### Yarn Workspaces Foreach Run Build Script with Specific Dependencies First

Source: https://yarnpkg.com/cli/workspaces/foreach

This example executes the 'build' script on specified packages and their dependencies, ensuring dependencies are built first. '-Rpt' signifies recursive, topological, and parallel execution. '--from' specifies the starting packages.

```bash
yarn workspaces foreach -Rpt --from '{workspace-a,workspace-b}' run build
```

--------------------------------

### Add Regular Package with Yarn

Source: https://yarnpkg.com/cli/add

Example of adding a standard package, 'lodash', to the current workspace. This is the most common use case for dependency installation.

```bash
yarn add lodash

```

--------------------------------

### Example: Generate 'hello-world' Package (JavaScript)

Source: https://yarnpkg.com/api/plugin-exec

This JavaScript example illustrates how to generate a basic 'hello-world' package using the `exec:` protocol. It writes a `package.json` and an `index.js` file to the `execEnv.buildDir`. The `index.js` exports a simple string, and `package.json` defines the package name and version. This demonstrates a straightforward use case for dynamic package generation.

```javascript
fs.writeFileSync(path.join(execEnv.buildDir, 'package.json'), JSON.stringify({
  name: 'hello-world',
  version: '1.0.0',
}));

fs.writeFileSync(path.join(execEnv.buildDir, 'index.js'), `  
  module.exports = 'hello world!';  
`);
```

--------------------------------

### Finalize Install with PnP in PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Finalizes the installation specifically for the Plug'n'Play (PnP) environment using provided PnP settings.

```typescript
__finalizeInstallWithPnp(pnpSettings: PnpSettings): Promise<void>
```

--------------------------------

### Install Individual Package with Yarn

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Installer

The `__installPackage` method installs a package onto the disk. It should return null if no install steps are needed, or an object detailing scripts to run. This function is guaranteed to be called for all packages before dependency attachment and returns a Promise<InstallStatus>.

```typescript
/**
 * Install a package on the disk.
 * Should return `null` if the package has no install steps, or an object describing the various scripts that need to be run otherwise.
 * Note that this function isn't called in any specific order. In particular, this means that the order in which this function is called will not necessarily match the order in which the packages will be built.
 * This function is guaranteed to be called for all packages before the dependencies start to be attached.
 *
 * @param pkg Package The package being installed
 * @param fetchResult FetchResult The fetched information about the package
 * @param api InstallPackageExtraApi An additional API one can use to interact with the core
 * @returns Promise<InstallStatus>
 */
__installPackage(pkg: Package, fetchResult: FetchResult, api: InstallPackageExtraApi): Promise<InstallStatus>;
```

--------------------------------

### Workspace Setup Method - Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-core/class/Workspace

Performs the setup for the workspace. This asynchronous method likely handles initialization tasks required for the workspace to function correctly within the project.

```typescript
__setup(): Promise<void>
```

--------------------------------

### Make Installer (TypeScript)

Source: https://yarnpkg.com/api/plugin-pnpm/class/PnpmLinker

Instantiates and returns an Installer object responsible for installing packages to the filesystem. This method is central to defining how packages are laid out.

```typescript
__makeInstaller(opts: LinkOptions): PnpmInstaller
```

--------------------------------

### finalizeInstallWithPnp Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Finalizes the installation process specifically for PnP (Plug'n'Play) settings.

```APIDOC
## finalizeInstallWithPnp Method

### Description
Finalizes the install using PnP (Plug'n'Play) settings.

### Method
__finalizeInstallWithPnp

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **pnpSettings** (PnpSettings) - Required - The PnP settings to apply during finalization.

### Request Example
```json
{
  "pnpSettings": { ... PnpSettings ... }
}
```

### Response
#### Success Response (200)
Promise<void>

#### Response Example
```json
null
```
```

--------------------------------

### Initialize a New Project with Yarn

Source: https://yarnpkg.com/getting-started/install

Initializes a new project to use Yarn version 2 or higher. This command sets up the project's Yarn configuration.

```bash
yarn init -2
```

--------------------------------

### Linker Methods

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Linker

This section details the methods available within the Linker API, including finding package locations and locators, getting custom data keys, making installers, and checking package support.

```APIDOC
## GET /api/linker/__findPackageLocation

### Description
Finds the filesystem location of a package given its locator.

### Method
GET

### Endpoint
/api/linker/__findPackageLocation

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (LinkOptions) - Required - The link options.

### Response
#### Success Response (200)
- **PortablePath** (string) - The filesystem path where the package is installed.

#### Response Example
"/path/to/package"
```

```APIDOC
## GET /api/linker/__findPackageLocator

### Description
Finds the locator of a package given its filesystem location.

### Method
GET

### Endpoint
/api/linker/__findPackageLocator

### Parameters
#### Query Parameters
- **location** (PortablePath) - Required - The queried location on the disk.
- **opts** (LinkOptions) - Required - The link options.

### Response
#### Success Response (200)
- **null | Locator** (object | null) - The locator of the package, or null if the location is not owned by any package.

#### Response Example
{
  "locator": {
    "name": "package-name",
    "range": "^1.0.0"
  }
}
```

```APIDOC
## GET /api/linker/__getCustomDataKey

### Description
Returns an arbitrary key used for saving and restoring the installer's custom data.

### Method
GET

### Endpoint
/api/linker/__getCustomDataKey

### Response
#### Success Response (200)
- **string** - An arbitrary key, typically the installer's name.

#### Response Example
"NodeModulesLinker"
```

```APIDOC
## POST /api/linker/__makeInstaller

### Description
Instantiates an Installer object that describes how to install packages on the disk.

### Method
POST

### Endpoint
/api/linker/__makeInstaller

### Parameters
#### Request Body
- **opts** (LinkOptions) - Required - The link options.

### Response
#### Success Response (200)
- **Installer** (object) - An Installer object.

#### Response Example
{
  "installer": {
    "type": "NodeModulesInstaller",
    "config": {}
  }
}
```

```APIDOC
## GET /api/linker/__supportsPackage

### Description
Checks if the linker supports a given package.

### Method
GET

### Endpoint
/api/linker/__supportsPackage

### Parameters
#### Query Parameters
- **pkg** (Package) - Required - The package definition.
- **opts** (MinimalLinkOptions) - Required - The minimal link options.

### Response
#### Success Response (200)
- **boolean** - True if the linker supports the package, false otherwise.

#### Response Example
true
```

--------------------------------

### Yarn Install with Skip Build Mode

Source: https://yarnpkg.com/cli/install

This command installs dependencies but skips the execution of any build scripts. This can speed up installations in environments where build steps are not immediately required or can be handled separately.

```bash
yarn install --mode=skip-build
```

--------------------------------

### Update Package JSON Scripts for Lifecycle

Source: https://yarnpkg.com/migration/guide

Demonstrates how to adjust package.json scripts to explicitly call custom `pre` scripts, as Yarn Modern no longer automatically runs them. This ensures custom pre-start logic is executed before the main start command.

```json
{
  "scripts": {
    "prestart": "do-something",
    "start": "http-server"
  }
}

// After adjustment:
{
  "scripts": {
    "prestart": "do-something",
    "start": "yarn prestart && http-server"
  }
}
```

--------------------------------

### Install Yarn Directly from Source

Source: https://yarnpkg.com/getting-started/install

Clones, builds, and installs the latest Yarn version directly from the project's source repository. This method does not use Corepack and stores the Yarn binary locally.

```bash
yarn set version from sources
```

--------------------------------

### finalizeInstall Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Finalizes the installation process by writing miscellaneous files to disk. It may return custom data related to the installation store.

```APIDOC
## finalizeInstall Method

### Description
Finalizes the install by writing miscellaneous files to the disk. It can optionally return custom data, including details about the installation store.

### Method
__finalizeInstall

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
null
```

### Response
#### Success Response (200)
Promise<undefined | { customData: { store: Map<LocatorHash, { manifest: { preferUnplugged: null | boolean; scripts: Map<string, string>; type: null | string }; misc: { extractHint: boolean; hasBindingGyp: boolean } }> } }>

#### Response Example
```json
{
  "customData": {
    "store": {
      "locatorHash1": {
        "manifest": {
          "preferUnplugged": null,
          "scripts": {"start": "node index.js"},
          "type": "module"
        },
        "misc": {
          "extractHint": false,
          "hasBindingGyp": true
        }
      }
    }
  }
}
```
```

--------------------------------

### Static Start Report Utility

Source: https://yarnpkg.com/api/yarnpkg-core/class/StreamReport

Utility for starting a stream report.

```APIDOC
## static start

### Description
Starts a stream report with given options and a callback.

### Method
N/A (Static Method)

### Endpoint
N/A

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
- **Promise<StreamReport>** - A promise that resolves with the StreamReport.

#### Response Example
None
```

--------------------------------

### Example yarn.lock File Structure

Source: https://yarnpkg.com/blog/2016/11/24/offline-mirror

This is an example of a `yarn.lock` file generated by Yarn. It details the exact versions and resolved tarball locations for each dependency and sub-dependency, ensuring consistent installations. The `resolved` field points to the package's location in the registry.

```text
# THIS IS AN AUTOGENERATED FILE. DO NOT EDIT THIS FILE DIRECTLY.
# yarn lockfile v1

is-array@^1.0.1:
  version "1.0.1"
  resolved "https://registry.yarnpkg.com/is-array/-/is-array-1.0.1.tgz#e9850cc2cc860c3bc0977e84ccf0dd464584279a"

left-pad@^1.1.3:
  version "1.1.3"
  resolved "https://registry.yarnpkg.com/left-pad/-/left-pad-1.1.3.tgz#612f61c033f3a9e08e939f1caebeea41b6f3199a"

mime-db@~1.25.0:
  version "1.25.0"
  resolved "https://registry.yarnpkg.com/mime-db/-/mime-db-1.25.0.tgz#c18dbd7c73a5dbf6f44a024dc0d165a1e7b1c392"

mime-types@^2.1.13:
  version "2.1.13"
  resolved "https://registry.yarnpkg.com/mime-types/-/mime-types-2.1.13.tgz#e07aaa9c6c6b9a7ca3012c69003ad25a39e92a88"
  dependencies:
    mime-db "~1.25.0"


```

--------------------------------

### Yarn Version Major Release Deferred Example

Source: https://yarnpkg.com/cli/version

This example shows how to prepare the package version for a future major release bump using the 'major' strategy with the '--deferred' flag.

```bash
yarn version major --deferred
```

--------------------------------

### Yarn Unplug Examples: Unplug All Packages (Testing)

Source: https://yarnpkg.com/cli/unplug

Provides an example of unplugging all packages using the '-R' flag and a wildcard '*'. This is explicitly noted as not recommended for general use and is primarily for testing purposes.

```bash
yarn unplug -R *
```

--------------------------------

### Usage Example

Source: https://yarnpkg.com/api/yarnpkg-shell

Demonstrates how to use the `execute` function to run shell commands.

```APIDOC
## Usage Example

### Description
Demonstrates how to use the `execute` function to run shell commands.

### Method
`execute` (from `@yarnpkg/shell`)

### Endpoint
N/A (This is a library function)

### Parameters

#### Function Parameters
- **command** (string) - Required - The shell command to execute.
- **args** (string[]) - Optional - An array of arguments to pass to the command.
- **__namedParameters** (Partial<UserOptions>) - Optional - An object containing custom shell options.

### Request Example
```javascript
import { execute } from '@yarnpkg/shell';

process.exitCode = await execute(`ls "$0" | wc -l`, [process.cwd()]);
```

### Response
#### Success Response (Promise<number>)
- Returns a Promise that resolves to a number representing the exit code of the executed command.
```

--------------------------------

### Install Workspaces from Git Repository

Source: https://yarnpkg.com/protocol/git

This example illustrates how to clone workspaces from a remote git repository. It requires the remote repository to use Yarn or npm (version 7.x or higher). This feature is not guaranteed to work across all package managers and should not be relied upon in published packages.

```bash
git@github.com:yarnpkg/berry.git#workspace=@yarnpkg/shell&tag=@yarnpkg/shell/2.1.0
```

--------------------------------

### Install and Run @yarnpkg/pnpify

Source: https://yarnpkg.com/cli/pnpify/run

Installs the '@yarnpkg/pnpify' package locally and then executes a command using 'yarn run'. This is a standard way to integrate PnPify into your project workflow.

```bash
yarn add --dev @yarnpkg/pnpify
yarn run pnpify run <commandName> ...
```

--------------------------------

### Yarn Install with JSON Output

Source: https://yarnpkg.com/cli/install

This command installs project dependencies and formats the output as an NDJSON stream. This is useful for scripting and programmatic processing of Yarn's output.

```bash
yarn install --json
```

--------------------------------

### Yarn Version Major Release Example

Source: https://yarnpkg.com/cli/version

This example demonstrates how to immediately bump the package version to the next major release using the 'major' strategy.

```bash
yarn version major
```

--------------------------------

### GET /____shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-http/class/TarballHttpResolver

Determines if the package definition for a given locator should be persisted between installs.

```APIDOC
## GET /____shouldPersistResolution

### Description
This function indicates whether the package definition for the specified locator must be kept between installs. It's typically true for cached packages and false for packages hydrated directly from the filesystem (e.g., workspaces).

### Method
GET

### Endpoint
/____shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **boolean** - True if the resolution should be persisted, false otherwise.

#### Response Example
```json
true
```
```

--------------------------------

### Get Custom Data Key

Source: https://yarnpkg.com/api/plugin-nm/class/NodeModulesLinker

Returns a unique string key for saving and restoring the installer's custom data. This key is typically the installer's name but can be a more complex stringified payload for versioning or other metadata.

```typescript
__getCustomDataKey(): string
```

--------------------------------

### attachCustomData Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Attaches custom data to the installer, typically called if the installer has a custom data key matching one stored.

```APIDOC
## attachCustomData Method

### Description
Attaches custom data to the installer. This method is only called if the installer has a custom data key matching one currently stored. It will be called with whatever `finalizeInstall` returned in its `customData` field.

### Method
__attachCustomData

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **customData** (any) - Required - The custom data to attach.

### Request Example
```json
{
  "customData": { ... any ... }
}
```

### Response
#### Success Response (200)
void

#### Response Example
```json
null
```
```

--------------------------------

### Finalize Install in PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Completes the package installation process by writing necessary files to disk. It may return custom data related to the store, manifest, and build hints.

```typescript
__finalizeInstall(): Promise<undefined | { customData: { store: Map<LocatorHash, { manifest: { preferUnplugged: null | boolean; scripts: Map<string, string>; type: null | string }; misc: { extractHint: boolean; hasBindingGyp: boolean } }> } }>
```

--------------------------------

### Get Custom Data Key - Linker Method

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Linker

The `getCustomDataKey` method returns a unique string key. This key is used for saving and restoring custom data associated with the installer. Typically, it's the installer's name, but can be more complex, like a stringified JSON payload including cache versions.

```TypeScript
/**
 * @returns {string} An arbitrary key for custom data.
 */
__getCustomDataKey(): string
```

--------------------------------

### Run yarn workspaces focus Command

Source: https://yarnpkg.com/cli/workspaces/focus

This snippet shows the basic usage of the 'yarn workspaces focus' command. It is used to install a single workspace and its dependencies. No specific dependencies are required, and it outputs to the console.

```bash
$ yarn workspaces focus ...
```

--------------------------------

### GET /shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-exec/class/ExecResolver

Determines if a package definition for a given locator should be persisted between installs. Useful for distinguishing cached packages from those resolved directly from the filesystem.

```APIDOC
## GET /shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. This is typically true for cached packages and false for packages hydrated directly from the filesystem (e.g., workspaces).

### Method
GET

### Endpoint
/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **result** (boolean) - True if the package definition should be persisted, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Install Specific Yarn Branch from Source

Source: https://yarnpkg.com/getting-started/install

Installs a specific version of Yarn from the source repository using a branch or pull request number. This is useful for testing specific changes or PRs.

```bash
yarn set version from sources --branch 1211
```

--------------------------------

### Example patch: protocol dependency in package.json

Source: https://yarnpkg.com/api/plugin-patch

This snippet demonstrates how to declare a dependency using the `patch:` protocol in a `package.json` file. This allows Yarn to apply a local patch file to a specific version of a package during installation. Dependencies cannot be added through the `patch:` protocol.

```json
{
  "dependencies": {
    "lodash": "patch:lodash@1.0.0#./my-patch-file.patch"
  }
}
```

--------------------------------

### GET /shouldPersistResolution

Source: https://yarnpkg.com/api/yarnpkg-core/class/LegacyMigrationResolver

Determines if the package definition for a given locator must be persisted between installs. Primarily used to differentiate between cached packages and those resolved directly from the filesystem.

```APIDOC
## GET /shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. This function helps differentiate between packages that should be cached and those that are directly hydrated from the filesystem (e.g., workspaces).

### Method
GET

### Endpoint
/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
This endpoint is expected to return `never`, suggesting it's primarily used for its side effects or error-throwing behavior rather than a direct boolean return in typical scenarios.

#### Response Example
(No success response example as the return type is `never`)

#### Error Response
(Specific error responses depend on implementation details.)
```

--------------------------------

### PnpInstaller Constructor

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Initializes a new instance of the PnpInstaller class with the specified options.

```APIDOC
## PnpInstaller Constructor

### Description
Initializes a new instance of the PnpInstaller class.

### Method
__constructor

### Endpoint
N/A

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
  "opts": { ... LinkOptions ... }
}
```

### Response
#### Success Response (200)
PnpInstaller instance

#### Response Example
```json
{
  "instance": "PnpInstaller"
}
```
```

--------------------------------

### Clone Monorepo and Build Specific Package with Exec Protocol (JavaScript)

Source: https://yarnpkg.com/protocol/exec

Clones a Git repository, installs its dependencies, packs a specific workspace, and extracts the package into the build directory. This example utilizes Node.js `child_process` for executing external commands like `git`, `yarn`, and `tar`.

```javascript
const pathToRepo = path.join(execEnv.tempDir, 'repo');
const pathToArchive = path.join(execEnv.tempDir, 'archive.tgz');
const pathToSubpackage = path.join(pathToRepo, 'packages/foobar');

// Clone the repository
child_process.execFileSync(`git`, [`clone`, `git@github.com:foo/bar`, pathToRepo]);

// Install the dependencies
child_process.execFileSync(`yarn`, [`install`], {cwd: pathToRepo});

// Pack a specific workspace
child_process.execFileSync(`yarn`, [`pack`, `--out`, pathToArchive], {cwd: pathToSubpackage});

// Send the package content into the build directory
child_process.execFileSync(`tar`, [`-x`, `-z`, `--strip-components=1`, `-f`, pathToArchive, `-C`, execEnv.buildDir]);

```

--------------------------------

### Initialize a package with a specific Yarn version

Source: https://yarnpkg.com/cli/init

Creates a new package and installs a specific Yarn version before initializing. Using '-i=latest' installs the latest version.

```bash
yarn init -i=latest
```

--------------------------------

### Perform Focused Installs with Yarn Workspaces

Source: https://yarnpkg.com/features/workspaces

These snippets illustrate the use of 'yarn workspaces focus' to optimize dependency installation. The first command installs dependencies only for the specified '@my-org/app' workspace and its transitive dependencies. The second command installs all workspace dependencies but excludes devDependencies using the --production flag.

```bash
yarn workspaces focus @my-org/app
```

```bash
yarn workspaces focus -A --production
```

--------------------------------

### Using Yarn API: afterAllInstalled Hook for Project Info

Source: https://yarnpkg.com/advanced/plugin-tutorial

This JavaScript code illustrates a Yarn plugin using the 'afterAllInstalled' hook to print information about the project's dependency tree. It accesses the 'Project' instance to count descriptors and packages, demonstrating how to introspect project details after installation.

```javascript
const fs = require(`fs`);
const util = require(`util`);

module.exports = {
  name: `plugin-project-info`,
  factory: require => {
    const {structUtils} = require(`@yarnpkg/core`);

    return {
      default: {
        hooks: {
          afterAllInstalled(project) {
            let descriptorCount = 0;
            for (const descriptor of project.storedDescriptors.values())
              if (!structUtils.isVirtualDescriptor(descriptor))
                descriptorCount += 1;

            let packageCount = 0;
            for (const pkg of project.storedPackages.values())
              if (!structUtils.isVirtualLocator(pkg))
                packageCount += 1;

            console.log(`This project contains ${descriptorCount} different descriptors that resolve to ${packageCount} packages`);
          }
        }
      }
    };
  }
};

```

--------------------------------

### yarn unlink Examples

Source: https://yarnpkg.com/cli/unlink

Provides various examples of using the yarn unlink command. These examples cover unregistering specific remote workspaces, all workspaces, or workspaces matching a glob pattern.

```bash
yarn unlink ~/ts-loader
```

```bash
yarn unlink ~/jest --all
```

```bash
yarn unlink --all
```

```bash
yarn unlink @babel/* 'pkg-{a,b}'
```

--------------------------------

### Yarn Add Command with TypeScript Plugin

Source: https://yarnpkg.com/api/plugin-typescript

Demonstrates how the Yarn TypeScript plugin automatically adds @types packages when a new package is installed, even if not explicitly requested. This simplifies TypeScript setup by ensuring type definitions are available.

```bash
❯ yarn/packages/plugin-typescript ❯ yarn add lodash  
  
➤ YN0000: · Yarn X.Y.Z  
➤ YN0000: ┌ Resolution step  
➤ YN0000: └ Completed in 0.24s  
➤ YN0000: ┌ Fetch step  
➤ YN0013: │ @types/lodash@npm:4.14.121 can't be found in the cache and will be fetched from the remote registry  
➤ YN0013: │ lodash@npm:4.14.0 can't be found in the cache and will be fetched from the remote registry  
➤ YN0000: └ Completed in 3.63s  
➤ YN0000: ┌ Link step  
➤ YN0000: └ Completed in 2.75s  
➤ YN0000: · Done with warnings in 6.81s  
```

--------------------------------

### Example Yarn Doctor Output

Source: https://yarnpkg.com/migration/pnp

This example shows the output from the Yarn Doctor, highlighting specific issues found in `webpack-dev-server`. It details undeclared dependencies, unsafe webpack configuration regarding loaders, and incorrect checks for the `node_modules` directory.

```text
➤ YN0000: Found 1 package(s) to process  
➤ YN0000: For a grand total of 236 file(s) to validate  
  
➤ YN0000: ┌ /webpack-dev-server/package.json  
➤ YN0000: │ /webpack-dev-server/test/testSequencer.js:5:19: Undeclared dependency on @jest/test-sequencer  
➤ YN0000: │ /webpack-dev-server/client-src/default/webpack.config.js:12:14: Webpack configs from non-private packages should avoid referencing loaders without require.resolve  
➤ YN0000: │ /webpack-dev-server/test/server/contentBase-option.test.js:68:8: Strings should avoid referencing the node_modules directory (prefer require.resolve)  
➤ YN0000: └ Completed in 5.12s  
  
➤ YN0000: Failed with errors in 5.12s  
```

--------------------------------

### Finalize Yarn Package Installation

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Installer

The `__finalizeInstall` method completes the installation process by writing necessary miscellaneous files to the disk. It returns a Promise that resolves to `undefined`, `void`, or `FinalizeInstallData`.

```typescript
/**
 * Finalize the install by writing miscellaneous files to the disk.
 *
 * @returns Promise<undefined | void | FinalizeInstallData>
 */
__finalizeInstall(): Promise<undefined | void | FinalizeInstallData>;
```

--------------------------------

### Get Git Head (TypeScript)

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmPublishUtils

Retrieves the current Git commit hash for a given working directory. Returns undefined if not a Git repository. Depends on Git being installed and accessible.

```typescript
declare function __getGitHead(workingDir: PortablePath): Promise<undefined | string>;
```

--------------------------------

### Configure Supported Architectures for Conditional Packages

Source: https://yarnpkg.com/blog/release/3

This YAML configuration allows for manual specification of supported operating systems and CPU architectures for packages. It's particularly useful for zero-install setups to ensure only compatible packages are fetched and installed, improving efficiency and reducing unnecessary downloads.

```yaml
supportedArchitectures:
  os: [linux, darwin]
  cpu: [x64, arm64]
```

--------------------------------

### PnpInstaller Constructor

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Initializes a new PnpInstaller instance with provided options. The constructor takes a LinkOptions object as a parameter.

```typescript
new PnpInstaller(opts: LinkOptions): PnpInstaller
```

--------------------------------

### Update Yarn to the Latest Stable Version

Source: https://yarnpkg.com/getting-started/install

Updates the project's Yarn to the most recent stable release and then installs the project's dependencies. This ensures you are using the latest stable features.

```bash
yarn set version stable
yarn install
```

--------------------------------

### Get Candidate Package Locators - Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-core/class/LockfileResolver

Retrieves a list of potential package locators that satisfy a given descriptor. The returned array must be sorted by preference, with the most preferred locators appearing first to guide the resolution algorithm.

```typescript
__getCandidates(descriptor: Descriptor, dependencies: unknown, opts: ResolveOptions): Promise<Package[]>
```

--------------------------------

### Filter Integration Tests with Yarn

Source: https://yarnpkg.com/advanced/contributing

This command shows how to filter integration tests using the `-t` flag with a specific test description. This enables targeted execution of integration tests, for example, to verify the correct installation of single dependencies without sub-dependencies.

```bash
yarn test:integration -t 'it should correctly install a single dependency that contains no sub-dependencies'
```

--------------------------------

### Install Project Dependencies with Yarn

Source: https://context7.com/context7/yarnpkg/llms.txt

Installs all project dependencies defined in package.json. Supports various modes for CI environments, including immutable installs, checksum verification, lockfile refreshing, skipping build scripts, and offline mode.

```bash
# Standard install
yarn install

# CI validation with zero-installs (immutable lockfile and cache)
yarn install --immutable --immutable-cache

# CI validation with checksum verification for external PRs
yarn install --immutable --immutable-cache --check-cache

# Refresh lockfile metadata while keeping same resolutions
yarn install --refresh-lockfile

# Skip build scripts
yarn install --mode=skip-build

# Update lockfile only (no linking)
yarn install --mode=update-lockfile

# Verbose build output for debugging
yarn install --inline-builds

# Offline mode (use cache only, no network)
YARN_ENABLE_OFFLINE_MODE=1 yarn install
```

--------------------------------

### Execute Shell Script with Yarn Exec

Source: https://yarnpkg.com/cli/exec

This snippet demonstrates how to execute a shell script using the 'yarn exec' command. It shows examples of running a single command and a more complex script involving multiple commands. The command executes within the project's root directory, with environment setup for compatibility.

```shell
$ yarn exec <commandName> ...
```

```shell
yarn exec echo Hello World
```

```shell
yarn exec 'tsc & babel src --out-dir lib'
```

--------------------------------

### Install TypeScript (Stable) with npm

Source: https://yarnpkg.com/package_name=typescript

Installs the latest stable version of TypeScript as a development dependency using npm. This is the recommended way to add TypeScript to your project for general use.

```bash
npm install -D typescript

```

--------------------------------

### Function: __makeRuntimeApi

Source: https://yarnpkg.com/api/yarnpkg-pnp

Creates a runtime Plug'n'Play API instance.

```APIDOC
## __makeRuntimeApi

### Description
Creates an instance of the Plug'n'Play API suitable for runtime use, given settings, a base path, and a fake filesystem.

### Method
N/A (This is a function, not an HTTP endpoint)

### Endpoint
N/A

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
  "settings": "PnpSettings object",
  "basePath": "/project/root",
  "fakeFs": "FakeFS object"
}
```

### Response
#### Success Response (PnpApi)
- **return value** (PnpApi) - The runtime PnpApi object.

#### Response Example
```json
{
  "example": "// PnpApi object structure..."
}
```
```

--------------------------------

### Set Yarn Version Examples

Source: https://yarnpkg.com/cli/set/version

Demonstrates various ways to specify the Yarn version, including 'latest', 'canary', 'classic', semver ranges, specific versions, local files, URLs, and 'self'. These examples cover different release channels and sources.

```bash
yarn set version latest
```

```bash
yarn set version canary
```

```bash
yarn set version classic
```

```bash
yarn set version 3.x
```

```bash
yarn set version 2.0.0-rc.30
```

```bash
yarn set version 1.22.1
```

```bash
yarn set version ./yarn.cjs
```

```bash
yarn set version https://repo.yarnpkg.com/3.1.0/packages/yarnpkg-cli/bin/yarn.js
```

```bash
yarn set version self
```

--------------------------------

### Yarn Info with All Versions

Source: https://yarnpkg.com/cli/info

This example shows how to use the '-A' or '--all' flag with 'yarn info' to print information about all versions of a package within the project. This is useful for understanding the version landscape of a dependency.

```bash
yarn info --all
```

--------------------------------

### Yarn Install Option - skip builds (Shell)

Source: https://yarnpkg.com/advanced/changelog

Introduces a new option for 'yarn install' to skip build scripts. This speeds up installation without affecting generated Yarn artifacts, unlike 'enableScripts'.

```shell
yarn install --skip-builds
```

--------------------------------

### ExecCommand Constructor - yarnpkg

Source: https://yarnpkg.com/api/plugin-essentials/class/ExecCommand

Demonstrates the instantiation of the ExecCommand class. It shows how to create a new ExecCommand instance with default settings.

```typescript
new ExecCommand(): default
```

--------------------------------

### Install Status Type Declaration

Source: https://yarnpkg.com/api/yarnpkg-core

The `InstallStatus` type represents the status of an ongoing or completed package installation. It includes information about the build request, the installation promise, and the package's location.

```typescript
__InstallStatus :  { buildRequest: BuildRequest | null; installPromise?: Promise<void>; packageLocation: PortablePath | null }
```

--------------------------------

### Example: Explain lodash dependency with yarn why

Source: https://yarnpkg.com/cli/why

This example demonstrates how to use the 'yarn why' command to find out why the 'lodash' package is being used in the current project.

```bash
yarn why lodash
```

--------------------------------

### Update All Installed SDKs and Editor Settings with Yarn

Source: https://yarnpkg.com/getting-started/editor-sdks

This command updates all currently installed SDKs and editor settings managed by `@yarnpkg/sdks`. Running this without arguments will scan the project's root `package.json` for supported dependencies and update accordingly.

```bash
yarn dlx @yarnpkg/sdks
```

--------------------------------

### Get Archive Path - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-nm

Determines the path to a package's archive if its location resides within an archive. It accepts a portable path to the package and returns either the archive path or null if the package is not in an archive. This is useful for packages installed from archives (e.g., zip files).

```typescript
import {PortablePath} from '@yarnpkg/fslib';

function getArchivePath(packagePath: PortablePath): PortablePath | null {
  // Implementation details...
  return null;
}
```

--------------------------------

### Example: Run Angular Build with PnPify

Source: https://yarnpkg.com/cli/pnpify/run

Demonstrates running the Angular CLI 'build' command using PnPify. This allows Angular projects to work seamlessly with Yarn's Plug'n'Play.

```bash
yarn pnpify ng build
```

--------------------------------

### Configure Zero-Installs Strategy for Yarn

Source: https://context7.com/context7/yarnpkg/llms.txt

Explains how to set up the zero-installs strategy by committing the Yarn cache and PnP loader to Git. This enables instant repository clones without requiring 'yarn install' for team members, with specific configurations for cache folder and compression level.

```yaml
# .yarnrc.yml

# Disable global cache (store in project)
enableGlobalCache: false

# Set local cache folder
cacheFolder: ./.yarn/cache

# No compression for better Git efficiency
compressionLevel: 0
```

--------------------------------

### Yarn Install with Zero-Installs Validation

Source: https://yarnpkg.com/cli/install

This command validates a project when using Zero-Installs, ensuring the lockfile and cache are not modified. It's a safer approach for CI environments, especially when accepting external contributions.

```bash
yarn install --immutable --immutable-cache
```

--------------------------------

### Install TypeScript (Nightly) with npm

Source: https://yarnpkg.com/package_name=typescript&version=6.0.0-dev

This snippet demonstrates how to install the nightly build of TypeScript using npm. This is useful for testing the latest features and potential bug fixes before they are released in stable versions.

```bash
npm install -D typescript@next
```

--------------------------------

### GET /get

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/httpUtils

Performs an HTTP GET request to the specified target.

```APIDOC
## GET /get

### Description
Performs an HTTP GET request to the specified target.

### Method
GET

### Endpoint
/get

### Parameters
#### Path Parameters
- **target** (string) - Required - The target URL for the request.

#### Request Body
- **__namedParameters** (Options) - Required - Options for the request.
  - **configuration** (Configuration) - Required
  - **customErrorMessage** (function) - Optional - A function to provide a custom error message.
  - **headers** ({}) - Optional - Custom headers for the request.
  - **jsonRequest** (boolean) - Optional - Whether to send the request as JSON.
  - **jsonResponse** (boolean) - Optional - Whether to expect a JSON response.
  - **method** (Method) - Optional - The HTTP method to use.
  - **wrapNetworkRequest** (function) - Optional - A function to wrap the network request.

### Response
#### Success Response (200)
- **any** - The response body.

### Request Example
```json
{
  "target": "/example/resource",
  "__namedParameters": {
    "configuration": { ... } 
  }
}
```

### Response Example
```json
{
  "body": "some response data"
}
```
```

--------------------------------

### transformPnpSettings Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Transforms the PnP (Plug'n'Play) settings before they are applied.

```APIDOC
## transformPnpSettings Method

### Description
Transforms the PnP (Plug'n'Play) settings.

### Method
__transformPnpSettings

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **pnpSettings** (PnpSettings) - Required - The PnP settings to transform.

### Request Example
```json
{
  "pnpSettings": { ... PnpSettings ... }
}
```

### Response
#### Success Response (200)
Promise<void>

#### Response Example
```json
null
```
```

--------------------------------

### Integrate Corepack with Volta

Source: https://yarnpkg.com/corepack

Commands to install Corepack globally and enable it with a specific install directory to overwrite Volta's Yarn shims, ensuring Corepack integration.

```bash
npm install -g corepack
corepack enable --install-directory "~/.volta/bin"
```

--------------------------------

### Install Dependencies with Offline Mirror

Source: https://yarnpkg.com/blog/2016/11/24/offline-mirror

This command sequence first removes the existing `node_modules` and `yarn.lock` files and then runs `yarn install`. When the offline mirror is configured, Yarn will attempt to use the locally cached packages first, ensuring a faster and more reliable installation process.

```bash
$ rm -rf node_modules/ yarn.lock
$ yarn install
yarn install v0.17.8
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
✨  Done in 0.57s.
```

--------------------------------

### Query Dependency Information with Yarn

Source: https://context7.com/context7/yarnpkg/llms.txt

Commands to retrieve detailed information about installed packages and their dependencies. This includes checking why a package is installed, fetching package metadata from the registry, and explaining specific error codes.

```bash
# Show why package is installed
yarn why lodash

# Show package info from registry
yarn npm info react

# Show specific version info
yarn npm info react@18.0.0

# Show all versions
yarn npm info react --json | jq .versions

# Explain error code
yarn explain YN0002

# Explain peer requirements
yarn explain peer-requirements
```

--------------------------------

### Instantiate HelpCommand - TypeScript

Source: https://yarnpkg.com/api/plugin-essentials/class/HelpCommand

Demonstrates how to create a new instance of the HelpCommand class. This is the default way to initialize the command.

```typescript
new HelpCommand(): default
```

--------------------------------

### PNP Settings API

Source: https://yarnpkg.com/api/yarnpkg-pnp

Configuration options for the Plug'n'Play environment.

```APIDOC
## __PnpSettings

### Description
Defines the configuration settings for the Yarn Plug'n'Play environment.

### Properties

*   **`dependencyTreeRoots`** (`PhysicalPackageLocator[]`) - The root packages in the dependency tree.
*   **`enableTopLevelFallback`** (`boolean` - Optional) - Enables fallback mechanism for top-level packages.
*   **`fallbackExclusionList`** (`PhysicalPackageLocator[]` - Optional) - List of packages excluded from the fallback mechanism.
*   **`fallbackPool`** (`Map<string, DependencyTarget>` - Optional) - A pool of fallback dependencies.
*   **`ignorePattern`** (`string | null` - Optional) - A pattern to ignore certain files or directories.
*   **`packageRegistry`** (`PackageRegistry`) - The registry for managing packages.
*   **`pnpZipBackend`** (`PnpZipBackend`) - The backend used for handling ZIP archives.
*   **`shebang`** (`string | null` - Optional) - Shebang line for executable scripts.
```

--------------------------------

### Yarn Install with Update Lockfile Mode

Source: https://yarnpkg.com/cli/install

This command is used to update the lockfile without performing a full installation. It fetches only missing packages or those without checksums, often used by automated tools like Renovate or Dependabot.

```bash
yarn install --mode=update-lockfile
```

--------------------------------

### Yarn Config Command Tree Display Example

Source: https://yarnpkg.com/blog/release/4

Demonstrates the new tree display for the 'yarn config' command, showing settings like 'cacheFolder' and 'enableHardenedMode' with their descriptions and values. This format improves clarity and allows for selective viewing of configurations.

```shell
├─ cacheFolder
│  ├─ Description: Folder where the cache files must be written
│  ├─ Source: 
│  └─ Value: '/Users/global/.yarn/berry/cache'
│
└─ enableHardenedMode
   ├─ Description: If true, automatically enable --check-resolutions --refresh-lockfile on installs
   ├─ Source: 
   └─ Value: null
```

--------------------------------

### VersionApplyCommand Constructor

Source: https://yarnpkg.com/api/plugin-version/class/VersionApplyCommand

Initializes a new instance of the VersionApplyCommand class. This constructor is the default entry point for creating a command object.

```typescript
new VersionApplyCommand(): default
```

--------------------------------

### Initialize New Library in Monorepo

Source: https://yarnpkg.com/getting-started/recipes

Initializes a new library within a monorepo using Yarn's `init` command. This command automates the creation of a new package directory and its initial setup.

```bash
yarn packages/my-new-lib init
```

--------------------------------

### Yarn Info for Virtual Packages

Source: https://yarnpkg.com/cli/info

This example shows how to use the '--virtuals' flag with 'yarn info' to list each instance of virtual packages. This is relevant in environments where virtual packages are utilized.

```bash
yarn info --virtuals
```

--------------------------------

### Attach Internal Dependencies in Yarn Installer

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Installer

The `__attachInternalDependencies` method links a package and its internal (same-linker) dependencies. This function is guaranteed to be called for all packages before installation finalization and returns a Promise<void>.

```typescript
/**
 * Link a package and its internal (same-linker) dependencies.
 * This function is guaranteed to be called for all packages before the install is finalized.
 *
 * @param locator Locator The package itself
 * @param dependencies [Descriptor, Locator][] The package dependencies
 * @returns Promise<void>
 */
__attachInternalDependencies(locator: Locator, dependencies: [Descriptor, Locator][]): Promise<void>;
```

--------------------------------

### Generate Base SDKs with Yarn

Source: https://yarnpkg.com/cli/sdks/default

This example demonstrates how to generate only the base SDKs using the 'yarn sdks base' command. This is useful when you want to manage editor settings manually or when an editor is not yet supported by Yarn's integrations.

```bash
yarn sdks base
```

--------------------------------

### Generate SDKs and Editor Settings for VSCode and Vim with Yarn

Source: https://yarnpkg.com/cli/sdks/default

This example shows how to generate base SDKs along with editor settings for specific editors, such as VSCode and Vim, using the 'yarn sdks vscode vim' command. This command ensures that the relevant configurations for these editors are set up automatically.

```bash
yarn sdks vscode vim
```

--------------------------------

### Install Dependencies with Yarn

Source: https://yarnpkg.com/advanced/contributing

This command installs project dependencies. It automatically picks up changes made to the TypeScript sources, utilizing esbuild for on-the-fly transpilation. This improves the developer experience at the cost of slightly slower execution compared to a regular Yarn installation.

```bash
yarn install
```

--------------------------------

### HTTP GET Request

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmHttpUtils

Performs an HTTP GET request to the specified path.

```APIDOC
## GET /path

### Description
Performs an HTTP GET request to the specified path.

### Method
GET

### Endpoint
/path

### Parameters
#### Path Parameters
- **path** (string) - Required - The path to send the GET request to.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "path": "/items"
}
```

### Response
#### Success Response (200)
- **any** - The response from the GET request.

#### Response Example
```json
[
  { "id": 1, "name": "Item 1" },
  { "id": 2, "name": "Item 2" }
]
```
```

--------------------------------

### Transform PnP Settings in PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Transforms the Plug'n'Play (PnP) settings for the installation process. This method allows for modification of PnP configurations before they are applied.

```typescript
__transformPnpSettings(pnpSettings: PnpSettings): Promise<void>
```

--------------------------------

### Yarn Unplug Examples: Unplug All Instances

Source: https://yarnpkg.com/cli/unplug

Shows how to use the '-A' or '--all' flag to unplug all instances of a package across all workspaces within the project. This is useful when a dependency is used in multiple places.

```bash
yarn unplug lodash -A
```

--------------------------------

### Configure Yarn Plug'n'Play (PnP) Strategy

Source: https://context7.com/context7/yarnpkg/llms.txt

Shows how to configure Yarn's Plug'n'Play (PnP) installation strategy via .yarnrc.yml. This eliminates the node_modules folder and provides options for ESM loader generation, strictness levels, ignored patterns, fallback mechanisms, and unplugged folder customization.

```yaml
# .yarnrc.yml

# Use PnP (default)
nodeLinker: pnp

# Generate ESM loader in addition to CJS
pnpEnableEsmLoader: true

# Control PnP strictness
pnpMode: strict  # or 'loose' for legacy compatibility

# Allow specific files to use traditional resolution
pnpIgnorePatterns:
  - "./legacy-subproject/*"

# Control fallback mechanism
pnpFallbackMode: dependencies-only  # or 'none', 'all'

# Customize unplugged folder for packages requiring extraction
pnpUnpluggedFolder: ./.yarn/unplugged
```

--------------------------------

### Basic usage of yarn explain peer-requirements

Source: https://yarnpkg.com/cli/explain/peer-requirements

This demonstrates the fundamental syntax for using the 'yarn explain peer-requirements' command, showing how to invoke it with or without a hash argument.

```bash
$ yarn explain peer-requirements [hash]
```

--------------------------------

### VirtualFS Constructor

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/VirtualFS

Initializes a new instance of VirtualFS.

```APIDOC
## VirtualFS Constructor

### Description
Initializes a new instance of VirtualFS.

### Method
`new VirtualFS(__namedParameters?: VirtualFSOptions): VirtualFS`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **__namedParameters** (VirtualFSOptions) - Optional - Configuration options for VirtualFS.
  - **pathUtils** (PathUtils<PortablePath>) - Optional - Path utility instance.

### Request Example
```json
{
  "pathUtils": { ... } 
}
```

### Response
#### Success Response (200)
- **instance** (VirtualFS) - The newly created VirtualFS instance.

#### Response Example
```json
{
  "instance": { ... }
}
```
```

--------------------------------

### WorkspaceFetcher Constructor

Source: https://yarnpkg.com/api/yarnpkg-core/class/WorkspaceFetcher

Initializes a new instance of the WorkspaceFetcher.

```APIDOC
## WorkspaceFetcher Constructor

### Description
Initializes a new instance of the WorkspaceFetcher.

### Method
Constructor

### Endpoint
N/A

### Parameters
None

### Request Example
```json
{
  "example": "new WorkspaceFetcher()"
}
```

### Response
#### Success Response (200)
- **WorkspaceFetcher** (WorkspaceFetcher) - An instance of the WorkspaceFetcher.

#### Response Example
```json
{
  "example": "WorkspaceFetcher instance"
}
```
```

--------------------------------

### Check Corepack Installation

Source: https://yarnpkg.com/corepack

Command to verify if Corepack is correctly installed and enabled. A successful output indicates that Corepack shims are properly configured.

```bash
yarn exec env
```

--------------------------------

### Yarn Install with Zero-Installs and Cache Check

Source: https://yarnpkg.com/cli/install

This command provides an enhanced validation for Zero-Installs by also checking the integrity of the package cache against the lockfile. This is recommended for CI workflows where PRs from third parties are accepted.

```bash
yarn install --immutable --immutable-cache --check-cache
```

--------------------------------

### Attach External Dependencies in Yarn Installer

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Installer

The `__attachExternalDependents` method links a package to the locations of its external dependent packages. This method is guaranteed to be called for all packages before installation finalization and returns a Promise<void>.

```typescript
/**
 * Link a package to the location of the external packages that depend on it (only the location is available, since two linkers should be generic enough to not have to make custom integrations).
 * Will never be called for packages supported by the same linker (they'll be linked through the `attachInternalDependencies` hook instead).
 * This function is guaranteed to be called for all packages before the install is finalized.
 *
 * @param locator Locator
 * @param dependentPaths PortablePath[]
 * @returns Promise<void>
 */
__attachExternalDependents(locator: Locator, dependentPaths: PortablePath[]): Promise<void>;
```

--------------------------------

### ExecFetcher Constructor

Source: https://yarnpkg.com/api/plugin-exec/class/ExecFetcher

Initializes a new instance of the ExecFetcher.

```APIDOC
## Constructor __constructor

### Description
Initializes a new instance of the ExecFetcher.

### Method
CONSTRUCTOR

### Endpoint
N/A

### Parameters
None

### Request Example
```json
{
  "example": "new ExecFetcher()"
}
```

### Response
#### Success Response (200)
- **instance** (ExecFetcher) - A new instance of ExecFetcher.

#### Response Example
```json
{
  "example": "<ExecFetcher instance>"
}
```
```

--------------------------------

### Hold Fetch Result for Install Package API

Source: https://yarnpkg.com/api/yarnpkg-core

The `holdFetchResult` function allows the core to prevent reclaiming the virtual filesystem after `installPackage` returns. This is useful for parallel installers to avoid filesystem contention. However, it may increase memory consumption, requiring an upper bound on concurrent installs.

```typescript
holdFetchResult: (promise: Promise<void>) => void
```

--------------------------------

### Install Package Extra API Type Declaration

Source: https://yarnpkg.com/api/yarnpkg-core

Defines the `InstallPackageExtraApi` type, which includes the `holdFetchResult` function. This API is used to manage the virtual filesystem during package installations, especially in parallel scenarios.

```typescript
__InstallPackageExtraApi :  { holdFetchResult: (promise: Promise<void>) => void }
```

--------------------------------

### Install TypeScript (Nightly) with npm

Source: https://yarnpkg.com/package_name=typescript

Installs the latest nightly build of TypeScript as a development dependency using npm. This is useful for testing upcoming features and bug fixes.

```bash
npm install -D typescript@next

```

--------------------------------

### Run yarn init command

Source: https://yarnpkg.com/cli/init

This is the basic usage of the 'yarn init' command to create a new package in the local directory. It prompts for package details.

```bash
yarn init
```

--------------------------------

### Get Packages - npmAuditUtils

Source: https://yarnpkg.com/api/plugin-npm-cli/namespace/npmAuditUtils

Retrieves package information based on project, roots, and recursion settings. Returns a map of packages, their versions, and associated locators.

```typescript
declare function __getPackages(project: Project, roots: TopLevelDependency[], __namedParameters: { recursive: boolean }): Map<string, Map<string, Locator[]>>
```

--------------------------------

### Attach Custom Data to Yarn Installer

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Installer

The `__attachCustomData` method is used to attach custom data to the installer. It is only called if a custom data key matches one currently stored and receives data returned from `finalizeInstall`'s `customData` field. This method returns void.

```typescript
/**
 * @param customData unknown
 * @returns void
 */
__attachCustomData(customData: unknown): void;
```

--------------------------------

### Yarnpkg: Constraints Configuration Example

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Demonstrates how to define constraints for workspaces using a declarative approach. The `constraints.constraints` function is called each time the constraints engine runs, allowing assertions on workspace definitions. This example shows how to ensure all workspaces define a 'license' property with the value 'MIT'.

```typescript
/**
 * Called each time the constraints engine runs. You can then use the methods from the provided context to assert values on any of your workspaces' definitions.
 * The constraints engine is declarative, and you don't need to compare values yourself except in some specific situations.
 * For instance, if you wish to ensure that all workspaces define a specific license, you would write something like this:
 *
 * // Yes: declarative
 * for (const w of Yarn.workspaces()) {
 *   w.set(`license`, `MIT`);
 * }
 *
 * // No: imperative
 * for (const w of Yarn.workspaces()) {
 *   if (w.manifest.license !== `MIT`) {
 *     w.set(`license`, `MIT`);
 *   }
 * }
 *
 * Note that the presence of this field will disable any evaluation of the `constraints.pro` file, although no warning is currently emitted.
 *
 * @param ctx Context provided to the constraints engine.
 * @returns A Promise that resolves when the constraints have been applied.
 */
constraints: (ctx: Constraints.Context) => Promise<void>;
```

--------------------------------

### Make Runtime API for PnP - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-pnp

Constructs the Plug'n'Play runtime API object. It requires PnP settings, a base path, and a FakeFS instance to provide the necessary runtime environment for dependency resolution.

```typescript
declare function makeRuntimeApi(settings: PnpSettings, basePath: string, fakeFs: FakeFS<PortablePath>): PnpApi;
```

--------------------------------

### attachInternalDependencies Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Links a package and its internal (same-linker) dependencies. This function is guaranteed to be called for all packages before the install is finalized.

```APIDOC
## attachInternalDependencies Method

### Description
Links a package and its internal (same-linker) dependencies. This function is guaranteed to be called for all packages before the install is finalized.

### Method
__attachInternalDependencies

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The package itself.
- **dependencies** ([Descriptor, Locator][]) - Required - An array of tuples containing package descriptors and locators for its dependencies.

### Request Example
```json
{
  "locator": { ... Locator ... },
  "dependencies": [
    [{ ... Descriptor ... }, { ... Locator ... }]
  ]
}
```

### Response
#### Success Response (200)
Promise<void>

#### Response Example
```json
null
```
```

--------------------------------

### Enabling Yarn PnP via Configuration

Source: https://yarnpkg.com/migration/pnp

To enable Yarn Plug'n'Play, you need to configure the `nodeLinker` setting in your `.yarnrc.yml` file. If the setting is absent or set to `pnp`, PnP is already active. Otherwise, remove the `nodeLinker` setting and run `yarn install`.

```yaml
nodeLinker: pnp
```

--------------------------------

### Start Docusaurus Local Server

Source: https://yarnpkg.com/advanced/contributing

This command spawns a local development server for Docusaurus, allowing you to see your documentation changes in real-time as you edit the `.mdx` files.

```shell
yarn start

```

--------------------------------

### Yarn Configuration Settings (.yarnrc.yml)

Source: https://yarnpkg.com/blog/release/2

Example configuration settings for Yarn, including scope, publish access, and path to the Yarn script. These are typically defined in a .yarnrc.yml file in newer versions of Yarn.

```yaml
initScope: yarnpkg
npmPublishAccess: public
yarnPath: scripts/run-yarn.js

```

--------------------------------

### LockfileResolver Methods

Source: https://yarnpkg.com/api/yarnpkg-core/class/LockfileResolver

Documentation for the core methods of the LockfileResolver, including binding descriptors, getting candidates, and resolving dependencies.

```APIDOC
## Methods

### `__bindDescriptor`

- **Description**: Binds a descriptor to a specific locator, considering the context of the dependency.
- **Method**: N/A (Instance Method)
- **Endpoint**: N/A

#### Parameters
- **descriptor** (Descriptor) - Required - The descriptor to bind.
- **fromLocator** (Locator) - Required - The locator of the package that depends on the descriptor.
- **opts** (MinimalResolveOptions) - Required - Options for the resolution process.

#### Returns
- **Descriptor** - The bound descriptor, potentially including information from `fromLocator` for relative paths.

### `__getCandidates`

- **Description**: Retrieves a list of package locators that satisfy a given descriptor.
- **Method**: N/A (Instance Method)
- **Endpoint**: N/A

#### Parameters
- **descriptor** (Descriptor) - Required - The descriptor to find candidates for.
- **dependencies** (unknown) - Required - The dependencies and their resolutions.
- **opts** (ResolveOptions) - Required - Options for the resolution process.

#### Returns
- **Promise<Package[]>** - A promise that resolves to an array of `Package` locators, sorted by preference.
```

```APIDOC
### `__getResolutionDependencies`

- **Description**: Identifies and returns descriptors for dependencies that need to be resolved before the target descriptor can be resolved.
- **Method**: N/A (Instance Method)
- **Endpoint**: N/A

#### Parameters
- **descriptor** (Descriptor) - Required - The descriptor for which to find resolution dependencies.
- **opts** (MinimalResolveOptions) - Required - Options for the resolution process.

#### Returns
- **Record<string, Descriptor>** - An object mapping dependency names to their corresponding descriptors.
```

--------------------------------

### Install Corepack Globally

Source: https://yarnpkg.com/corepack

Command to install Corepack globally using npm. This is a workaround for system package managers that might not include Corepack by default.

```bash
npm install -g corepack
```

--------------------------------

### Registering a Yarn Hook: setupScriptEnvironment

Source: https://yarnpkg.com/advanced/plugin-tutorial

This JavaScript snippet demonstrates how to create a Yarn plugin that registers to the 'setupScriptEnvironment' hook. It injects a custom environment variable 'HELLO_WORLD' into the script execution environment. This is useful for customizing build or test processes.

```javascript
module.exports = {
  name: `plugin-hello-world`,
  factory: require => ({
    hooks: {
      setupScriptEnvironment(project, scriptEnv) {
        scriptEnv.HELLO_WORLD = `my first plugin!`;
      },
    },
  })
};

```

--------------------------------

### Get Yarn Configuration Setting (CLI)

Source: https://yarnpkg.com/cli/config/get

This snippet demonstrates how to use the `yarn config get` command in the command-line interface to retrieve various configuration settings. It covers basic retrieval, accessing nested fields, and displaying secrets. The `--json` option formats the output as NDJSON.

```bash
yarn config get <name>
yarn config get yarnPath
yarn config get packageExtensions
yarn config get 'npmScopes["my-company"].npmRegistryServer'
yarn config get npmAuthToken --no-redacted
yarn config get packageExtensions --json
```

--------------------------------

### Update All SDKs and Editor Settings with Yarn

Source: https://yarnpkg.com/cli/sdks/default

This example illustrates the default behavior of the 'yarn sdks' command when run without any arguments. It updates all existing SDKs and editor settings for a pnpified project. If the project is not pnpified, it will throw an error.

```bash
yarn sdks
```

--------------------------------

### Yarn Unplug Examples: Unplug All and Recursive

Source: https://yarnpkg.com/cli/unplug

Combines the '-A' and '-R' flags to unplug a package and its transitive dependencies from all workspaces. This provides the most comprehensive unplugging scope.

```bash
yarn unplug lodash -AR
```

--------------------------------

### Yarn `afterAllInstalled` Hook

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Hooks

The `afterAllInstalled` hook is called after the `install` method of the `Project` class has successfully completed. It takes the `project` and `options` as parameters and returns `void`.

```typescript
afterAllInstalled?: (project: Project, options: InstallOptions) => void;
```

--------------------------------

### Initialize a workspace root with yarn init

Source: https://yarnpkg.com/cli/init

Sets up a new package as a workspace root, creating a 'packages/' directory. Packages initialized with '-w' are private by default.

```bash
yarn init -w
```

--------------------------------

### Set Install State Path in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

Specifies the path where Yarn will persist install state information. This file is used for optimization and is not required to be in Git.

```yaml
installStatePath: "./.yarn/install-state.gz"
```

--------------------------------

### Prolog Predicate Call Example

Source: https://yarnpkg.com/advanced/error-codes

Demonstrates how to correctly instantiate a Prolog predicate parameter, specifically the WorkspaceCwd parameter, before using it in subsequent predicates. This example contrasts an incorrect call with a correct one that ensures the parameter is defined.

```prolog
workspace_field(WorkspaceCwd, 'name', _).

```

```prolog
workspace(WorkspaceCwd), workspace_field(WorkspaceCwd, 'name', _).

```

--------------------------------

### LightReport Constructors and Methods

Source: https://yarnpkg.com/api/yarnpkg-core/class/LightReport

This section details the constructors and methods available for the LightReport class, including how to initialize it, report various types of messages, and manage progress.

```APIDOC
## Constructor: __constructor

### Description
Initializes a new instance of LightReport.

### Method
__constructor

### Parameters
#### __namedParameters: LightReportOptions
- **__namedParameters** (LightReportOptions) - Description not provided

### Returns
LightReport

## Method: __createStreamReporter

### Description
Creates a stream reporter.

### Method
__createStreamReporter

### Parameters
#### prefix: null | string = null
- **prefix** (null | string) - Optional prefix for the stream reporter.

### Returns
PassThrough

## Method: __exitCode

### Description
Returns the exit code.

### Method
__exitCode

### Returns
0 | 1

## Method: __finalize

### Description
Finalizes the report.

### Method
__finalize

### Returns
Promise<void>

## Method: __getRecommendedLength

### Description
Gets the recommended length for reports.

### Method
__getRecommendedLength

### Returns
number

## Method: __hasErrors

### Description
Checks if there are any errors in the report.

### Method
__hasErrors

### Returns
boolean

## Method: __reportCacheHit

### Description
Reports a cache hit.

### Method
__reportCacheHit

### Parameters
#### locator: Locator
- **locator** (Locator) - The locator for the cache hit.

### Returns
void

## Method: __reportCacheMiss

### Description
Reports a cache miss.

### Method
__reportCacheMiss

### Parameters
#### locator: Locator
- **locator** (Locator) - The locator for the cache miss.

### Returns
void

## Method: __reportError

### Description
Reports an error.

### Method
__reportError

### Parameters
#### name: MessageName
- **name** (MessageName) - The name of the error message.
#### text: string
- **text** (string) - The error message text.

### Returns
void

## Method: __reportErrorOnce

### Description
Reports an error once.

### Method
__reportErrorOnce

### Parameters
#### name: MessageName
- **name** (MessageName) - The name of the error message.
#### text: string
- **text** (string) - The error message text.
#### opts?: { key?: any; reportExtra?: (report: Report) => void }
- **opts.key** (any) - Optional key for deduplication.
- **opts.reportExtra** ((report: Report) => void) - Optional function to report extra information.

### Returns
void

## Method: __reportExceptionOnce

### Description
Reports an exception once.

### Method
__reportExceptionOnce

### Parameters
#### error: Error | ReportError
- **error** (Error | ReportError) - The error or report error to report.

### Returns
void

## Method: __reportFold

### Description
Reports a foldable section of text.

### Method
__reportFold

### Parameters
#### title: string
- **title** (string) - The title of the foldable section.
#### text: string
- **text** (string) - The text content of the foldable section.

### Returns
void

## Method: __reportInfo

### Description
Reports informational text.

### Method
__reportInfo

### Parameters
#### name: null | MessageName
- **name** (null | MessageName) - The name of the informational message.
#### text: string
- **text** (string) - The informational message text.

### Returns
void

## Method: __reportInfoOnce

### Description
Reports informational text once.

### Method
__reportInfoOnce

### Parameters
#### name: MessageName
- **name** (MessageName) - The name of the informational message.
#### text: string
- **text** (string) - The informational message text.
#### opts?: { key?: any; reportExtra?: (report: Report) => void }
- **opts.key** (any) - Optional key for deduplication.
- **opts.reportExtra** ((report: Report) => void) - Optional function to report extra information.

### Returns
void

## Method: __reportJson

### Description
Reports JSON data.

### Method
__reportJson

### Parameters
#### data: any
- **data** (any) - The JSON data to report.

### Returns
void

## Method: __reportProgress

### Description
Reports progress updates.

### Method
__reportProgress

### Parameters
#### progress: AsyncIterable<{ progress: number; title?: string }, any, any>
- **progress** (AsyncIterable<{ progress: number; title?: string }>) - An async iterable providing progress updates.

### Returns
{ stop: () => void }
  * **stop**: () => void - Function to stop the progress reporting.

## Method: __reportSeparator

### Description
Reports a separator line.

### Method
__reportSeparator

### Returns
void

## Method: __reportWarning

### Description
Reports a warning.

### Method
__reportWarning

### Parameters
#### name: MessageName
- **name** (MessageName) - The name of the warning message.
#### text: string
- **text** (string) - The warning message text.

### Returns
void

## Method: __reportWarningOnce

### Description
Reports a warning once.

### Method
__reportWarningOnce

### Parameters
#### name: MessageName
- **name** (MessageName) - The name of the warning message.
#### text: string
- **text** (string) - The warning message text.
#### opts?: { key?: any; reportExtra?: (report: Report) => void }
- **opts.key** (any) - Optional key for deduplication.
- **opts.reportExtra** ((report: Report) => void) - Optional function to report extra information.

### Returns
void

## Method: __startProgressPromise

### Description
Starts a progress tracker for a promise.

### Method
__startProgressPromise

### Type parameters
#### T
#### P : ProgressIterable

### Parameters
#### progressIt: P
- **progressIt** (P) - The progress iterable.
#### cb: (progressIt: P) => Promise<T>
- **cb** ((progressIt: P) => Promise<T>) - The callback function that returns a promise.

### Returns
Promise<T>

## Properties

### ____cacheHits

### Description
Stores cache hit locators.

### Property
__cacheHits

### Type
Set<LocatorHash>

### ____cacheMisses

### Description
Stores cache miss locators.

### Property
__cacheMisses

### Type
Set<LocatorHash>

```

--------------------------------

### Yarn Info with Recursive Dependencies

Source: https://yarnpkg.com/cli/info

This example demonstrates the use of the '-R' or '--recursive' flag with 'yarn info' to include information about transitive dependencies. This provides a more comprehensive view of package relationships.

```bash
yarn info --recursive
```

--------------------------------

### FileFetcher Constructor

Source: https://yarnpkg.com/api/plugin-file/class/FileFetcher

Initializes a new instance of the FileFetcher.

```APIDOC
## FileFetcher Constructor

### Description
Initializes a new instance of the FileFetcher.

### Method
CONSTRUCTOR

### Endpoint
N/A

### Parameters
None

### Request Example
```json
{
  "example": "new FileFetcher()"
}
```

### Response
#### Success Response (200)
- **FileFetcher** (object) - An instance of the FileFetcher.

#### Response Example
```json
{
  "example": "new FileFetcher()"
}
```
```

--------------------------------

### Yarn Unplug Examples: Basic Unplug

Source: https://yarnpkg.com/cli/unplug

Demonstrates how to unplug a specific package, like 'lodash', from the active workspace. This is the most common use case for debugging or testing individual dependencies.

```bash
yarn unplug lodash
```

--------------------------------

### Attach Custom Data to PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Attaches custom data to the installer. This method is called when the installer has a custom data key that matches stored data, and it receives the 'customData' field returned by 'finalizeInstall'.

```typescript
__attachCustomData(customData: any): void
```

--------------------------------

### File Stats and Symlinks

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/PortableNodeModulesFS

Provides methods to get file statistics and create symbolic links.

```APIDOC
## GET /fs/statPromise

### Description
Asynchronously retrieves the status of a file.

### Method
GET

### Endpoint
/fs/statPromise

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (object) - Optional - Options, can include `{ bigint: true }` to return BigIntStats.

### Response
#### Success Response (200)
- **Promise<Stats | BigIntStats>** - A promise that resolves with file statistics.

## GET /fs/statSync

### Description
Synchronously retrieves the status of a file.

### Method
GET

### Endpoint
/fs/statSync

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (object) - Optional - Options, can include `{ bigint: true }` to return BigIntStats.

### Response
#### Success Response (200)
- **Stats | BigIntStats** - File statistics.

## POST /fs/symlinkPromise

### Description
Asynchronously creates a symbolic link.

### Method
POST

### Endpoint
/fs/symlinkPromise

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **p** (PortablePath) - Required - The path where the symbolic link should be created.

### Response
#### Success Response (200)
- **Promise<void>** - A promise that resolves when the symbolic link is created.

## POST /fs/symlinkSync

### Description
Synchronously creates a symbolic link.

### Method
POST

### Endpoint
/fs/symlinkSync

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **p** (PortablePath) - Required - The path where the symbolic link should be created.

### Response
#### Success Response (200)
- **void** - Indicates the symbolic link was created.
```

--------------------------------

### Install TypeScript (Stable) with npm

Source: https://yarnpkg.com/package_name=typescript&version=6.0.0-dev

This snippet shows how to install the latest stable version of TypeScript as a development dependency using npm. It's commonly used in JavaScript/TypeScript projects for type checking and compilation.

```bash
npm install -D typescript
```

--------------------------------

### attachExternalDependents Method

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Links a package to the location of its external dependent packages. This is called before the install is finalized and ensures all packages are linked.

```APIDOC
## attachExternalDependents Method

### Description
Links a package to the location of the external packages that depend on it. This function is guaranteed to be called for all packages before the install is finalized. It will never be called for packages supported by the same linker.

### Method
__attachExternalDependents

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The package locator.
- **dependentPaths** (PortablePath[]) - Required - An array of portable paths representing the dependent packages.

### Request Example
```json
{
  "locator": { ... Locator ... },
  "dependentPaths": ["/path/to/dep1", "/path/to/dep2"]
}
```

### Response
#### Success Response (200)
Promise<void>

#### Response Example
```json
null
```
```

--------------------------------

### Configure Node Module Installation Mode in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

Specifies how Node.js packages should be installed. Options include 'classic' (standard copy/clone), 'hardlinks-global' (hardlinks to a global store), and 'hardlinks-local' (hardlinks within the project).

```yaml
nmMode: "classic"
```

--------------------------------

### Yarn Workspaces Foreach Run Build Script

Source: https://yarnpkg.com/cli/workspaces/foreach

This example shows how to run the 'build' script on all descendant packages using 'yarn workspaces foreach'. The '-A' flag targets all workspaces.

```bash
yarn workspaces foreach -A run build
```

--------------------------------

### Read-Only Packages - Filesystem Error Example (JavaScript)

Source: https://yarnpkg.com/blog/release/2

Shows an example of an error that occurs when attempting to modify a file within a Yarn package archive, which is mounted as a read-only filesystem. This prevents accidental cache corruption.

```javascript
const {writeFileSync} = require(`fs`);
const lodash = require.resolve(`lodash`);

// Error: EROFS: read-only filesystem, open '/node_modules/lodash/lodash.js'
writeFileSync(lodash, `module.exports = 42;`);

```

--------------------------------

### Yarn Link All Workspaces

Source: https://yarnpkg.com/cli/link

This example demonstrates linking all workspaces from a remote project into the current project using the '--all' flag. This is useful for quickly integrating an entire remote project's components.

```bash
yarn link ~/jest --all
```

--------------------------------

### Get System Architecture Name in Node.js

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/nodeUtils

Retrieves a string representation of the system's architecture. An optional Architecture object can be provided to get the name for a specific architecture.

```javascript
/**
 * @param {Architecture} [architecture]
 * @returns {string}
 */
function __getArchitectureName(architecture) {}
```

--------------------------------

### JsZipImpl Constructor

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/JsZipImpl

Initializes a new instance of JsZipImpl. This is the primary way to create a zip archive object.

```APIDOC
## JsZipImpl Constructor

### Description
Initializes a new instance of JsZipImpl with optional configuration.

### Method
`constructor`

### Parameters
#### opts: ZipImplInput
- **opts** (ZipImplInput) - Optional - Configuration options for the JsZipImpl instance.

### Returns
- JsZipImpl - A new instance of the JsZipImpl class.

### Request Example
```json
{
  "opts": {}
}
```

### Response Example
```json
{
  "instance": "JsZipImpl"
}
```
```

--------------------------------

### NpmHttpFetcher Constructor

Source: https://yarnpkg.com/api/plugin-npm/class/NpmHttpFetcher

Initializes a new instance of the NpmHttpFetcher.

```APIDOC
## NpmHttpFetcher Constructor

### Description
Initializes a new instance of the NpmHttpFetcher.

### Method
CONSTRUCTOR

### Endpoint
N/A

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **NpmHttpFetcher** (NpmHttpFetcher) - A new instance of NpmHttpFetcher.

#### Response Example
```json
{
  "instance": "NpmHttpFetcher"
}
```
```

--------------------------------

### Build a local Yarn plugin

Source: https://yarnpkg.com/cli/builder/build/plugin

This command builds a local Yarn plugin. It requires the '@yarnpkg/builder' package to be installed. The command can be run directly if the package is installed locally and executed via 'yarn run', or by using 'yarn dlx'.

```bash
yarn builder build plugin
```

--------------------------------

### Generate Editor SDKs and Settings with Yarn

Source: https://yarnpkg.com/getting-started/editor-sdks

This command generates the base SDKs along with editor-specific settings for VSCode, Vim, and other supported editors. It uses `yarn dlx` to run the `@yarnpkg/sdks` package, enabling seamless integration of Yarn PnP with IDEs.

```bash
yarn dlx @yarnpkg/sdks vscode vim ...
```

--------------------------------

### Add TypeScript and VSCode SDK for PnP

Source: https://yarnpkg.com/getting-started/recipes

Installs TypeScript as a development dependency and sets up the VSCode SDK for Plug'n'Play (PnP) integration. This enables better IntelliSense and type checking within VSCode when using Yarn PnP.

```bash
yarn add --dev typescript
yarn dlx @yarnpkg/sdks vscode
```

--------------------------------

### Yarn Configuration Examples

Source: https://context7.com/context7/yarnpkg/llms.txt

Configuration settings for Yarn's caching mechanisms, including global cache, immutable cache, and mirror enablement. These settings control how Yarn manages package caches for improved performance and resilience.

```yaml
enableGlobalCache: true
globalFolder: "${HOME}/.yarn/berry"
enableImmutableCache: true
enableMirror: true
cacheMigrationMode: always
```

--------------------------------

### Platform Compatibility (OS) in package.json

Source: https://yarnpkg.com/configuration/manifest

Lists the operating systems on which the package is designed to work. Yarn checks `process.platform` against this list during installation; mismatches may skip postinstall scripts or prevent installation if the package is only in `optionalDependencies`.

```json
{
  "os": [
    "linux",
    "darwin",
    "win32"
  ]
}
```

--------------------------------

### Yarn Unplug Examples: Unplug Scoped Packages

Source: https://yarnpkg.com/cli/unplug

Shows how to unplug all packages within a specific scope, such as '@babel'. This uses glob patterns to target multiple packages under a namespace.

```bash
yarn unplug @babel/*
```

--------------------------------

### Yarn optionalDependencies Configuration

Source: https://yarnpkg.com/configuration/manifest

Specifies dependencies that Yarn should only install if the OS, CPU, and libc fields match the host platform. These dependencies are allowed to have a failing postinstall script and are not installed if platform filters do not match.

```json
{
  "optionalDependencies": {
    "fsevents": "^5.0.0"
  }
}
```

--------------------------------

### Get Workspace Accessible Binaries

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/scriptUtils

Retrieves a list of binaries that can be accessed by a specified workspace.

```APIDOC
## GET /scriptUtils/__getWorkspaceAccessibleBinaries

### Description
Returns the binaries that can be accessed by the specified workspace.

### Method
GET

### Endpoint
/scriptUtils/__getWorkspaceAccessibleBinaries

### Parameters
#### Path Parameters
None

#### Query Parameters
- **workspace** (Workspace) - Required - The queried workspace.

### Request Example
```json
{
  "workspace": "<workspace-definition>"
}
```

### Response
#### Success Response (200)
- **Promise<PackageAccessibleBinaries>** - An object containing accessible binaries.

#### Response Example
```json
{
  "binaries": {
    "another-binary": "path/to/workspace/binary"
  }
}
```
```

--------------------------------

### Example Yarnrc Configuration (.yarnrc.yml) in YAML

Source: https://yarnpkg.com/configuration/yarnrc

This snippet demonstrates how to configure various Yarn settings within the .yarnrc.yml file using YAML syntax. It includes examples for cache folder, cache migration mode, changeset base references, ignore patterns, checksum behavior, cloning concurrency, compression level, constraints path, and default language name.

```yaml
cacheFolder: "./.yarn/cache"
cacheMigrationMode: "required-only" | "match-spec" | "always"
changesetBaseRefs: [
  "master",
  "origin/master",
  "upstream/master",
  "main",
  "origin/main",
  "upstream/main"
]
changesetIgnorePatterns: [
  "**/*.test.{js,ts}"
]
checksumBehavior: "throw" | "update" | "ignore" | "reset"
cloneConcurrency: 2
compressionLevel: 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | "mixed"
constraintsPath: "./constraints.pro"
defaultLanguageName: "node"
```

--------------------------------

### Run Command with Temporary PnPify

Source: https://yarnpkg.com/cli/pnpify/run

Downloads and executes '@yarnpkg/pnpify' in a temporary environment without local installation. Useful for quick checks or one-off commands.

```bash
yarn dlx @yarnpkg/pnpify run <commandName> ...
```

--------------------------------

### JailFS Constructor - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Initializes a new instance of the JailFS class. It takes a target path and optional options for configuration. This constructor is the entry point for creating a JailFS instance.

```typescript
new JailFS(target: PortablePath, __namedParameters?: JailFSOptions): JailFS
```

--------------------------------

### Yarnpkg Report Section and Timer Management

Source: https://yarnpkg.com/api/yarnpkg-core/class/Report

Details methods for starting sections and timers, both synchronously and asynchronously. These are used for timing specific operations or marking sections within a report.

```typescript
__startSectionPromise
```

```typescript
__startSectionSync
```

```typescript
__startTimerPromise
```

```typescript
__startTimerSync
```

--------------------------------

### mkdirpSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Synchronously creates a directory, including any necessary parent directories.

```APIDOC
## mkdirpSync

### Description
Synchronously creates a directory, including any necessary parent directories. Returns the path of the created directory or undefined if it already existed.

### Method
`mkdirpSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory to create.
#### Optional Parameters
- **chmod** (number) - Optional - The file mode to use when creating the directory.
- **utimes** (Array<string | number | Date>) - Optional - The access and modification times to set on the created directory.

### Returns
`undefined | string` - Returns the path of the created directory or undefined if it already existed.
```

--------------------------------

### genTraversePromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/ProxiedFS

Asynchronously generates a traversal of a directory starting from an initial path, with options for stable sorting.

```APIDOC
## genTraversePromise

### Description
Asynchronously generates a traversal of a directory starting from an initial path, with options for stable sorting.

### Method
Async Generator

### Endpoint
N/A (Function call)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
async function traverse(startPath) {
  for await (const item of fs.genTraversePromise(startPath, { stableSort: true })) {
    console.log(item);
  }
}
```

### Response
#### Success Response (AsyncGenerator<P, void, unknown>)
Returns an AsyncGenerator that yields paths during traversal.

#### Response Example
```javascript
// AsyncGenerator object
```
```

--------------------------------

### ZipOpenFS Constructor

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D/class/ZipOpenFS

Creates a new ZipOpenFS instance. Takes optional ZipOpenFSOptions.

```APIDOC
## new ZipOpenFS(opts?: ZipOpenFSOptions)

### Description
Creates a new instance of the ZipOpenFS class.

### Method
Constructor

### Parameters
- **opts** (ZipOpenFSOptions) - Optional - Configuration options for the ZipOpenFS instance. Defaults to `{}` if not provided.

### Returns
ZipOpenFS
```

--------------------------------

### Get Package Accessible Binaries

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/scriptUtils

Retrieves a list of binaries that can be accessed by a specified package.

```APIDOC
## GET /scriptUtils/__getPackageAccessibleBinaries

### Description
Returns the binaries that can be accessed by the specified package.

### Method
GET

### Endpoint
/scriptUtils/__getPackageAccessibleBinaries

### Parameters
#### Path Parameters
None

#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **project** (GetPackageAccessibleBinariesOptions) - Required - The project owning the package.

### Request Example
```json
{
  "locator": "<package-locator>",
  "project": "<project-definition>"
}
```

### Response
#### Success Response (200)
- **Promise<PackageAccessibleBinaries>** - An object containing accessible binaries.

#### Response Example
```json
{
  "binaries": {
    "some-binary": "path/to/binary"
  }
}
```
```

--------------------------------

### Run Binaries with 'yarn run bin' or Shortcut

Source: https://yarnpkg.com/migration/pnp

Provides a unified command to execute binaries or scripts located within the project's dependencies. This replaces the need to directly access the `node_modules/.bin` directory, which is not generated by Yarn PnP.

```bash
yarn run jest
# or, using the shortcut:
yarn jest
```

--------------------------------

### Yarn Unplug Examples: Unplug Specific Version

Source: https://yarnpkg.com/cli/unplug

Demonstrates how to unplug a specific version of a package. This is crucial when dealing with version-specific bugs or compatibility issues.

```bash
yarn unplug lodash@1.2.3
```

--------------------------------

### Configure ESLint with Rules

Source: https://yarnpkg.com/package/eslint

This JavaScript configuration example demonstrates how to define rules and their error levels for specific file types using ESLint's programmatic API.

```javascript
import { defineConfig } from "eslint/config";

export default defineConfig([
    {
        files: ["**/*.js", "**/*.cjs", "**/*.mjs"],
        rules: {
            "prefer-const": "warn",
            "no-constant-binary-expression": "error",
        },
    },
]);

```

--------------------------------

### Yarn devDependencies Configuration

Source: https://yarnpkg.com/configuration/manifest

Defines dependencies required for a package to function correctly as a workspace. These are typically only needed when the package is installed as part of a workspace project, such as after cloning a repository and running 'yarn install'.

```json
{
  "devDependencies": {
    "webpack": "^5.0.0"
  }
}
```

--------------------------------

### opendirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Asynchronously opens a directory for reading its entries.

```APIDOC
## opendirPromise

### Description
Asynchronously opens a directory for reading its entries.

### Method
POST

### Endpoint
/websites/yarnpkg/opendirPromise

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path to the directory.
- **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The size of the buffer to use.
  - **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Request Example
```json
{
  "p": "/path/to/directory",
  "opts": {
    "bufferSize": 4096,
    "recursive": true
  }
}
```

### Response
#### Success Response (200)
- **result** (Dir<PortablePath>) - A directory handle object.

#### Response Example
```json
{
  "result": {
    "path": "/path/to/directory"
  }
}
```
```

--------------------------------

### Yarn PnP Package Dependencies Example

Source: https://yarnpkg.com/advanced/pnp-spec

Defines the set of dependencies a package can access. Each entry is a tuple of package name and its reference. A null reference indicates a missing peer dependency.

```javascript
packageDependencies: [
  ["react", "npm:18.0.0"],
],
```

```javascript
packageDependencies: [
  ["react-dom", null],
],
```

--------------------------------

### Update Yarn to the Latest Canary Version

Source: https://yarnpkg.com/getting-started/install

Updates the project's Yarn to the latest Release Candidate (canary) build. Use this command to access features not yet released on the stable channel.

```bash
yarn set version canary
```

--------------------------------

### Configure .gitignore for Zero-Installs

Source: https://context7.com/context7/yarnpkg/llms.txt

Provides a sample .gitignore file tailored for projects using the zero-installs strategy with Yarn PnP. It ensures that Yarn's cache, patches, and other internal files are correctly handled for Git repository management.

```bash
# .gitignore
.yarn/*
!.yarn/cache
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions
.pnp.*

```

--------------------------------

### GET Network Settings

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/httpUtils

Retrieves network settings for a given target, searching through configuration for the most specific match.

```APIDOC
## GET Network Settings

### Description
Retrieves network settings for a given target, searching through configuration for the most specific match.

### Method
GET

### Endpoint
/getNetworkSettings

### Parameters
#### Path Parameters
- **target** (string | URL) - Required - The target to get network settings for.

#### Request Body
- **opts** ({ configuration: Configuration }) - Required - Options containing the configuration.
  - **configuration** (Configuration) - Required - The configuration object.

### Response
#### Success Response (200)
- **enableNetwork** (null | boolean) - Whether network is enabled.
- **httpProxy** (null | string) - The HTTP proxy settings.
- **httpsCaFilePath** (null | PortablePath) - Path to the HTTPS CA certificate file.
- **httpsCertFilePath** (null | PortablePath) - Path to the HTTPS certificate file.
- **httpsKeyFilePath** (null | PortablePath) - Path to the HTTPS key file.
- **httpsProxy** (null | string) - The HTTPS proxy settings.

### Request Example
```json
{
  "target": "https://example.com",
  "opts": {
    "configuration": { ... } 
  }
}
```

### Response Example
```json
{
  "enableNetwork": true,
  "httpProxy": null,
  "httpsCaFilePath": null,
  "httpsCertFilePath": null,
  "httpsKeyFilePath": null,
  "httpsProxy": null
}
```
```

--------------------------------

### mkdirpSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Synchronously creates a directory, including any necessary parent directories.

```APIDOC
## mkdirpSync

### Description
Synchronously creates a directory and its parents if they do not exist.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirpSync

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path of the directory to create.
- **chmod** (number) - Optional - The file mode to use for creating directories.
- **utimes** ([string | number | Date, string | number | Date]) - Optional - The access and modification times to use for creating directories.

### Request Example
```json
{
  "p": "/path/to/directory",
  "chmod": 755,
  "utimes": ["2023-10-27T10:00:00Z", "2023-10-27T10:00:00Z"]
}
```

### Response
#### Success Response (200)
- **result** (string | undefined) - Returns the path if successful, otherwise undefined.

#### Response Example
```json
{
  "result": "/path/to/directory"
}
```
```

--------------------------------

### Enable Automatic TypeScript Type Installation in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

Determines whether Yarn should automatically install `@types` dependencies for packages lacking typings. This feature is enabled by default if a `tsconfig.json` exists at the project root or current workspace.

```json
tsEnableAutoTypes: true
```

--------------------------------

### Add Package from GitHub Protocol with Yarn

Source: https://yarnpkg.com/cli/add

Illustrates using the 'github:' protocol to add a package from GitHub, offering a more concise way to specify GitHub sources.

```bash
yarn add lodash@github:lodash/lodash

```

--------------------------------

### Configure Package Installation Behavior in Yarn

Source: https://yarnpkg.com/configuration/manifest

The 'installConfig' field provides extra settings that affect how a package is installed. It includes 'hoistingLimits' to define the maximum level for package hoisting (options: 'workspaces', 'dependencies', 'none') and 'selfReferences' to control whether workspaces are allowed to require themselves.

```yaml
installConfig:
  hoistingLimits: "workspaces"
  selfReferences: true
```

--------------------------------

### NodeModulesLinker Constructor

Source: https://yarnpkg.com/api/plugin-nm/class/NodeModulesLinker

Initializes a new instance of NodeModulesLinker. This is the primary constructor for creating linker objects that manage package installations on the file system.

```typescript
new NodeModulesLinker(): NodeModulesLinker
```

--------------------------------

### opendirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Asynchronously opens a directory and returns a directory iterator.

```APIDOC
## opendirPromise

### Description
Asynchronously opens a directory and returns a directory iterator (`Dir<PortablePath>`) which can be used to iterate over the directory's entries.

### Method
`opendirPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory to open.
#### Optional Parameters
- **opts** (Object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The size of the buffer to use for reading directory entries.
  - **recursive** (boolean) - Optional - Whether to recursively open subdirectories.

### Returns
`Promise<Dir<PortablePath>>` - A promise that resolves with the directory iterator.
```

--------------------------------

### watchFile API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NoFS

Starts watching a file for changes. It does not return any value.

```APIDOC
## never watchFile

### Description
Starts watching a file for changes. This operation returns immediately and does not yield a value.

### Method
sync

### Endpoint
N/A (Internal function)

### Parameters
None

### Request Example
```json
{}
```

### Response
#### Success Response (void)
This function returns void.
```

--------------------------------

### Create Custom Yarn Plugin

Source: https://context7.com/context7/yarnpkg/llms.txt

Example of creating a custom Yarn plugin in JavaScript (.cjs file) that defines a new command and how to register it in `.yarnrc.yml`.

```javascript
// .yarn/plugins/my-plugin.cjs
module.exports = {
  name: '@my-org/plugin-custom',
  factory: (require) => {
    const { BaseCommand } = require('@yarnpkg/cli');

    class MyCommand extends BaseCommand {
      static paths = [['my-command']];

      async execute() {
        this.context.stdout.write('Hello from custom plugin!\n');
      }
    }

    return {
      commands: [MyCommand],
    };
  },
};

```

```yaml
# .yarnrc.yml
plugins:
  - path: .yarn/plugins/my-plugin.cjs
    spec: "@my-org/plugin-custom"

```

--------------------------------

### Realpath

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/ProxiedFS

Gets the canonicalized absolute pathname.

```APIDOC
## ____realpathSync

### Description
Synchronously gets the canonicalized absolute pathname.

### Method
GET

### Endpoint
/path/realpath/sync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to resolve.

### Request Example
```json
{
  "path": "/path/to/resolve"
}
```

### Response
#### Success Response (200)
- **P** - The canonicalized absolute pathname.

#### Response Example
```json
{
  "realpath": "/canonical/absolute/path"
}
```
```

--------------------------------

### Create Directory - mkdirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously creates a directory. Supports options for mode and recursion. Returns a Promise that resolves with the created directory path or undefined.

```typescript
declare function __mkdirPromise(p: PortablePath, opts?: Partial<{ mode: number; recursive: boolean }>): Promise<undefined | string>;
```

--------------------------------

### Yarn Info for Package Manifest

Source: https://yarnpkg.com/cli/info

This example illustrates using the '--manifest' flag with 'yarn info' to display data directly from the package archive, such as license and homepage information. This provides access to metadata embedded within the package.

```bash
yarn info --manifest
```

--------------------------------

### shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-npm/class/NpmTagResolver

Indicates whether the package definition for a specified locator must be kept between installs.

```APIDOC
## shouldPersistResolution

### Description
This function indicates whether the package definition for the specified locator must be kept between installs. It should typically return `true` for cached packages and `false` for packages hydrated directly from the filesystem (e.g., workspaces). Packages returning `false` are still stored in the lockfile but will be resolved again on the next install.

### Method
`shouldPersistResolution`

### Parameters
#### Path Parameters
* None

#### Query Parameters
* None

#### Request Body
* **locator** (Locator) - Required - The queried package.
* **opts** (MinimalResolveOptions) - Required - The resolution options.

### Request Example
```json
{
  "locator": {
    "name": "example-package",
    "reference": "workspace:.yalc/example-package"
  },
  "opts": {}
}
```

### Response
#### Success Response (never)
* Returns `true` if the package should be persisted, `false` otherwise.

#### Response Example
```json
true
```
```

--------------------------------

### Get Ident URL

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmHttpUtils

Generates the URL for a given package identifier.

```APIDOC
## GET /ident/url

### Description
Generates the URL for a given package identifier.

### Method
GET

### Endpoint
/ident/url

### Parameters
#### Path Parameters
- **ident** (Ident) - Required - The identifier for the package.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "ident": { /* Ident object */ }
}
```

### Response
#### Success Response (200)
- **string** - The generated URL for the package identifier.

#### Response Example
```json
"https://registry.npmjs.org/example-package"
```
```

--------------------------------

### NpmLoginCommand Constructor and Methods

Source: https://yarnpkg.com/api/plugin-npm-cli/class/NpmLoginCommand

This snippet demonstrates the basic instantiation of the NpmLoginCommand and its primary execution methods. It includes the constructor signature and the return types for the execute and validateAndExecute methods, indicating asynchronous operations that return a promise resolving to a number.

```typescript
new NpmLoginCommand(): default
__execute(): Promise<0 | 1>
__validateAndExecute(): Promise<number>
```

--------------------------------

### getLocator Function

Source: https://yarnpkg.com/advanced/pnpapi

A helper function to easily work with "referencish" ranges, simplifying the process of getting a PackageLocator.

```APIDOC
## `getLocator(...)`

### Description
This function is a small helper that makes it easier to work with "referencish" ranges. As seen in the `PackageInformation` interface, the `packageDependencies` map values may be either a string or a tuple, and the way to compute the resolved locator changes depending on that. `getLocator` avoids the need for manual `Array.isArray` checks.

Just like for `topLevel`, you're under no obligation to use it; you're free to roll your own version if our implementation isn't suitable.
```

--------------------------------

### statSync

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipOpenFS

Gets the stats of a file or directory synchronously.

```APIDOC
## POST /websites/yarnpkg/statSync

### Description
Gets the stats of a file or directory synchronously.

### Method
POST

### Endpoint
/websites/yarnpkg/statSync

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file or directory.
- **opts** (StatSyncOptions) - Optional - Options for retrieving stats.

### Request Body
```json
{
  "p": "/path/to/file_or_directory",
  "opts": {
    "bigint": true,
    "throwIfNoEntry": false
  }
}
```

### Response
#### Success Response (200)
- **Stats | BigIntStats | undefined** - The stats of the file or directory, or undefined if `throwIfNoEntry` is false and the entry does not exist.

#### Response Example
```json
{
  "isFile": true,
  "isDirectory": false,
  "size": 1024,
  "mtimeMs": 1678886400000,
  "atimeMs": 1678886400000
}
```
```

--------------------------------

### statPromise

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipOpenFS

Gets the stats of a file or directory asynchronously.

```APIDOC
## POST /websites/yarnpkg/statPromise

### Description
Gets the stats of a file or directory asynchronously.

### Method
POST

### Endpoint
/websites/yarnpkg/statPromise

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file or directory.
- **opts** (StatOptions) - Optional - Options for retrieving stats.

### Request Body
```json
{
  "p": "/path/to/file_or_directory",
  "opts": {
    "bigint": true,
    "throwIfNoEntry": false
  }
}
```

### Response
#### Success Response (200)
- **Promise<Stats | BigIntStats>** - A promise that resolves with the stats of the file or directory.

#### Response Example
```json
{
  "isFile": true,
  "isDirectory": false,
  "size": 1024,
  "mtimeMs": 1678886400000,
  "atimeMs": 1678886400000
}
```
```

--------------------------------

### Get Plugin Configuration - @yarnpkg/cli

Source: https://yarnpkg.com/api/yarnpkg-cli

Retrieves the current plugin configuration for the Yarn CLI. This configuration dictates which plugins are loaded and how they are initialized.

```typescript
function __getPluginConfiguration(): PluginConfiguration
```

--------------------------------

### Show package info with yarn

Source: https://yarnpkg.com/cli/npm/info

This command fetches and displays information about a specified package from the npm registry. It can show all available information or specific fields. The package does not need to be installed locally. Options like --json and --fields allow for customized output.

```bash
yarn npm info react
yarn npm info react --json
yarn npm info react@16.12.0
yarn npm info react@next
yarn npm info react --fields description
yarn npm info react --fields versions
yarn npm info react --fields readme
yarn npm info react --fields homepage,repository
```

--------------------------------

### watch API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NoFS

Starts watching a file for changes. It does not return any value.

```APIDOC
## never watch

### Description
Starts watching a file for changes. This operation returns immediately and does not yield a value.

### Method
sync

### Endpoint
N/A (Internal function)

### Parameters
None

### Request Example
```json
{}
```

### Response
#### Success Response (void)
This function returns void.
```

--------------------------------

### File Existence and Status

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Provides methods to check if a file exists and to get file status information. Both promise-based and synchronous versions are available.

```APIDOC
## `existsPromise`

### Description
Asynchronously checks if a file or directory exists.

### Method
`Promise<boolean>`

### Parameters
- **p** (`PortablePath`) - The path to check.

### Returns
`Promise<boolean>`

## `existsSync`

### Description
Synchronously checks if a file or directory exists.

### Method
`boolean`

### Parameters
- **p** (`PortablePath`) - The path to check.

### Returns
`boolean`

## `fstatPromise`

### Description
Asynchronously gets the status of a file descriptor. Can return `Stats` or `BigIntStats` based on options.

### Method
`Promise<Stats | BigIntStats>`

### Parameters
- **fd** (`number`) - The file descriptor.
- **opts** (object, optional) - Options for retrieving stats.
  - **bigint** (`true`) - If true, returns `BigIntStats`.

### Returns
`Promise<Stats>` or `Promise<BigIntStats>`
```

--------------------------------

### getRealPath

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Gets the real path of a given path. This is an abstract method.

```APIDOC
## getRealPath

### Description
Gets the real path of a given path. This is an abstract method.

### Method
N/A (Abstract method)

### Endpoint
N/A (Abstract method)

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "example": "Not applicable"
}
```

### Response
#### Success Response (P)
- **Type**: P
- **Description**: The real path.

#### Response Example
```json
{
  "example": "Not applicable"
}
```
```

--------------------------------

### NpmSemverResolver - __constructor

Source: https://yarnpkg.com/api/plugin-npm/class/NpmSemverResolver

Initializes a new instance of NpmSemverResolver.

```APIDOC
## new NpmSemverResolver()

### Description
Initializes a new instance of the NpmSemverResolver.

### Method
CONSTRUCTOR

### Endpoint
N/A

### Parameters
None

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **NpmSemverResolver** (NpmSemverResolver) - A new instance of NpmSemverResolver.

#### Response Example
```json
{
  "instance": "NpmSemverResolver"
}
```
```

--------------------------------

### Yarn Command for Version Upgrade

Source: https://yarnpkg.com/features/release-workflow

Demonstrates how to upgrade a workspace's version and how Yarn automatically updates dependent workspaces with semver ranges.

```bash
yarn version 1.1.1
```

--------------------------------

### Length Recommendation

Source: https://yarnpkg.com/api/yarnpkg-core/class/Report

Method to get the recommended length for report outputs.

```APIDOC
## Length Recommendation

### `__getRecommendedLength`

*   `__getRecommendedLength(): number`

    Gets the recommended length for terminal output based on its size.

    #### Returns
    *   `number` - The recommended length.
```

--------------------------------

### Get File Stats

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Retrieve statistics about a file or directory, including size, modification times, and more.

```APIDOC
## GET /fs/stat

### Description
Retrieves status information for a file or directory. Supports returning standard stats or big-integer stats.

### Method
GET

### Endpoint
/fs/stat

### Parameters
#### Query Parameters
- **path** (PortablePath) - Required - The path to the file or directory.
- **options** (object) - Optional - Configuration options.
  - **bigint** (boolean) - Optional - If true, returns BigIntStats. Defaults to false.
  - **throwIfNoEntry** (boolean) - Optional - If true, throws an error if the path does not exist. Defaults to true.

### Request Example
```json
{
  "path": "/path/to/file",
  "options": {
    "bigint": true
  }
}
```

### Response
#### Success Response (200)
- **stats** (Stats | BigIntStats) - An object containing file statistics.

#### Response Example
```json
{
  "stats": {
    "dev": 2050,
    "ino": 131074,
    "mode": 33188,
    "nlink": 1,
    "uid": 501,
    "gid": 20,
    "rdev": 0,
    "size": 1024,
    "blksize": 4096,
    "blocks": 8,
    "atimeMs": 1678886400000,
    "mtimeMs": 1678886400000,
    "ctimeMs": 1678886400000,
    "birthtimeMs": 1678886400000
  }
}
```
```

--------------------------------

### Get Top Level Dependencies - npmAuditUtils

Source: https://yarnpkg.com/api/plugin-npm-cli/namespace/npmAuditUtils

Fetches the top-level dependencies for a given project and workspace, with options to include all dependencies and specify the environment. Returns an array of top-level dependency objects.

```typescript
declare function __getTopLevelDependencies(project: Project, workspace: Workspace, __namedParameters: { all: boolean; environment: Environment }): TopLevelDependency[]
```

--------------------------------

### Example package.json for Yarn Project

Source: https://yarnpkg.com/blog/2016/11/24/offline-mirror

This JSON object represents a `package.json` file for a Node.js project using Yarn. It defines the project's name, version, entry point, license, and lists its direct dependencies with version ranges.

```json
{
  "name": "yarn-offline",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "dependencies": {
    "is-array": "^1.0.1",
    "left-pad": "^1.1.3",
    "mime-types": "^2.1.13"
  }
}

```

--------------------------------

### watchFile - Watch for File Changes

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Starts watching a file for changes. Returns a `StatWatcher` object.

```APIDOC
## POST /fs/watchFile

### Description
Starts watching a file for changes.

### Method
POST

### Endpoint
/fs/watchFile

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the file to watch.
- **cb** (WatchFileCallback) - Required - The callback function to handle changes.
- **opts** (Partial<{ bigint: boolean; interval: number; persistent: boolean }>) - Optional - Options for watching.
  - **bigint** (boolean) - If true, uses big-endian numbers for stats.
  - **interval** (number) - The polling interval in milliseconds.
  - **persistent** (boolean) - Whether to keep the process running as long as files are being watched.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "interval": 5000
  }
}
```

### Response
#### Success Response (200)
- **watcher** (StatWatcher) - An object representing the file change watcher.
```

--------------------------------

### GET /____supportsLocator

Source: https://yarnpkg.com/api/plugin-http/class/TarballHttpResolver

Checks if the resolver supports a given locator.

```APIDOC
## GET /____supportsLocator

### Description
This function must return true if the specified locator is intended to be turned into a package definition by this resolver. If it returns false, other functions (except its locator counterpart) will not be called.

### Method
GET

### Endpoint
/____supportsLocator

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The locator that needs to be validated.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **boolean** - True if the resolver supports the locator, false otherwise.

#### Response Example
```json
true
```
```

--------------------------------

### Instantiate FileResolver

Source: https://yarnpkg.com/api/plugin-file/class/FileResolver

Creates a new instance of the FileResolver. This is the entry point for using the resolver's functionality.

```javascript
new FileResolver(): FileResolver
```

--------------------------------

### File System Operations (stat, symlink, truncate, unlink, watch, write)

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

This section details various file system operations including getting file statistics, creating symbolic links, truncating files, unlinking files, watching for file changes, and writing file content. Both promise-based and synchronous methods are provided.

```APIDOC
## GET /statSync

### Description
Retrieves statistics about a file or directory. Overloaded to handle different options for bigint and throwIfNoEntry.

### Method
GET

### Endpoint
/statSync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file or directory.

#### Query Parameters
- **opts** (StatSyncOptions) - Optional - Options for statSync, including bigint and throwIfNoEntry.

### Request Example
```json
{
  "p": "/path/to/file"
}
```

### Response
#### Success Response (200)
- **stats** (Stats | BigIntStats | undefined) - File or directory statistics, or undefined if throwIfNoEntry is false and the entry does not exist.

#### Response Example
```json
{
  "stats": {
    "dev": 2112,
    "ino": 582806,
    "mode": 33188,
    "nlink": 1,
    "uid": 1000,
    "gid": 1000,
    "rdev": 0,
    "size": 1024,
    "blksize": 4096,
    "blocks": 8,
    "atimeMs": 1577836800000.0,
    "mtimeMs": 1577836800000.0,
    "ctimeMs": 1577836800000.0,
    "birthtimeMs": 1577836800000.0
  }
}
```

## POST /symlinkPromise

### Description
Asynchronously creates a symbolic link.

### Method
POST

### Endpoint
/symlinkPromise

### Parameters
#### Path Parameters
- **target** (P) - Required - The target of the symbolic link.
- **p** (P) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of the symbolic link (e.g., 'dir', 'file').

### Request Example
```json
{
  "target": "/path/to/target",
  "p": "/path/to/symlink",
  "type": "file"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /symlinkSync

### Description
Synchronously creates a symbolic link.

### Method
POST

### Endpoint
/symlinkSync

### Parameters
#### Path Parameters
- **target** (P) - Required - The target of the symbolic link.
- **p** (P) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of the symbolic link (e.g., 'dir', 'file').

### Request Example
```json
{
  "target": "/path/to/target",
  "p": "/path/to/symlink",
  "type": "file"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /truncatePromise

### Description
Asynchronously truncates a file to a specified length.

### Method
POST

### Endpoint
/truncatePromise

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file to truncate.
- **len** (number) - Optional - The desired length of the file.

### Request Example
```json
{
  "p": "/path/to/file",
  "len": 100
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /truncateSync

### Description
Synchronously truncates a file to a specified length.

### Method
POST

### Endpoint
/truncateSync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file to truncate.
- **len** (number) - Optional - The desired length of the file.

### Request Example
```json
{
  "p": "/path/to/file",
  "len": 100
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /unlinkPromise

### Description
Asynchronously removes a file or symbolic link.

### Method
POST

### Endpoint
/unlinkPromise

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file or symbolic link to remove.

### Request Example
```json
{
  "p": "/path/to/file"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /unlinkSync

### Description
Synchronously removes a file or symbolic link.

### Method
POST

### Endpoint
/unlinkSync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file or symbolic link to remove.

### Request Example
```json
{
  "p": "/path/to/file"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /unwatchFile

### Description
Stops watching for changes on a file.

### Method
POST

### Endpoint
/unwatchFile

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file to stop watching.
- **cb** (WatchFileCallback) - Optional - The callback function to remove.

### Request Example
```json
{
  "p": "/path/to/file"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /utimesPromise

### Description
Asynchronously updates the access and modification times of a file.

### Method
POST

### Endpoint
/utimesPromise

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
- **atime** (string | number | Date) - Required - The access time.
- **mtime** (string | number | Date) - Required - The modification time.

### Request Example
```json
{
  "p": "/path/to/file",
  "atime": "2023-01-01T12:00:00Z",
  "mtime": "2023-01-01T12:00:00Z"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /utimesSync

### Description
Synchronously updates the access and modification times of a file.

### Method
POST

### Endpoint
/utimesSync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
- **atime** (string | number | Date) - Required - The access time.
- **mtime** (string | number | Date) - Required - The modification time.

### Request Example
```json
{
  "p": "/path/to/file",
  "atime": "2023-01-01T12:00:00Z",
  "mtime": "2023-01-01T12:00:00Z"
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /watch

### Description
Watches for changes on a file or directory. Returns a Watcher object.

### Method
POST

### Endpoint
/watch

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to watch.
- **cb** (WatchCallback) - Optional - The callback function to execute on changes.
- **opts** (WatchOptions) - Optional - Options for watching.

### Request Example
```json
{
  "p": "/path/to/watch",
  "cb": "() => console.log('change')",
  "opts": {
    "persistent": true
  }
}
```

### Response
#### Success Response (200)
- **watcher** (Watcher) - The watcher object.

#### Response Example
```json
{
  "watcher": {}
}
```

## POST /watchFile

### Description
Watches for changes on a file using polling. Returns a StatWatcher object.

### Method
POST

### Endpoint
/watchFile

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file to watch.
- **cb** (WatchFileCallback) - Required - The callback function to execute on changes.
- **opts** (Partial<{ bigint: boolean; interval: number; persistent: boolean }>) - Optional - Options for watching.

### Request Example
```json
{
  "p": "/path/to/file",
  "cb": "() => console.log('change')",
  "opts": {
    "interval": 5000,
    "persistent": true
  }
}
```

### Response
#### Success Response (200)
- **statWatcher** (StatWatcher) - The stat watcher object.

#### Response Example
```json
{
  "statWatcher": {}
}
```

## POST /writeFilePromise

### Description
Asynchronously writes data to a file. Creates the file if it does not exist.

### Method
POST

### Endpoint
/writeFilePromise

### Parameters
#### Path Parameters
- **p** (FSPath<P>) - Required - The path to the file.
- **content** (string | ArrayBufferView<ArrayBufferLike>) - Required - The content to write.
- **opts** (WriteFileOptions) - Optional - Options for writing the file.

### Request Example
```json
{
  "p": "/path/to/file",
  "content": "Hello, world!",
  "opts": {
    "encoding": "utf8"
  }
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /writeFileSync

### Description
Synchronously writes data to a file. Creates the file if it does not exist.

### Method
POST

### Endpoint
/writeFileSync

### Parameters
#### Path Parameters
- **p** (FSPath<P>) - Required - The path to the file.
- **content** (string | ArrayBufferView<ArrayBufferLike>) - Required - The content to write.
- **opts** (WriteFileOptions) - Optional - Options for writing the file.

### Request Example
```json
{
  "p": "/path/to/file",
  "content": "Hello, world!",
  "opts": {
    "encoding": "utf8"
  }
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /writeJsonPromise

### Description
Asynchronously writes JSON data to a file.

### Method
POST

### Endpoint
/writeJsonPromise

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
- **data** (any) - Required - The JSON data to write.
- **compact** (boolean) - Optional - If true, writes JSON in a compact format.

### Request Example
```json
{
  "p": "/path/to/file.json",
  "data": {
    "key": "value"
  },
  "compact": true
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /writeJsonSync

### Description
Synchronously writes JSON data to a file.

### Method
POST

### Endpoint
/writeJsonSync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
- **data** (any) - Required - The JSON data to write.
- **compact** (boolean) - Optional - If true, writes JSON in a compact format.

### Request Example
```json
{
  "p": "/path/to/file.json",
  "data": {
    "key": "value"
  },
  "compact": true
}
```

### Response
#### Success Response (200)
- **void** - Indicates successful completion.

#### Response Example
```json
{
  "success": true
}
```

## POST /writePromise

### Description
Asynchronously writes data to a file descriptor. Supports writing Buffers or strings.

### Method
POST

### Endpoint
/writePromise

### Parameters
#### Path Parameters
- **fd** (number) - Required - The file descriptor.
- **buffer** (Buffer<ArrayBufferLike> | string) - Required - The data to write.
- **offset** (number) - Optional - The position in the buffer to start writing from.
- **length** (number) - Optional - The number of bytes to write.
- **position** (number) - Optional - The position in the file to write to.

### Request Example
```json
{
  "fd": 1,
  "buffer": "Hello",
  "position": 0
}
```

### Response
#### Success Response (200)
- **bytesWritten** (number) - The number of bytes written.

#### Response Example
```json
{
  "bytesWritten": 5
}
```
```

--------------------------------

### Directory Creation (mkdir) Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NodeFS

Provides methods for creating directories asynchronously with promises or synchronously, with options for mode and recursion.

```APIDOC
## mkdirPromise

### Description
Asynchronously creates a directory, similar to `fs.mkdir`. It supports specifying the mode and creating parent directories recursively.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirPromise

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path of the directory to create.
- **opts** (Partial<{ mode: number; recursive: boolean }>) - Optional - An object containing options: `mode` for directory permissions and `recursive` to create parent directories if they don't exist. Defaults to `{ recursive: false }`.

### Request Example
```json
{
  "p": "/path/to/new/directory",
  "opts": {
    "mode": 484, 
    "recursive": true
  }
}
```

### Response
#### Success Response (200)
- **undefined | string** - Returns the resolved path if created, otherwise undefined.

#### Response Example
```json
"/path/to/new/directory"
```

## mkdirSync

### Description
Synchronously creates a directory, similar to `fs.mkdirSync`. It supports specifying the mode and creating parent directories recursively.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirSync

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path of the directory to create.
- **opts** (Partial<{ mode: number; recursive: boolean }>) - Optional - An object containing options: `mode` for directory permissions and `recursive` to create parent directories if they don't exist. Defaults to `{ recursive: false }`.

### Request Example
```json
{
  "p": "/path/to/new/directory",
  "opts": {
    "mode": 484, 
    "recursive": true
  }
}
```

### Response
#### Success Response (200)
- **undefined | string** - Returns the resolved path if created, otherwise undefined.

#### Response Example
```json
"/path/to/new/directory"
```
```

--------------------------------

### Attach Internal Dependencies in PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Links a package and its internal dependencies within the same linker. This method is guaranteed to be called for all packages before the install is finalized.

```typescript
__attachInternalDependencies(locator: Locator, dependencies: [Descriptor, Locator][]): Promise<void>
```

--------------------------------

### Symbolic Links

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Create symbolic links asynchronously or synchronously.

```APIDOC
## POST /fs/symlinkPromise

### Description
Asynchronously creates a symbolic link.

### Method
POST

### Endpoint
/fs/symlinkPromise

### Parameters
#### Request Body
- **target** (PortablePath) - Required - The path the symbolic link points to.
- **p** (PortablePath) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of symbolic link (e.g., 'file', 'dir').

### Request Example
```json
{
  "target": "/path/to/original",
  "p": "/path/to/symlink",
  "type": "file"
}
```

### Response
#### Success Response (200)
- **message** (string) - Indicates successful creation.

#### Response Example
```json
{
  "message": "Symbolic link created successfully."
}
```

## POST /fs/symlinkSync

### Description
Synchronously creates a symbolic link.

### Method
POST

### Endpoint
/fs/symlinkSync

### Parameters
#### Request Body
- **target** (PortablePath) - Required - The path the symbolic link points to.
- **p** (PortablePath) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of symbolic link (e.g., 'file', 'dir').

### Request Example
```json
{
  "target": "/path/to/original",
  "p": "/path/to/symlink",
  "type": "dir"
}
```

### Response
#### Success Response (200)
- **message** (string) - Indicates successful creation.

#### Response Example
```json
{
  "message": "Symbolic link created successfully."
}
```
```

--------------------------------

### statSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/PosixFS

Synchronously gets file status. Overloaded to handle different options for bigint and throwIfNoEntry.

```APIDOC
## GET /statSync

### Description
Synchronously gets file status. This function is overloaded to handle different options for bigint and throwIfNoEntry.

### Method
GET

### Endpoint
/statSync

### Parameters
#### Path Parameters
- **p** (NativePath) - Required - The path to the file.
- **opts** (StatSyncOptions) - Optional - Options for the stat operation, including `bigint` and `throwIfNoEntry`.

### Response
#### Success Response (200)
- **Stats** - File statistics object.
- **undefined** - If `throwIfNoEntry` is false and the file does not exist.
- **BigIntStats** - If `bigint` option is true.

#### Response Example
```json
{
  "dev": 21, "mode": 33188, "nlink": 1, "uid": 1000, "gid": 1000, "rdev": 0, "blksize": 4096, "ino": 123456789, "size": 1024, "blocks": 8, "atimeMs": 1678886400000, "mtimeMs": 1678886400000, "ctimeMs": 1678886400000, "atime": "2023-03-15T12:00:00.000Z", "mtime": "2023-03-15T12:00:00.000Z", "ctime": "2023-03-15T12:00:00.000Z"
}
```
```

--------------------------------

### GET /____supportsDescriptor

Source: https://yarnpkg.com/api/plugin-http/class/TarballHttpResolver

Checks if the resolver supports a given descriptor.

```APIDOC
## GET /____supportsDescriptor

### Description
This function must return true if the specified descriptor is intended to be turned into a locator by this resolver. If it returns false, other functions (except its locator counterpart) will not be called.

### Method
GET

### Endpoint
/____supportsDescriptor

### Parameters
#### Query Parameters
- **descriptor** (Descriptor) - Required - The descriptor that needs to be validated.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **boolean** - True if the resolver supports the descriptor, false otherwise.

#### Response Example
```json
true
```
```

--------------------------------

### JavaScript Check for Plug'n'Play Environment

Source: https://yarnpkg.com/advanced/pnpapi

Demonstrates how to check if the current environment is running under Plug'n'Play by inspecting the `process.versions.pnp` property.

```javascript
if (process.versions.pnp) {
  // do something with the PnP API ...
} else {
  // fallback
}

```

--------------------------------

### resolve API

Source: https://yarnpkg.com/api/plugin-npm/class/NpmSemverResolver

Retrieves the full package definition for a given locator. This function is used to get detailed information about a specific package.

```APIDOC
## GET /websites/yarnpkg/resolve

### Description
Given a locator, returns the full package definition for the package pointed at.

### Method
GET

### Endpoint
/websites/yarnpkg/resolve

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The source locator.
- **opts** (ResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **bin** (Map<string, PortablePath>) - Map of binary executables.
- **conditions** (null | string) - Package conditions.
- **dependencies** (Map<IdentHash, Descriptor>) - Package dependencies.
- **dependenciesMeta** (Map<string, Map<null | string, DependencyMeta>>) - Metadata for package dependencies.
- **identHash** (IdentHash) - Hash identifier for the package.
- **languageName** (string) - The language name of the package.
- **linkType** (LinkType) - The type of link used for the package.
- **locatorHash** (LocatorHash) - Hash identifier for the locator.
- **name** (string) - The name of the package.
- **peerDependencies** (Map<IdentHash, Descriptor>) - Package peer dependencies.
- **peerDependenciesMeta** (Map<string, PeerDependencyMeta>) - Metadata for package peer dependencies.
- **reference** (string) - The reference string for the package.
- **scope** (null | string) - The scope of the package.
- **version** (string) - The version of the package.

#### Response Example
```json
{
  "bin": {},
  "conditions": null,
  "dependencies": new Map(),
  "dependenciesMeta": new Map(),
  "identHash": "some-hash",
  "languageName": "typescript",
  "linkType": "hard",
  "locatorHash": "locator-hash",
  "name": "example-package",
  "peerDependencies": new Map(),
  "peerDependenciesMeta": new Map(),
  "reference": "npm:example-package@1.0.0",
  "scope": null,
  "version": "1.0.0"
}
```
```

--------------------------------

### Directory Creation (mkdirp) Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NodeFS

Provides methods for recursively creating directories (mkdirp) asynchronously with promises or synchronously, with options for chmod and utimes.

```APIDOC
## mkdirpPromise

### Description
Asynchronously ensures that a directory exists, creating it and any necessary parent directories if they do not exist. Supports custom chmod and utimes.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirpPromise

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path of the directory to ensure exists.
- **chmod** (number) - Optional - The mode to use when creating directories.
- **utimes** ([string | number | Date, string | number | Date]) - Optional - The access and modification times to use when creating directories.

### Request Example
```json
{
  "p": "/path/to/deeply/nested/directory",
  "chmod": 4096,
  "utimes": ["2023-10-27T10:00:00Z", "2023-10-27T11:00:00Z"]
}
```

### Response
#### Success Response (200)
- **undefined | string** - Returns the resolved path if created, otherwise undefined.

#### Response Example
```json
"/path/to/deeply/nested/directory"
```

## mkdirpSync

### Description
Synchronously ensures that a directory exists, creating it and any necessary parent directories if they do not exist. Supports custom chmod and utimes.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirpSync

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path of the directory to ensure exists.
- **chmod** (number) - Optional - The mode to use when creating directories.
- **utimes** ([string | number | Date, string | number | Date]) - Optional - The access and modification times to use when creating directories.

### Request Example
```json
{
  "p": "/path/to/deeply/nested/directory",
  "chmod": 4096,
  "utimes": ["2023-10-27T10:00:00Z", "2023-10-27T11:00:00Z"]
}
```

### Response
#### Success Response (200)
- **undefined | string** - Returns the resolved path if created, otherwise undefined.

#### Response Example
```json
"/path/to/deeply/nested/directory"
```
```

--------------------------------

### Get Supported Architectures in Yarn

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Returns a set of supported architectures for the current environment. This method does not take any parameters.

```typescript
declare __getSupportedArchitectures(): ArchitectureSet;

```

--------------------------------

### watch - Watch for File System Events

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Starts watching a path for file system events. Can be used with or without options.

```APIDOC
## POST /fs/watch

### Description
Starts watching a path for file system events.

### Method
POST

### Endpoint
/fs/watch

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to watch.
- **cb** (WatchCallback) - Optional - The callback function to handle events.
- **opts** (WatchOptions) - Optional - Options for watching.

### Request Example
```json
{
  "p": "/path/to/watch",
  "opts": {
    "persistent": true
  }
}
```

### Response
#### Success Response (200)
- **watcher** (Watcher) - An object representing the file system watcher.
```

--------------------------------

### Stat Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/AliasFS

Provides methods to get file status information.

```APIDOC
## GET /__statPromise

### Description
Gets file status information asynchronously.

### Method
GET

### Endpoint
/__statPromise

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
#### Query Parameters
- **opts** (undefined | (StatOptions & { bigint?: false })) - Optional - Options for stat operation (non-bigint).
- **opts** (StatOptions & { bigint: true }) - Optional - Options for stat operation (bigint).

### Response
#### Success Response (200)
- **Promise<Stats>** - A promise that resolves with file status information (Stats).
- **Promise<BigIntStats>** - A promise that resolves with file status information (BigIntStats).

#### Response Example
{
  "example": {
    "dev": 2112,
    "ino": 5820465,
    "mode": 16893,
    "nlink": 1,
    "uid": 501,
    "gid": 20,
    "rdev": 0,
    "size": 1024,
    "atimeMs": 1678886400000,
    "mtimeMs": 1678886400000,
    "ctimeMs": 1678886400000,
    "birthtimeMs": 1678886400000
  }
}

## GET /__statSync

### Description
Gets file status information synchronously.

### Method
GET

### Endpoint
/__statSync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
#### Query Parameters
- **opts** (StatSyncOptions & { bigint?: false; throwIfNoEntry: false }) - Optional - Options for stat operation (non-bigint, no throw).
- **opts** (StatSyncOptions & { bigint: true; throwIfNoEntry: false }) - Optional - Options for stat operation (bigint, no throw).
- **opts** (StatSyncOptions & { bigint?: false }) - Optional - Options for stat operation (non-bigint).
- **opts** (StatSyncOptions & { bigint: true }) - Optional - Options for stat operation (bigint).
- **opts** (StatSyncOptions & { bigint: boolean; throwIfNoEntry?: false }) - Optional - Options for stat operation (boolean bigint, no throw).

### Response
#### Success Response (200)
- **Stats** - File status information.
- **undefined** - If `throwIfNoEntry` is false and the file does not exist.
- **BigIntStats** - File status information with bigint values.

#### Response Example
{
  "example": {
    "dev": 2112,
    "ino": 5820465,
    "mode": 16893,
    "nlink": 1,
    "uid": 501,
    "gid": 20,
    "rdev": 0,
    "size": 1024,
    "atimeMs": 1678886400000,
    "mtimeMs": 1678886400000,
    "ctimeMs": 1678886400000,
    "birthtimeMs": 1678886400000
  }
}
```

--------------------------------

### GET /resolve

Source: https://yarnpkg.com/api/plugin-exec/class/ExecResolver

Retrieves the full package definition for a given locator. This function resolves a locator to its complete package information.

```APIDOC
## GET /resolve

### Description
Given a locator, this function returns the full package definition for the package it points to.

### Method
GET

### Endpoint
/resolve

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The source locator of the package.
- **opts** (ResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **bin** (Map<string, PortablePath>) - Binary files associated with the package.
- **conditions** (string | null) - Package conditions.
- **dependencies** (Map<IdentHash, Descriptor>) - Package dependencies.
- **dependenciesMeta** (Map<string, Map<null | string, DependencyMeta>>) - Metadata for dependencies.
- **identHash** (IdentHash) - Hash identifier for the package.
- **languageName** (string) - The programming language name associated with the package.
- **linkType** (LinkType) - The type of link for the package.
- **locatorHash** (LocatorHash) - Hash identifier for the locator.
- **name** (string) - The name of the package.
- **peerDependencies** (Map<IdentHash, Descriptor>) - Peer dependencies of the package.
- **peerDependenciesMeta** (Map<string, PeerDependencyMeta>) - Metadata for peer dependencies.
- **reference** (string) - The reference string for the package.
- **scope** (string | null) - The scope of the package.
- **version** (string) - The version of the package.

#### Response Example
```json
{
  "bin": {
    "my-command": "/path/to/bin/my-command"
  },
  "conditions": null,
  "dependencies": {},
  "dependenciesMeta": {},
  "identHash": "abc123xyz",
  "languageName": "typescript",
  "linkType": "hard",
  "locatorHash": "def456uvw",
  "name": "my-package",
  "peerDependencies": {},
  "peerDependenciesMeta": {},
  "reference": "1.0.0",
  "scope": null,
  "version": "1.0.0"
}
```
```

--------------------------------

### Use Yarn Bundle for CI (Shell)

Source: https://yarnpkg.com/blog/2016/11/24/offline-mirror

Illustrates how to use a bundled Yarn JavaScript file for running commands like 'install' on CI systems without internet access. This approach ensures consistent Yarn versions across different operating system environments.

```shell
node ./yarn-0.23.2.js install

```

--------------------------------

### GET /____resolve

Source: https://yarnpkg.com/api/plugin-http/class/TarballHttpResolver

Resolves a given locator to its full package definition, including dependencies and metadata.

```APIDOC
## GET /____resolve

### Description
Given a locator, this function returns the full package definition for the package it points to. This includes details like binary paths, conditions, dependencies, metadata, and version information.

### Method
GET

### Endpoint
/____resolve

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The source locator.
- **opts** (ResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **bin** (Map<string, PortablePath>) - Map of binary paths.
- **conditions** (null | string) - Package conditions.
- **dependencies** (Map<IdentHash, Descriptor>) - Package dependencies.
- **dependenciesMeta** (Map<string, Map<null | string, DependencyMeta>>) - Dependency metadata.
- **identHash** (IdentHash) - Hash of the package identifier.
- **languageName** (string) - The name of the language for the package.
- **linkType** (LinkType) - The type of link for the package.
- **locatorHash** (LocatorHash) - Hash of the locator.
- **name** (string) - The name of the package.
- **peerDependencies** (Map<IdentHash, Descriptor>) - Peer dependencies.
- **peerDependenciesMeta** (Map<string, PeerDependencyMeta>) - Peer dependency metadata.
- **reference** (string) - The reference string for the package.
- **scope** (null | string) - The scope of the package.
- **version** (string) - The version of the package.

#### Response Example
```json
{
  "bin": {},
  "conditions": null,
  "dependencies": {},
  "dependenciesMeta": {},
  "identHash": "some-hash",
  "languageName": "typescript",
  "linkType": "hard",
  "locatorHash": "another-hash",
  "name": "my-package",
  "peerDependencies": {},
  "peerDependenciesMeta": {},
  "reference": "npm:my-package@1.0.0",
  "scope": null,
  "version": "1.0.0"
}
```
```

--------------------------------

### File Stat Operations (lstat)

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NodeFS

Provides methods to get file status information (lstat) asynchronously with promises or synchronously.

```APIDOC
## lstatPromise

### Description
Asynchronously retrieves status information about a file or directory, similar to `fs.lstat`. It does not follow symbolic links.

### Method
POST

### Endpoint
/websites/yarnpkg/lstatPromise

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path to the file or directory.
- **opts** (StatOptions & { bigint?: false }) - Optional - Options for stat. If `bigint` is false or omitted, returns `Stats`.
- **opts** (StatOptions & { bigint: true }) - Optional - Options for stat. If `bigint` is true, returns `BigIntStats`.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "bigint": false
  }
}
```

### Response
#### Success Response (200)
- **Stats | BigIntStats** - An object containing file status information.

#### Response Example
```json
{
  "isFile": true,
  "isDirectory": false,
  "size": 1024
}
```

## lstatSync

### Description
Synchronously retrieves status information about a file or directory, similar to `fs.lstatSync`. It does not follow symbolic links.

### Method
POST

### Endpoint
/websites/yarnpkg/lstatSync

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path to the file or directory.
- **opts** (StatSyncOptions & { bigint?: false; throwIfNoEntry?: false }) - Optional - Options for stat sync. If `throwIfNoEntry` is false, may return `undefined`.
- **opts** (StatSyncOptions & { bigint: true; throwIfNoEntry?: false }) - Optional - Options for stat sync. If `bigint` is true and `throwIfNoEntry` is false, may return `undefined`.
- **opts** (StatSyncOptions & { bigint?: false }) - Optional - Options for stat sync. If `bigint` is false or omitted, returns `Stats`.
- **opts** (StatSyncOptions & { bigint: true }) - Optional - Options for stat sync. If `bigint` is true, returns `BigIntStats`.
- **opts** (StatSyncOptions & { bigint: boolean; throwIfNoEntry?: false }) - Optional - Options for stat sync. If `throwIfNoEntry` is false, may return `Stats` or `BigIntStats`.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "throwIfNoEntry": false
  }
}
```

### Response
#### Success Response (200)
- **Stats | BigIntStats | undefined** - An object containing file status information, or undefined if `throwIfNoEntry` is false and the entry does not exist.

#### Response Example
```json
{
  "isFile": true,
  "isDirectory": false,
  "size": 1024
}
```
```

--------------------------------

### Set Initialization Fields in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

Specifies additional fields to be set when creating packages using the `init` command. This example sets the homepage field.

```YAML
initFields:
  homepage: "https://yarnpkg.com"
```

--------------------------------

### ESLint Configuration with pnpm

Source: https://yarnpkg.com/package_name=eslint

These settings in a `.npmrc` file ensure that pnpm installs dependencies in a manner compatible with npm, reducing potential errors when using ESLint with pnpm.

```ini
auto-install-peers=true
node-linker=hoisted
```

--------------------------------

### Yarn Unplug Command Usage

Source: https://yarnpkg.com/cli/unplug

Illustrates the basic command-line usage for the 'yarn unplug' command. It shows how to initiate the unplugging process for packages.

```bash
yarn unplug ...
```

--------------------------------

### File System Operations (fstat)

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Provides synchronous and asynchronous methods to get file status information.

```APIDOC
## __fstatSync / __fstatPromise

### Description
Synchronously or asynchronously retrieves file status information for a given file descriptor.

### Method
`__fstatSync(fd: number): Stats`
`__fstatSync(fd: number, opts: { bigint: true }): BigIntStats`
`__fstatSync(fd: number, opts?: { bigint?: boolean }): Stats | BigIntStats`

`__fstatPromise(fd: number): Promise<Stats>`
`__fstatPromise(fd: number, opts: { bigint: true }): Promise<BigIntStats>`
`__fstatPromise(fd: number, opts?: { bigint?: boolean }): Promise<Stats | BigIntStats>`

### Parameters
#### Path Parameters
- **fd** (number) - Required - The file descriptor.
- **opts** (object) - Optional - Options for retrieving stats. Can include `bigint: true` for BigIntStats.
  - **bigint** (boolean) - Optional - If true, returns `BigIntStats`.

### Response
#### Success Response
- **Stats** - File status information.
- **BigIntStats** - File status information with BigInt values.

#### Response Example
```json
{
  "dev": 21, 
  "mode": 33188,
  "nlink": 1,
  "uid": 501,
  "gid": 20,
  "rdev": 0,
  "blksize": 4096,
  "ino": 1234567890,
  "size": 1024,
  "blocks": 8,
  "atimeMs": 1678886400000,
  "mtimeMs": 1678886400000,
  "ctimeMs": 1678886400000,
  "birthtimeMs": 1678886400000
}
```
```

--------------------------------

### ZipFS Constructors

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Details on how to construct a ZipFS instance, either from a path or buffer.

```APIDOC
## Constructors

### `__new ZipFS(): ZipFS`

Creates a new, empty ZipFS instance.

### `__new ZipFS(p: PortablePath, opts?: ZipPathOptions): ZipFS`

Creates a new ZipFS instance by reading from the specified portable path.

*   **Parameters**:
    *   `p` (PortablePath) - The path to the zip file.
    *   `opts` (ZipPathOptions, optional) - Options for reading the zip file.

### `__new ZipFS(data: null | Buffer<ArrayBufferLike>, opts?: ZipBufferOptions): ZipFS`

Creates a new ZipFS instance from the provided buffer data.

*   **Parameters**:
    *   `data` (null | Buffer<ArrayBufferLike>) - The buffer containing zip file data.
    *   `opts` (ZipBufferOptions, optional) - Options for reading the zip data from a buffer.

#### Returns
ZipFS - The constructed ZipFS instance.
```

--------------------------------

### Yarn Workspaces Foreach Publish All Packages

Source: https://yarnpkg.com/cli/workspaces/foreach

Example of publishing all packages using 'yarn workspaces foreach'. The '-A' flag ensures all workspaces are included, and '--no-private' prevents private packages from being published. 'npm publish --tolerate-republish' is the command executed.

```bash
yarn workspaces foreach -A --no-private npm publish --tolerate-republish
```

--------------------------------

### GET /supportsLocator

Source: https://yarnpkg.com/api/yarnpkg-core/class/LegacyMigrationResolver

Checks if the resolver supports a given locator. This function ensures that the locator is of a type that this resolver can process into a package definition.

```APIDOC
## GET /supportsLocator

### Description
Returns `true` if the specified locator is intended to be turned into a package definition by this resolver. If `false`, other functions (except its locator counterpart) will not be called for this locator.

### Method
GET

### Endpoint
/supportsLocator

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The locator that needs to be validated.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **boolean** - `true` if the locator is supported, `false` otherwise.

#### Response Example
```json
{
  "supported": true
}
```
```

--------------------------------

### shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-npm/class/NpmRemapResolver

Determines if a package definition for a given locator should be persisted between installs. Typically true for cached packages and false for workspace-related packages.

```APIDOC
## GET /shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. Returns true for cached packages and false for packages hydrated directly from the filesystem (e.g., workspaces).

### Method
GET

### Endpoint
/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- Returns a boolean indicating whether the resolution should be persisted (type: never, indicates an incomplete function signature in the source, actual return type would be boolean).

#### Response Example
```json
// Actual return type is boolean, 'never' indicates an incomplete signature in the source.
true
```
```

--------------------------------

### prepareForPack

Source: https://yarnpkg.com/api/plugin-pack/namespace/packUtils

Prepares a workspace for packing, executing a callback upon completion.

```APIDOC
## prepareForPack

### Description
Prepares a workspace for packing, executing a callback upon completion.

### Method
N/A (Function)

### Endpoint
N/A (Function)

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
  "workspace": "Workspace object",
  "report": "Report object",
  "cb": "() => Promise<void>"
}
```

### Response
#### Success Response (200)
- **Promise<void>** (void) - A promise that resolves when preparation is complete.

#### Response Example
```json
null
```
```

--------------------------------

### Yarnpkg: Get Workspaces

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Selects all workspaces matching the provided filter. If no filter is provided, it returns all workspaces.

```typescript
/**
 * Select all matching workspaces according to the provided filter.
 * @param filter Optional filter to apply to the workspaces.
 * @returns An array of Workspace objects.
 */
__workspaces(filter?: WorkspaceFilter): Workspace[];
```

--------------------------------

### GithubFetcher Constructor

Source: https://yarnpkg.com/api/plugin-github/class/GithubFetcher

Initializes a new instance of the GithubFetcher. This constructor is part of the GithubFetcher class, which handles fetching package data from GitHub repositories.

```typescript
new GithubFetcher(): GithubFetcher
```

--------------------------------

### VSCode Settings for Yarn Plug'n'Play TypeScript

Source: https://yarnpkg.com/getting-started/editor-sdks

Generates the `.vscode/settings.json` file to configure VSCode for Yarn Plug'n'Play. This allows VSCode to correctly resolve TypeScript versions and type definitions from your project's PnP installation.

```bash
yarn dlx @yarnpkg/sdks vscode
```

--------------------------------

### Get File Stats Asynchronously

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Asynchronously retrieves statistics for a file. Can return either standard Stats or BigIntStats based on the options.

```APIDOC
## __statPromise

### Description
Asynchronously retrieves statistics for a file.

### Method
Not Applicable (Asynchronous function)

### Endpoint
Not Applicable (Local file system operation)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "p": "/path/to/file"
}
```
Or with options:
```json
{
  "p": "/path/to/file",
  "opts": {
    "bigint": true
  }
}
```

### Response
#### Success Response (Promise<Stats | BigIntStats>)
Returns a Promise that resolves with the file statistics. The type of statistics (Stats or BigIntStats) depends on the `bigint` option.

#### Response Example
```json
{
  "dev": 2112,
  "ino": 491785,
  "mode": 33188,
  "nlink": 1,
  "uid": 1000,
  "gid": 1000,
  "rdev": 0,
  "size": 1024,
  "blksize": 4096,
  "blocks": 8,
  "atimeMs": 1678886400000.0,
  "mtimeMs": 1678886400000.0,
  "ctimeMs": 1678886400000.0,
  "atime": "2023-03-15T12:00:00.000Z",
  "mtime": "2023-03-15T12:00:00.000Z",
  "ctime": "2023-03-15T12:00:00.000Z"
}
```
```

--------------------------------

### Run Scripts with Yarn

Source: https://context7.com/context7/yarnpkg/llms.txt

Executes scripts defined in package.json or binaries from installed dependencies. Supports shorthands, Node.js debugging, running scripts from the root workspace, and binary-only execution.

```bash
# Run script from package.json
yarn run test

# Shorthand (omit "run")
yarn test

# Run with Node.js debugger
yarn run --inspect-brk webpack

# Run from root workspace instead of current
yarn run build --top-level

# Run binary only (ignore scripts)
yarn run eslint --binaries-only

# Run global script (with colon) from anywhere in project
yarn workspace:build
```

--------------------------------

### Create Directory for node_modules Project

Source: https://yarnpkg.com/getting-started/recipes

Creates a new directory intended to house a project that will use the `node_modules` linker, typically for compatibility with tools that do not support Plug'n'Play (PnP).

```bash
mkdir nm-packages/myproj
touch nm-packages/myproj/yarn.lock
```

--------------------------------

### Get Readme Content (TypeScript)

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmPublishUtils

Asynchronously retrieves the content of the README file for a given workspace. Returns a Promise that resolves to the README content as a string.

```typescript
declare function __getReadmeContent(workspace: Workspace): Promise<string>;
```

--------------------------------

### PosixFS Methods

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/PosixFS

Lists and describes the available methods for interacting with the file system through PosixFS.

```APIDOC
## Methods

### `__accessPromise(p: NativePath, mode?: number): Promise<void>`

Asynchronously checks if a file exists and is accessible.

**Parameters:**
* `p` (NativePath): The path to the file.
* `mode` (number, optional): The access mode flags.

**Returns:**
* `Promise<void>`

### `__accessSync(p: NativePath, mode?: number): void`

Synchronously checks if a file exists and is accessible.

**Parameters:**
* `p` (NativePath): The path to the file.
* `mode` (number, optional): The access mode flags.

**Returns:**
* `void`

### `__appendFilePromise(p: FSPath<NativePath>, content: string | Uint8Array<ArrayBufferLike>, opts?: WriteFileOptions): Promise<void>`

Asynchronously appends data to a file.

**Parameters:**
* `p` (FSPath<NativePath>): The path to the file.
* `content` (string | Uint8Array<ArrayBufferLike>): The data to append.
* `opts` (WriteFileOptions, optional): Options for writing the file.

**Returns:**
* `Promise<void>`

### `__appendFileSync(p: FSPath<NativePath>, content: string | Uint8Array<ArrayBufferLike>, opts?: WriteFileOptions): void`

Synchronously appends data to a file.

**Parameters:**
* `p` (FSPath<NativePath>): The path to the file.
* `content` (string | Uint8Array<ArrayBufferLike>): The data to append.
* `opts` (WriteFileOptions, optional): Options for writing the file.

**Returns:**
* `void`

### `__changeFilePromise(p: NativePath, content: Buffer<ArrayBufferLike>): Promise<void>`

Asynchronously changes the content of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `content` (Buffer<ArrayBufferLike>): The new content for the file.

**Returns:**
* `Promise<void>`

### `__changeFilePromise(p: NativePath, content: string, opts?: Partial<{ automaticNewlines: boolean; mode: number }>): Promise<void>`

Asynchronously changes the content of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `content` (string): The new content for the file.
* `opts` (Partial<{ automaticNewlines: boolean; mode: number }>, optional): Options for changing the file content.

**Returns:**
* `Promise<void>`

### `__changeFileSync(p: NativePath, content: Buffer<ArrayBufferLike>): void`

Synchronously changes the content of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `content` (Buffer<ArrayBufferLike>): The new content for the file.

**Returns:**
* `void`

### `__changeFileSync(p: NativePath, content: string, opts?: Partial<{ automaticNewlines: boolean; mode: number }>): void`

Synchronously changes the content of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `content` (string): The new content for the file.
* `opts` (Partial<{ automaticNewlines: boolean; mode: number }>, optional): Options for changing the file content.

**Returns:**
* `void`

### `__checksumFilePromise(path: NativePath, __namedParameters?: { algorithm?: string }): Promise<string>`

Asynchronously calculates the checksum of a file.

**Parameters:**
* `path` (NativePath): The path to the file.
* `__namedParameters` (object, optional): Named parameters.
    * `algorithm` (string, optional): The algorithm to use for checksum calculation.

**Returns:**
* `Promise<string>`: The checksum of the file.

### `__chmodPromise(p: NativePath, mask: number): Promise<void>`

Asynchronously changes the permissions of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `mask` (number): The new permission mask.

**Returns:**
* `Promise<void>`

### `__chmodSync(p: NativePath, mask: number): void`

Synchronously changes the permissions of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `mask` (number): The new permission mask.

**Returns:**
* `void`

### `__chownPromise(p: NativePath, uid: number, gid: number): Promise<void>`

Asynchronously changes the ownership of a file.

**Parameters:**
* `p` (NativePath): The path to the file.
* `uid` (number): The new user ID.
* `gid` (number): The new group ID.

**Returns:**
* `Promise<void>`
```

--------------------------------

### File Stat Operations

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D/class/ZipOpenFS

Provides synchronous and asynchronous methods to get file status information.

```APIDOC
## STAT PROMISE

### Description
Asynchronously retrieves the status of a file.

### Method
`statPromise`

### Endpoint
N/A (Asynchronous function)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (StatOptions) - Optional - Options for retrieving statistics, including `bigint` for BigInt stats.

### Response
#### Success Response (Promise<Stats | BigIntStats>)
Returns a Promise that resolves with file status information.

### Response Example
```json
{
  "isFile": true,
  "isDirectory": false,
  "size": 1024,
  "mtimeMs": 1678886400000
}
```
```

```APIDOC
## STAT SYNC

### Description
Synchronously retrieves the status of a file.

### Method
`statSync`

### Endpoint
N/A (Synchronous function)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (StatSyncOptions) - Optional - Options for retrieving statistics, including `bigint` for BigInt stats and `throwIfNoEntry`.

### Response
#### Success Response (Stats | BigIntStats | undefined)
Returns file status information or undefined if `throwIfNoEntry` is false and the entry does not exist.

### Response Example
```json
{
  "isFile": true,
  "isDirectory": false,
  "size": 1024,
  "mtimeMs": 1678886400000
}
```
```

--------------------------------

### Yarn Info for Package Cache Details

Source: https://yarnpkg.com/cli/info

This example shows how to use the '--cache' flag with 'yarn info' to retrieve information about the package's cache entry, including its path, size, and checksum. This is useful for cache management and integrity checks.

```bash
yarn info --cache
```

--------------------------------

### Generate Base SDK with Yarn

Source: https://yarnpkg.com/getting-started/editor-sdks

This command generates only the base SDKs without any editor-specific configurations. This is useful when you only need the core SDK components for environments that can be configured manually or do not require specific editor integration files.

```bash
yarn dlx @yarnpkg/sdks base
```

--------------------------------

### Deprecating Bundle Dependencies - Package.json Example (JSON)

Source: https://yarnpkg.com/blog/release/2

Illustrates the format for specifying bundle dependencies in a package.json file. This feature is now deprecated in Yarn, and packages will be downloaded directly from their listed dependencies.

```json
{
  "bundleDependencies": [
    "not-supported-anymore"
  ]
}

```

--------------------------------

### General Yarn Configuration Settings

Source: https://context7.com/context7/yarnpkg/llms.txt

Details various configuration options available in .yarnrc.yml, including cache settings, installation behavior (nodeLinker, enableScripts), network configurations (timeouts, concurrency), and registry settings for npm scopes.

```yaml
# .yarnrc.yml

# Cache settings
cacheFolder: ./.yarn/cache
enableGlobalCache: false
compressionLevel: 0

# Install behavior
nodeLinker: pnp
enableScripts: true
enableImmutableInstalls: false  # true on CI

# Network settings
httpTimeout: 60000
networkConcurrency: 50
enableNetwork: true
enableStrictSsl: true

# Registry configuration
npmRegistryServer: https://registry.yarnpkg.com
npmScopes:
  my-company:
    npmRegistryServer: https://npm.pkg.github.com
    npmAuthToken: "${GITHUB_TOKEN}"
```

--------------------------------

### Add Package from GitHub Shorthand with Yarn

Source: https://yarnpkg.com/cli/add

A shorthand notation for adding packages from GitHub using just the repository owner and name, simplifying the GitHub dependency specification.

```bash
yarn add lodash@lodash/lodash

```

--------------------------------

### Yarn Dedupe: Deduplicate All Packages

Source: https://yarnpkg.com/cli/dedupe

Example of how to run the 'yarn dedupe' command to deduplicate all packages in the project. This is the default behavior when no specific package or strategy is provided.

```bash
yarn dedupe
```

--------------------------------

### List all peer requirements with yarn

Source: https://yarnpkg.com/cli/explain/peer-requirements

This command lists all available peer requirements, each associated with a unique hash. The output helps in identifying relevant hashes for further detailed explanations.

```bash
yarn explain peer-requirements
```

--------------------------------

### Get Target Path - getTarget

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Retrieves the target path. This function does not take any parameters and returns a PortablePath.

```typescript
declare function __getTarget(): PortablePath;
```

--------------------------------

### GET /____getSatisfying

Source: https://yarnpkg.com/api/plugin-http/class/TarballHttpResolver

Finds locators that potentially satisfy a given descriptor based on provided dependencies and options.

```APIDOC
## GET /____getSatisfying

### Description
Given a descriptor and a list of locators, this function determines which of the locators potentially satisfy the descriptor. It differs from `getCandidates` by statically computing satisfied references without network calls. The returned locators are sorted to prioritize preferred ones.

### Method
GET

### Endpoint
/____getSatisfying

### Parameters
#### Query Parameters
- **descriptor** (Descriptor) - Required - The target descriptor.
- **dependencies** (Record<string, Package>) - Required - The resolution dependencies and their resolutions.
- **locators** (Locator[]) - Required - The candidate locators.
- **opts** (ResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **locators** (Locator[]) - An array of locators that satisfy the descriptor, sorted by preference.
- **sorted** (boolean) - Indicates if the returned locators are sorted.

#### Response Example
```json
{
  "locators": [
    {
      "name": "example-package",
      "reference": "workspace:.",
      "range": "*"
    }
  ],
  "sorted": true
}
```
```

--------------------------------

### PNP API

Source: https://yarnpkg.com/api/yarnpkg-pnp

Functions for interacting with the Plug'n'Play package resolution system.

```APIDOC
## __PnpApi

### Description
Provides methods for finding package locators, resolving package information, and managing the dependency tree.

### Methods

#### `findPackageLocator`

*   **Description**: Finds the physical package locator for a given location.
*   **Parameters**:
    *   `location` (NativePath) - The path to search for.
*   **Returns**: `PhysicalPackageLocator | null`

#### `getAllLocators`

*   **Description**: Retrieves all available package locators.
*   **Returns**: `PhysicalPackageLocator[]`

#### `getDependencyTreeRoots`

*   **Description**: Gets the root locators of the dependency tree.
*   **Returns**: `PhysicalPackageLocator[]`

#### `getLocator`

*   **Description**: Retrieves a package locator by its name and reference.
*   **Parameters**:
    *   `name` (string) - The name of the package.
    *   `referencish` (string | [string, string]) - The reference identifier for the package.
*   **Returns**: `PhysicalPackageLocator`

#### `getPackageInformation`

*   **Description**: Gets detailed information about a package based on its locator.
*   **Parameters**:
    *   `locator` (PackageLocator) - The locator of the package.
*   **Returns**: `PackageInformation<NativePath> | null`

#### `resolveRequest`

*   **Description**: Resolves a package request relative to an issuer path, with optional resolution options.
*   **Parameters**:
    *   `request` (string) - The package request string.
    *   `issuer` (NativePath | null) - The issuer path, or null if not applicable.
    *   `opts` (ResolveRequestOptions) - Optional resolution settings.
*   **Returns**: `NativePath | null`

#### `resolveToUnqualified`

*   **Description**: Resolves a package request to an unqualified path, with optional resolution options.
*   **Parameters**:
    *   `request` (string) - The package request string.
    *   `issuer` (NativePath | null) - The issuer path, or null if not applicable.
    *   `opts` (ResolveToUnqualifiedOptions) - Optional resolution settings.
*   **Returns**: `NativePath | null`

#### `resolveUnqualified`

*   **Description**: Resolves an unqualified path, with optional resolution options.
*   **Parameters**:
    *   `unqualified` (NativePath) - The unqualified path to resolve.
    *   `opts` (ResolveUnqualifiedOptions) - Optional resolution settings.
*   **Returns**: `NativePath`

#### `resolveVirtual`

*   **Description**: Resolves a virtual path to its physical equivalent, if applicable.
*   **Parameters**:
    *   `p` (NativePath) - The virtual path to resolve.
*   **Returns**: `NativePath | null`

### Properties

*   **`VERSIONS`** (`{ std: number }`) - Contains version information for the PNP system.
*   **`topLevel`** (`{ name: null; reference: null }`) - Represents the top-level scope, typically with null name and reference.
```

--------------------------------

### Yarnpkg: Get Packages

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Selects all packages based on a provided filter. The filter can specify various criteria to narrow down the selection.

```typescript
/**
 * Select all dependencies according to the provided filter.
 * @param filter Optional filter to apply to the packages.
 * @returns An array of Package objects.
 */
__packages(filter: DependencyFilter): Package[];
```

--------------------------------

### Attach External Dependencies in PnpInstaller

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpInstaller

Links a package to the locations of its external dependencies. This method is guaranteed to be called for all packages before the install is finalized and is used for packages supported by different linkers.

```typescript
__attachExternalDependents(locator: Locator, dependentPaths: PortablePath[]): Promise<void>
```

--------------------------------

### RunCommand Constructor and Properties (TypeScript)

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/RunCommand

Demonstrates the constructor and key properties of the RunCommand class. Properties include arguments, command name, current working directory, paths, and usage information. This class is essential for managing and executing commands within the Yarnpkg environment.

```typescript
class RunCommand {
  __args: string[] = ...;
  __commandName: string = ...;
  __cwd: string = ...;
  static __paths: string[][] = ...;
  static __usage: Usage = ...;

  constructor() {
    // ...
  }
}
```

--------------------------------

### Get Yarn Linkers

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Returns an array of Linker objects used by Yarn. This method does not take any parameters.

```typescript
declare __getLinkers(): Linker[];

```

--------------------------------

### Yarn DLX Basic Usage

Source: https://yarnpkg.com/cli/dlx

This snippet shows the fundamental syntax for using 'yarn dlx'. It demonstrates how to invoke a command, which Yarn will then resolve and execute from a temporary environment. This is useful for running package binaries directly without adding them to project dependencies.

```bash
yarn dlx <command> ...
```

--------------------------------

### File Stat Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/ProxiedFS

Provides functions to get file status information, including synchronous and asynchronous versions, and options for bigint stats.

```APIDOC
## __statPromise

### Description
Asynchronously retrieves the status of a file.

### Method
GET

### Endpoint
/fs/stat

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
#### Query Parameters
- **bigint** (boolean) - Optional - If true, returns BigIntStats. Defaults to false.
- **throwIfNoEntry** (boolean) - Optional - If true, throws an error if the file does not exist. Defaults to true.

### Request Example
```json
{
  "path": "/path/to/stat",
  "bigint": false
}
```

### Response
#### Success Response (200)
- **Stats** or **BigIntStats** - File status information.

#### Response Example
```json
{
  "dev": 2112,
  "ino": 49151,
  "mode": 33188,
  "nlink": 1,
  "uid": 1000,
  "gid": 1000,
  "rdev": 0,
  "size": 1024,
  "blksize": 4096,
  "blocks": 8,
  "atimeMs": 1678886400000,
  "mtimeMs": 1678886400000,
  "ctimeMs": 1678886400000,
  "birthtimeMs": 1678886400000
}
```

## __statSync

### Description
Synchronously retrieves the status of a file.

### Method
GET

### Endpoint
/fs/stat/sync

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
#### Query Parameters
- **bigint** (boolean) - Optional - If true, returns BigIntStats. Defaults to false.
- **throwIfNoEntry** (boolean) - Optional - If true, throws an error if the file does not exist. Defaults to true.

### Request Example
```json
{
  "path": "/path/to/stat/sync",
  "bigint": false
}
```

### Response
#### Success Response (200)
- **Stats** or **BigIntStats** - File status information. Returns undefined if `throwIfNoEntry` is false and the file does not exist.

#### Response Example
```json
{
  "dev": 2112,
  "ino": 49151,
  "mode": 33188,
  "nlink": 1,
  "uid": 1000,
  "gid": 1000,
  "rdev": 0,
  "size": 1024,
  "blksize": 4096,
  "blocks": 8,
  "atimeMs": 1678886400000,
  "mtimeMs": 1678886400000,
  "ctimeMs": 1678886400000,
  "birthtimeMs": 1678886400000
}
```
```

--------------------------------

### File Status API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CwdFS

Provides functions to get file status information, supporting both standard Stats and BigIntStats.

```APIDOC
## fstatSync API

### Description
Synchronously gets the status of a file descriptor. Supports returning Stats or BigIntStats.

### Method
SYNCHRONOUS

### Endpoint
N/A (synchronous function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Example for Stats
const stats = fstatSync(fd);

// Example for BigIntStats
const bigIntStats = fstatSync(fd, { bigint: true });
```

### Response
#### Success Response
- **stats** (Stats | BigIntStats) - File status information.

#### Response Example
```json
{
  "dev": 21, 
  "mode": 33188,
  "nlink": 1,
  "uid": 501,
  "gid": 20,
  "rdev": 0,
  "blksize": 4096,
  "ino": 1234567890,
  "size": 1024,
  "blocks": 8,
  "atimeMs": 1678886400000.0,
  "mtimeMs": 1678886400000.0,
  "ctimeMs": 1678886400000.0,
  "birthtimeMs": 1678886400000.0
}
```
```

```APIDOC
## lstatPromise API

### Description
Asynchronously gets the status of a path. Supports returning Stats or BigIntStats.

### Method
ASYNC

### Endpoint
N/A (asynchronous function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Example for Stats
const stats = await lstatPromise('/path/to/file');

// Example for BigIntStats
const bigIntStats = await lstatPromise('/path/to/file', { bigint: true });
```

### Response
#### Success Response
- **stats** (Stats | BigIntStats) - File status information.

#### Response Example
```json
{
  "dev": 21,
  "mode": 33188,
  "nlink": 1,
  "uid": 501,
  "gid": 20,
  "rdev": 0,
  "blksize": 4096,
  "ino": 1234567890,
  "size": 1024,
  "blocks": 8,
  "atimeMs": 1678886400000.0,
  "mtimeMs": 1678886400000.0,
  "ctimeMs": 1678886400000.0,
  "birthtimeMs": 1678886400000.0
}
```
```

```APIDOC
## lstatSync API

### Description
Synchronously gets the status of a path. Supports returning Stats or BigIntStats, and can optionally not throw an error if the entry does not exist.

### Method
SYNCHRONOUS

### Endpoint
N/A (synchronous function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Example for Stats
const stats = lstatSync('/path/to/file');

// Example for BigIntStats with option to not throw
const statsOrUndefined = lstatSync('/path/to/file', { bigint: true, throwIfNoEntry: false });
```

### Response
#### Success Response
- **stats** (Stats | BigIntStats | undefined) - File status information, or undefined if `throwIfNoEntry` is false and the entry does not exist.

#### Response Example
```json
{
  "dev": 21,
  "mode": 33188,
  "nlink": 1,
  "uid": 501,
  "gid": 20,
  "rdev": 0,
  "blksize": 4096,
  "ino": 1234567890,
  "size": 1024,
  "blocks": 8,
  "atimeMs": 1678886400000.0,
  "mtimeMs": 1678886400000.0,
  "ctimeMs": 1678886400000.0,
  "birthtimeMs": 1678886400000.0
}
```
```

--------------------------------

### WorkspaceResolver Methods

Source: https://yarnpkg.com/api/yarnpkg-core/class/WorkspaceResolver

This section details the methods available in the WorkspaceResolver for handling package resolution, including binding descriptors, getting candidate locators, and retrieving resolution dependencies.

```APIDOC
## WorkspaceResolver API Documentation

### Description
Provides methods for resolving package descriptors into specific package locators, considering various resolution strategies and dependencies.

### Methods

#### `__bindDescriptor`

##### Description
Binds a descriptor to a specific locator, potentially modifying it based on the context of the dependent package.

##### Method
POST

##### Endpoint
`/workspace-resolver/__bindDescriptor`

##### Parameters

###### Path Parameters
None

###### Query Parameters
None

###### Request Body
- **descriptor** (Descriptor) - Required - The descriptor to bind.
- **fromLocator** (Locator) - Required - The locator of the package that depends on the descriptor.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

##### Request Example
```json
{
  "descriptor": {
    "name": "example-package",
    "range": "^1.0.0"
  },
  "fromLocator": {
    "name": "parent-package",
    "reference": "1.2.3"
  },
  "opts": {
    "someOption": true
  }
}
```

##### Response

###### Success Response (200)
- **descriptor** (Descriptor) - The potentially modified descriptor.

###### Response Example
```json
{
  "descriptor": {
    "name": "example-package",
    "range": "1.2.3",
    "resolvedFrom": {
      "name": "parent-package",
      "reference": "1.2.3"
    }
  }
}
```

#### `__getCandidates`

##### Description
Retrieves a list of potential package locators that satisfy a given descriptor.

##### Method
POST

##### Endpoint
`/workspace-resolver/__getCandidates`

##### Parameters

###### Path Parameters
None

###### Query Parameters
None

###### Request Body
- **descriptor** (Descriptor) - Required - The descriptor to find candidates for.
- **dependencies** (unknown) - Required - The resolution dependencies and their current resolutions.
- **opts** (ResolveOptions) - Required - The resolution options.

##### Request Example
```json
{
  "descriptor": {
    "name": "example-package",
    "range": "^1.0.0"
  },
  "dependencies": {},
  "opts": {
    "loose": false
  }
}
```

##### Response

###### Success Response (200)
- **locators** (Array<Locator>) - An array of locators that satisfy the descriptor, sorted by preference.

###### Response Example
```json
{
  "locators": [
    {
      "name": "example-package",
      "reference": "1.2.3"
    },
    {
      "name": "example-package",
      "reference": "1.5.0"
    }
  ]
}
```

#### `__getResolutionDependencies`

##### Description
Determines the set of descriptors that must be resolved before the given descriptor can be resolved.

##### Method
POST

##### Endpoint
`/workspace-resolver/__getResolutionDependencies`

##### Parameters

###### Path Parameters
None

###### Query Parameters
None

###### Request Body
- **descriptor** (Descriptor) - Required - The descriptor for which to find dependencies.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

##### Request Example
```json
{
  "descriptor": {
    "name": "example-package",
    "range": "^1.0.0"
  },
  "opts": {
    "someOption": true
  }
}
```

##### Response

###### Success Response (200)
- **dependencies** (Object) - An object representing the descriptors that need to be resolved first.

###### Response Example
```json
{
  "dependencies": {
    "sub-dependency": {
      "name": "sub-dependency",
      "range": "~2.0.0"
    }
  }
}
```
```

--------------------------------

### shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-link/class/LinkResolver

Indicates whether the package definition for a given locator should be persisted between installs. Typically used to differentiate between cached packages and those that are dynamically resolved (e.g., from workspaces).

```APIDOC
## GET /_shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. Returns true for cached packages and false for packages hydrated directly from the filesystem (like workspaces).

### Method
GET

### Endpoint
/_shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **persist** (boolean) - True if the resolution should be persisted, false otherwise.

#### Response Example
```json
{
  "persist": true
}
```
```

--------------------------------

### shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-file/class/TarballFileResolver

Determines if a package definition should be persisted between installations. This is typically true for cached packages and false for packages resolved directly from the filesystem (e.g., in workspaces).

```APIDOC
## shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. Generally, this should return true for cached packages and false for packages that hydrate directly from the filesystem, such as those in workspaces. Packages returning false are still stored in the lockfile, but their definitions will be resolved again on the next install.

### Method
`shouldPersistResolution(locator: Locator, opts: MinimalResolveOptions): boolean`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "locator": {
    "name": "my-package",
    "reference": "1.0.0",
    "scope": null
  },
  "opts": {}
}
```

### Response
#### Success Response (200)
- **result** (boolean) - True if the resolution should persist, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Yarn Link Specific Workspaces

Source: https://yarnpkg.com/cli/link

This example shows how to link specific remote workspaces into the current project. You provide the paths to the desired workspaces as arguments to the 'yarn link' command.

```bash
yarn link ~/ts-loader ~/jest
```

--------------------------------

### Run Unit Tests with Yarn

Source: https://yarnpkg.com/advanced/contributing

This command executes the unit test suite for the Yarn project. Unit tests are crucial for verifying individual components and are accessible from any directory within the repository.

```bash
yarn test:unit
```

--------------------------------

### GET /supportsDescriptor

Source: https://yarnpkg.com/api/yarnpkg-core/class/LegacyMigrationResolver

Checks if the resolver supports a given descriptor. This function is a prerequisite for other resolver functions, ensuring the descriptor is of a type this resolver handles.

```APIDOC
## GET /supportsDescriptor

### Description
Returns `true` if the specified descriptor is intended to be turned into a locator by this resolver. If `false`, other functions (except its locator counterpart) will not be called for this descriptor.

### Method
GET

### Endpoint
/supportsDescriptor

### Parameters
#### Query Parameters
- **descriptor** (Descriptor) - Required - The descriptor that needs to be validated.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **boolean** - `true` if the descriptor is supported, `false` otherwise.

#### Response Example
```json
{
  "supported": true
}
```
```

--------------------------------

### GET /supportsLocator

Source: https://yarnpkg.com/api/plugin-exec/class/ExecResolver

Verifies if a given locator is intended to be resolved into a package definition by this resolver. If false, other resolver functions (except the descriptor counterpart) will not be called.

```APIDOC
## GET /supportsLocator

### Description
Returns true if the specified locator is meant to be turned into a package definition by this resolver. If it returns false, other functions (except its locator counterpart) will not be invoked.

### Method
GET

### Endpoint
/supportsLocator

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The locator to validate.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **result** (boolean) - True if the resolver supports the locator, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Manage Yarn Workspaces

Source: https://context7.com/context7/yarnpkg/llms.txt

Commands for managing monorepos configured with Yarn workspaces. Includes focusing installations on specific workspaces, running commands across multiple workspaces in parallel or topological order, and executing commands on changed workspaces.

```bash
# Focus install on specific workspace and its dependencies
yarn workspaces focus @my-org/app

# Focus on all workspaces, production dependencies only
yarn workspaces focus -A --production

# Run command on all workspaces in parallel, topological order
yarn workspaces foreach --all -pt npm publish

# Run on workspaces changed since main branch
yarn workspaces foreach --since run lint
```

--------------------------------

### Get System Architecture in Node.js

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/nodeUtils

Retrieves the current system's architecture details, including CPU, libc, and OS. This function returns an object conforming to the Architecture type.

```javascript
/**
 * @returns {Architecture}
 */
function __getArchitecture() {}
```

--------------------------------

### Get Cached Package Extensions in Yarn

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Computes and returns cached package extensions. This is an asynchronous operation.

```typescript
declare __getPackageExtensions(): Promise<PackageExtensions>;

```

--------------------------------

### Directory Opening Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NodeFS

Allows opening directories for reading, with options for buffer size and recursion.

```APIDOC
## POST /fs/opendirPromise

### Description
Asynchronously opens a directory for reading.

### Method
POST

### Endpoint
/fs/opendirPromise

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the directory to open.
- **opts** (object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - The size of the buffer to use.
  - **recursive** (boolean) - Whether to open the directory recursively.

### Response
#### Success Response (200)
- **dirHandle** (Dir<PortablePath>) - A handle to the opened directory.

#### Response Example
```json
{
  "dirHandle": { ... }
}
```

## POST /fs/opendirSync

### Description
Synchronously opens a directory for reading.

### Method
POST

### Endpoint
/fs/opendirSync

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the directory to open.
- **opts** (object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - The size of the buffer to use.
  - **recursive** (boolean) - Whether to open the directory recursively.

### Response
#### Success Response (200)
- **dirHandle** (Dir<PortablePath>) - A handle to the opened directory.

#### Response Example
```json
{
  "dirHandle": { ... }
}
```
```

--------------------------------

### Yarnpkg: Get Workspace Dependencies

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Selects all dependencies based on a provided filter. The filter can specify various criteria to narrow down the selection.

```typescript
/**
 * Select all dependencies according to the provided filter.
 * @param filter Optional filter to apply to the dependencies.
 * @returns An array of Dependency objects.
 */
__dependencies(filter?: DependencyFilter): Dependency[];
```

--------------------------------

### Configure Project Constraints with JavaScript

Source: https://context7.com/context7/yarnpkg/llms.txt

Defines project-wide rules using a JavaScript configuration file (yarn.config.cjs). This example shows how to enforce dependency versions, set engine requirements, and prohibit specific packages, demonstrating the power of constraint enforcement.

```javascript
// yarn.config.cjs
const { defineConfig } = require('@yarnpkg/types');

module.exports = defineConfig({
  async constraints({Yarn}) {
    // Enforce same React version across all workspaces
    for (const dep of Yarn.dependencies({ ident: 'react' })) {
      dep.update('18.0.0');
    }

    // Enforce engines.node field in all workspaces
    for (const workspace of Yarn.workspaces()) {
      workspace.set('engines.node', '>=18.0.0');
    }

    // Enforce consistent dependency versions
    for (const dependency of Yarn.dependencies()) {
      if (dependency.type === 'peerDependencies') continue;

      for (const otherDep of Yarn.dependencies({ident: dependency.ident})) {
        if (otherDep.type === 'peerDependencies') continue;
        dependency.update(otherDep.range);
      }
    }

    // Prohibit specific packages
    for (const dep of Yarn.dependencies({ ident: 'moment' })) {
      dep.delete();
      dep.workspace.set('dependencies.date-fns', '^2.0.0');
    }
  },
});
```

--------------------------------

### File System Operations (lstat)

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Provides synchronous and asynchronous methods to get file status information without following symlinks.

```APIDOC
## __lstatSync / __lstatPromise

### Description
Synchronously or asynchronously retrieves file status information for a given path, without following symbolic links.

### Method
`__lstatSync(p: PortablePath): Stats`
`__lstatSync(p: PortablePath, opts?: StatSyncOptions & { bigint?: false; throwIfNoEntry: false }): undefined | Stats`
`__lstatSync(p: PortablePath, opts: StatSyncOptions & { bigint: true; throwIfNoEntry: false }): undefined | BigIntStats`
`__lstatSync(p: PortablePath, opts?: StatSyncOptions & { bigint?: false }): Stats`
`__lstatSync(p: PortablePath, opts: StatSyncOptions & { bigint: true }): BigIntStats`
`__lstatSync(p: PortablePath, opts: StatSyncOptions & { bigint: boolean; throwIfNoEntry?: false }): Stats | BigIntStats`
`__lstatSync(p: PortablePath, opts?: StatSyncOptions): undefined | Stats | BigIntStats`

`__lstatPromise(p: PortablePath): Promise<Stats>`
`__lstatPromise(p: PortablePath, opts: undefined | (StatOptions & { bigint?: false })): Promise<Stats>`
`__lstatPromise(p: PortablePath, opts: StatOptions & { bigint: true }): Promise<BigIntStats>`
`__lstatPromise(p: PortablePath, opts?: StatOptions): Promise<Stats | BigIntStats>`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (object) - Optional - Options for retrieving stats. Can include `bigint: true` for BigIntStats.
  - **bigint** (boolean) - Optional - If true, returns `BigIntStats`.
  - **throwIfNoEntry** (boolean) - Optional - If true, throws an error if the path does not exist.

### Response
#### Success Response
- **Stats** - File status information.
- **BigIntStats** - File status information with BigInt values.
- **undefined** - If `throwIfNoEntry` is false and the path does not exist.

#### Response Example
```json
{
  "dev": 21,
  "mode": 33188,
  "nlink": 1,
  "uid": 501,
  "gid": 20,
  "rdev": 0,
  "blksize": 4096,
  "ino": 1234567890,
  "size": 1024,
  "blocks": 8,
  "atimeMs": 1678886400000,
  "mtimeMs": 1678886400000,
  "ctimeMs": 1678886400000,
  "birthtimeMs": 1678886400000
}
```
```

--------------------------------

### Execute Temporary Packages with Yarn DLX

Source: https://context7.com/context7/yarnpkg/llms.txt

Runs packages in ephemeral environments without permanent installation. Useful for scaffolding projects or executing one-off commands. Supports specifying versions and quiet mode.

```bash
# Scaffold new Vite project
yarn dlx create-vite

# Run with multiple packages
yarn dlx -p typescript -p ts-node ts-node --transpile-only -e "console.log('hello!')"

# Execute specific version
yarn dlx create-react-app@latest my-app

# Quiet mode (minimal output)
yarn dlx -q create-next-app --typescript
```

--------------------------------

### Generate Hello World Package with Exec Protocol (JavaScript)

Source: https://yarnpkg.com/protocol/exec

Generates a simple 'hello-world' package by writing 'package.json' and 'index.js' files into the build directory using Node.js built-in modules available globally. Uses `fs` and `path` for file operations.

```javascript
fs.writeFileSync(path.join(execEnv.buildDir, 'package.json'), JSON.stringify({
  name: 'hello-world',
  version: '1.0.0',
}));

fs.writeFileSync(path.join(execEnv.buildDir, 'index.js'), `
  module.exports = 'hello world!';
`);

```

--------------------------------

### Yarnpkg: Get Unique Package

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Selects a unique package based on a provided filter. Returns null if no matching package is found.

```typescript
/**
 * Select a unique workspace according to the provided filter.
 * @param filter Filter to apply to find the package.
 * @returns A Package object or null.
 */
__package(filter: DependencyFilter): null | Package;
```

--------------------------------

### Choose Node Linker Strategy in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

Selects the strategy for installing Node.js project dependencies. Available options are 'pnp' (Plug'n'Play), 'pnpm' (using symlinks/hardlinks to a global store), and 'node-modules' (standard node_modules folder).

```yaml
nodeLinker: "pnp"
```

--------------------------------

### mkdirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Asynchronously creates a directory. This is an abstract method.

```APIDOC
## mkdirPromise

### Description
Asynchronously creates a directory. This is an abstract method.

### Method
Promise<string | undefined>

### Endpoint
N/A (Abstract method)

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "example": "Not applicable"
}
```

### Response
#### Success Response (Promise<string | undefined>)
- **Type**: Promise<string | undefined>
- **Description**: A promise that resolves with the path of the created directory, or undefined.

#### Response Example
```json
{
  "example": "Not applicable"
}
```
```

--------------------------------

### Get Real Path - getRealPath

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Retrieves the real path of the current context. This function does not take any parameters and returns a PortablePath.

```typescript
declare function __getRealPath(): PortablePath;
```

--------------------------------

### mkdirpSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Synchronously creates a directory, including any necessary parent directories. This is an abstract method.

```APIDOC
## mkdirpSync

### Description
Synchronously creates a directory, including any necessary parent directories. This is an abstract method.

### Method
string | undefined

### Endpoint
N/A (Abstract method)

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "example": "Not applicable"
}
```

### Response
#### Success Response (string | undefined)
- **Type**: string | undefined
- **Description**: The path of the created directory, or undefined.

#### Response Example
```json
{
  "example": "Not applicable"
}
```
```

--------------------------------

### Yarn .pnp.data.json Manifest Structure

Source: https://yarnpkg.com/advanced/pnp-spec

Illustrates the JSON structure of the .pnp.data.json file generated by Yarn when pnpEnableInlining is set to false. It includes example data for header information, dependency tree roots, ignore patterns, fallback pools, and package registry data.

```json
__info: [
"This file is automatically generated. Do not touch it, or risk",
"your modifications being lost."
],

```

```json
dependencyTreeRoots: [{
name: "@app/monorepo",
reference: "workspace:."
}, {
name: "@app/website",
reference: "workspace:website"
}],

```

```json
ignorePatternData: "^examples(/|$)",

```

```json
enableTopLevelFallback: true,

```

```json
fallbackPool: [[
"@app/monorepo",
"workspace:."
]],

```

```json
fallbackExclusionList: [[
"@app/server",
["workspace:sources/server"]
]],

```

```json
packageRegistryData: [
[null, [
[null, {
packageLocation: "./",

```

--------------------------------

### Yarnpkg: Get Unique Dependency

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Selects a unique dependency based on a provided filter. Returns null if no matching dependency is found.

```typescript
/**
 * Select a unique workspace according to the provided filter.
 * @param filter Filter to apply to find the dependency.
 * @returns A Dependency object or null.
 */
__dependency(filter: DependencyFilter): null | Dependency;
```

--------------------------------

### Prettier Input and Output Example

Source: https://yarnpkg.com/package/prettier

Demonstrates the transformation of long, unformatted code into a consistently styled, more readable format using Prettier. This highlights Prettier's ability to manage line length and argument formatting.

```javascript
foo(reallyLongArg(), omgSoManyParameters(), IShouldRefactorThis(), isThereSeriouslyAnotherOne());
```

```javascript
foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne(),
);
```

--------------------------------

### Add PnPify Dependency using Yarn

Source: https://yarnpkg.com/advanced/pnpify

This command adds the PnPify package as a dependency to your project using Yarn. It ensures that the necessary tools for PnPify are installed.

```bash
yarn add @yarnpkg/pnpify
```

--------------------------------

### statPromise - Get File Stats Asynchronously

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously retrieves statistics for a file. Can return either standard stats or big-endian stats.

```APIDOC
## POST /fs/statPromise

### Description
Asynchronously retrieves statistics for a file.

### Method
POST

### Endpoint
/fs/statPromise

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **opts** (object) - Optional - Options for retrieving stats.
  - **bigint** (boolean) - If true, returns big-endian stats. Defaults to false.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "bigint": true
  }
}
```

### Response
#### Success Response (200)
- **stats** (Stats | BigIntStats) - File statistics.
```

--------------------------------

### PortalResolver Constructor - Yarnpkg

Source: https://yarnpkg.com/api/plugin-link/class/PortalResolver

Demonstrates the instantiation of the PortalResolver class in Yarnpkg. This is the entry point for creating a new resolver instance.

```typescript
new PortalResolver(): PortalResolver
```

--------------------------------

### shouldPersistResolution API

Source: https://yarnpkg.com/api/plugin-npm/class/NpmSemverResolver

Indicates whether the package definition for a given locator must be kept between installs. Typically true for cached packages and false for packages hydrated directly from the filesystem.

```APIDOC
## GET /websites/yarnpkg/shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. Returns true for cached packages and false for packages resolved directly from the filesystem (e.g., workspaces).

### Method
GET

### Endpoint
/websites/yarnpkg/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **persist** (boolean) - True if the resolution should be persisted, false otherwise.

#### Response Example
```json
{
  "persist": true
}
```
```

--------------------------------

### TarballFileFetcher Constructor

Source: https://yarnpkg.com/api/plugin-file/class/TarballFileFetcher

Information about the constructor for TarballFileFetcher.

```APIDOC
## __constructor TarballFileFetcher

### Description
Initializes a new instance of the TarballFileFetcher class.

### Method
CONSTRUCTOR

### Endpoint
N/A

### Parameters
None

### Request Example
```json
{
  "example": "new TarballFileFetcher()"
}
```

### Response
#### Success Response (200)
- **TarballFileFetcher** (TarballFileFetcher) - An instance of the TarballFileFetcher.

#### Response Example
```json
{
  "example": "<TarballFileFetcher instance>"
}
```
```

--------------------------------

### SdkCommand Constructor

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/SdkCommand

Initializes a new instance of the SdkCommand class. This constructor is the entry point for creating SdkCommand objects. It does not take any explicit arguments in its default form.

```typescript
new SdkCommand(): default
```

--------------------------------

### Get CLI Instance - @yarnpkg/cli

Source: https://yarnpkg.com/api/yarnpkg-cli

Retrieves an instance of the Yarn CLI. It allows specifying a custom working directory and plugin configuration. The function returns a Promise that resolves with the CLI instance and its default context, including path, plugins, and I/O streams.

```typescript
function __getCli(__namedParameters?: { cwd?: PortablePath; pluginConfiguration?: PluginConfiguration }): Promise<Cli<CommandContext> & { defaultContext: { cwd: PortablePath; plugins: PluginConfiguration; quiet: boolean; stderr: WriteStream & {}; stdin: ReadStream & {}; stdout: WritableStream & {} } }>
```

--------------------------------

### Yarn Info for Package Dependents

Source: https://yarnpkg.com/cli/info

This example shows how to use the '--dependents' flag with 'yarn info' to list all packages that depend on the specified package. This is helpful for understanding the impact of changes to a package.

```bash
yarn info --dependents
```

--------------------------------

### GET Package Metadata

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmHttpUtils

Retrieves package metadata from the npm registry. This function caches and returns specific fields from the metadata. For other fields, consider alternative methods.

```APIDOC
## GET /package/metadata

### Description
Caches and returns the package metadata for the given ident. Note: This function only caches and returns specific fields from the metadata. If you need other fields, use the uncached get or consider whether it would make more sense to extract the fields from the on-disk packages using the linkers or from the fetch results using the fetchers.

### Method
GET

### Endpoint
/package/metadata

### Parameters
#### Path Parameters
- **ident** (Ident) - Required - Identifier for the package.

#### Query Parameters
- **cache** (Cache) - Optional - Cache object for storing metadata.
- **project** (Project) - Required - Project context.
- **version** (string) - Optional - Specific version of the package.

### Request Example
```json
{
  "ident": "example-package",
  "__namedParameters": {
    "cache": { /* Cache object */ },
    "project": { /* Project object */ },
    "version": "1.0.0"
  }
}
```

### Response
#### Success Response (200)
- **dist-tags** (Record<string, string>) - Distribution tags for the package.
- **time** (Record<string, string>) - Optional. Timestamps for package versions.
- **versions** (Record<string, { [ key in typeof CACHED_FIELDS[number] ]: any } & { dist: { tarball: string } }>) - Object containing version-specific metadata.

#### Response Example
```json
{
  "dist-tags": {
    "latest": "1.0.0"
  },
  "time": {
    "1.0.0": "2023-01-01T12:00:00Z"
  },
  "versions": {
    "1.0.0": {
      "dist": {
        "tarball": "https://registry.npmjs.org/example-package/-/example-package-1.0.0.tgz"
      }
    }
  }
}
```
```

--------------------------------

### Executing Binaries with Yarn CLI (Shell)

Source: https://yarnpkg.com/advanced/rulebook

Illustrates how to execute binaries managed by Yarn, such as Jest, using the `yarn bin` command. This approach is preferred over hardcoding paths to `node_modules/.bin`. It also shows an alternative using `yarn run --inspect`.

```shell
yarn node --inspect $(yarn bin jest)
```

```shell
yarn run --inspect jest
```

--------------------------------

### Yarn Add with Optional Flag

Source: https://yarnpkg.com/cli/add

Adds a package to 'optionalDependencies' using the '-O' or '--optional' flag. These dependencies are not critical and the installation will not fail if they are missing.

```bash
yarn add <package-name> -O

```

--------------------------------

### Get Base File System - getBaseFs

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Retrieves the base file system object, typed as FakeFS<PortablePath>. This function does not take any parameters.

```typescript
declare function __getBaseFs(): FakeFS<PortablePath>;
```

--------------------------------

### Create Directory - mkdirSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Synchronously creates a directory. Supports options for mode and recursion. Returns the created directory path or undefined.

```typescript
declare function __mkdirSync(p: PortablePath, opts?: Partial<{ mode: number; recursive: boolean }>): undefined | string;
```

--------------------------------

### Package Persistence: shouldPersistResolution

Source: https://yarnpkg.com/api/plugin-git/class/GitResolver

Determines if a package definition for a given locator should be persisted between installs. Typically returns true for cached packages and false for those hydrated directly from the filesystem (e.g., workspaces).

```APIDOC
## GET /websites/yarnpkg/shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. This is generally true for cached packages and false for packages resolved directly from the filesystem, such as those in workspaces. Packages returning false are still stored in the lockfile but will be resolved again on subsequent installs.

### Method
GET

### Endpoint
/websites/yarnpkg/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The package locator being queried.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **result** (boolean) - True if the resolution should be persisted, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Get Publish Access (TypeScript)

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmPublishUtils

Determines the publish access level for a given workspace and identifier. Returns a string representing the access level.

```typescript
declare function __getPublishAccess(workspace: Workspace, ident: Ident): string;
```

--------------------------------

### Get Available Parallelism in Node.js

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/nodeUtils

Retrieves the number of available parallel processing units on the system. This function returns a number representing the parallelism.

```javascript
/**
 * @returns {number}
 */
function __availableParallelism() {}
```

--------------------------------

### Get Severity Inclusions - npmAuditUtils

Source: https://yarnpkg.com/api/plugin-npm-cli/namespace/npmAuditUtils

Determines the set of severities to be included in the audit report. Allows for optional filtering by a specific severity level.

```typescript
declare function __getSeverityInclusions(severity?: Severity): Set<npmAuditTypes.Severity>
```

--------------------------------

### Get File Stats Synchronously

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Synchronously retrieves statistics for a file. Can return either standard Stats or BigIntStats based on the options. Can also return undefined if `throwIfNoEntry` is false.

```APIDOC
## __statSync

### Description
Synchronously retrieves statistics for a file.

### Method
Not Applicable (Synchronous function)

### Endpoint
Not Applicable (Local file system operation)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "p": "/path/to/file"
}
```
Or with options:
```json
{
  "p": "/path/to/file",
  "opts": {
    "bigint": true,
    "throwIfNoEntry": false
  }
}
```

### Response
#### Success Response (Stats | BigIntStats | undefined)
Returns the file statistics. The type of statistics (Stats or BigIntStats) depends on the `bigint` option. Returns `undefined` if `throwIfNoEntry` is `false` and the file does not exist.

#### Response Example
```json
{
  "dev": 2112,
  "ino": 491785,
  "mode": 33188,
  "nlink": 1,
  "uid": 1000,
  "gid": 1000,
  "rdev": 0,
  "size": 1024,
  "blksize": 4096,
  "blocks": 8,
  "atimeMs": 1678886400000.0,
  "mtimeMs": 1678886400000.0,
  "ctimeMs": 1678886400000.0,
  "atime": "2023-03-15T12:00:00.000Z",
  "mtime": "2023-03-15T12:00:00.000Z",
  "ctime": "2023-03-15T12:00:00.000Z"
}
```
```

--------------------------------

### Get Registry Configuration

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Retrieves the configuration for a specific registry. It takes the registry URL and a Configuration object. It returns a MapLike object with the registry details or null if not found.

```typescript
function __getRegistryConfiguration(registry: string, __namedParameters: { configuration: Configuration }): MapLike | null {
  // implementation details
}
```

--------------------------------

### Yarn Info for Package Name Only

Source: https://yarnpkg.com/cli/info

This example demonstrates using the '--name-only' flag with 'yarn info' to print only the names of the matching packages. This is useful when a simple list of package names is required.

```bash
yarn info --name-only
```

--------------------------------

### Get Special Configuration Value in Yarn

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Retrieves a special configuration value by its key. It can accept optional transforms for settings.

```typescript
declare __getSpecial <T = any>(key: string, __namedParameters: Partial<SettingTransforms>): T;

```

--------------------------------

### TypeScript Configuration with defineConfig (CJS)

Source: https://yarnpkg.com/features/constraints

This example demonstrates how to configure `yarn.config.cjs` with TypeScript support using the `defineConfig` function imported from `@yarnpkg/types`. This improves type safety and provides better autocompletion for the `Yarn` object within the constraints function.

```javascript
/** @type {import('@yarnpkg/types')} */
const { defineConfig } = require('@yarnpkg/types');

module.exports = defineConfig({
  async constraints({Yarn}) {
    // `Yarn` is now well-typed ✨
  },
});
```

--------------------------------

### Platform Compatibility (CPU) in package.json

Source: https://yarnpkg.com/configuration/manifest

Specifies the CPU architectures compatible with the package. Yarn compares `process.arch` against this list during installation. Failure to match can lead to skipped postinstall scripts or non-installation if the package is exclusively an optional dependency.

```json
{
  "cpu": [
    "x64",
    "ia32",
    "arm64"
  ]
}
```

--------------------------------

### GET /supportsDescriptor

Source: https://yarnpkg.com/api/plugin-exec/class/ExecResolver

Checks if a given descriptor is intended to be resolved by this specific resolver. If false, other resolver functions (except the locator counterpart) will not be called.

```APIDOC
## GET /supportsDescriptor

### Description
Returns true if the specified descriptor is meant to be turned into a locator by this resolver. If it returns false, other functions (except its locator counterpart) will not be invoked.

### Method
GET

### Endpoint
/supportsDescriptor

### Parameters
#### Query Parameters
- **descriptor** (Descriptor) - Required - The descriptor to validate.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **result** (boolean) - True if the resolver supports the descriptor, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Accessing Dependency Files with require.resolve (JavaScript)

Source: https://yarnpkg.com/advanced/rulebook

Demonstrates how to safely access dependency files, like `package.json`, using `require.resolve` to avoid hardcoding paths. This method ensures compatibility with Yarn's hoisting and various install strategies. It reads the file content into a variable.

```javascript
const fs = require(`fs`);  
const data = fs.readFileSync(require.resolve(`my-dep/package.json`));  
```

--------------------------------

### Traverse Directory Asynchronously - genTraversePromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously traverses a directory starting from an initial path. Returns an AsyncGenerator that yields PortablePath entries. Supports an option for stable sorting. Requires an initial path.

```typescript
declare function __genTraversePromise(init: PortablePath, __namedParameters?: { stableSort?: boolean }): AsyncGenerator<PortablePath, void, unknown>;
```

--------------------------------

### Get Audit Registry Configuration

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Retrieves the audit registry configuration. It requires a Configuration object as input and returns a string representing the audit registry URL.

```typescript
function __getAuditRegistry(__namedParameters: { configuration: Configuration }): string {
  // implementation details
}
```

--------------------------------

### Plugin and Configuration Management

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Utilities for adding and finding plugins, and creating configuration objects.

```APIDOC
## POST /plugins/add

### Description
Adds plugins to the current project context.

### Method
POST

### Endpoint
/plugins/add

### Parameters
#### Request Body
- **cwd** (PortablePath) - Required - The current working directory.
- **pluginMetaList** (Array<PluginMeta>) - Required - A list of plugin metadata to add.

### Request Example
```json
{
  "cwd": "/path/to/project",
  "pluginMetaList": []
}
```

### Response
#### Success Response (200)
- **result** (Promise<void>) - Indicates the plugins have been added.

#### Response Example
```json
{
  "result": null
}
```

## POST /configuration/create

### Description
Creates a new configuration object with default values, ignoring rc files.

### Method
POST

### Endpoint
/configuration/create

### Parameters
#### Request Body
- **startingCwd** (PortablePath) - Required - The starting directory for configuration.
- **plugins** (Map<string, Plugin>) - Optional - A map of plugins to include.

### Request Example
```json
{
  "startingCwd": "/path/to/project",
  "plugins": {}
}
```

### Response
#### Success Response (200)
- **configuration** (Configuration) - The created configuration object.

#### Response Example
```json
{
  "configuration": {}
}
```

## POST /configuration/find

### Description
Finds and instantiates a configuration object based on rc files and environment settings.

### Method
POST

### Endpoint
/configuration/find

### Parameters
#### Request Body
- **startingCwd** (PortablePath) - Required - The starting directory for the search.
- **pluginConfiguration** (PluginConfiguration | null) - Optional - Plugin configuration details.
- **findOptions** (FindProjectOptions) - Optional - Options for finding the project configuration.

### Request Example
```json
{
  "startingCwd": "/path/to/project",
  "pluginConfiguration": null,
  "findOptions": {}
}
```

### Response
#### Success Response (200)
- **configuration** (Configuration) - The found configuration object.

#### Response Example
```json
{
  "configuration": {}
}
```
```

--------------------------------

### Yarn Performance Benchmark Results

Source: https://yarnpkg.com/blog/release/4

Presents the results of a performance benchmark comparing Yarn 3.6.0 and 4.0.0 for installing Gatsby. It shows the mean execution time, standard deviation, and the speed improvement of Yarn 4.0.0 over 3.6.0, indicating a significant performance uplift.

```text
Benchmark 1: 3.6.0  
  Time (mean ± σ):     65.599 s ±  2.214 s    [User: 82.952 s, System: 8.638 s]  
  Range (min … max):   62.167 s … 68.277 s    10 runs  
  
Benchmark 2: 4.0.0  
  Time (mean ± σ):     16.724 s ±  0.928 s    [User: 14.622 s, System: 5.743 s]  
  Range (min … max):   15.318 s … 18.110 s    10 runs  
  
Summary  
  4.0.0 ran 3.92 ± 0.25 times faster than 3.6.0  
```

--------------------------------

### JsZipImpl Methods

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/JsZipImpl

Documentation for the methods used to interact with and manipulate zip archives.

```APIDOC
## JsZipImpl Methods

### `__addDirectory(path: string): number`

#### Description
Adds a directory to the zip archive.

#### Parameters
- **path** (string) - Required - The path of the directory to add.

#### Returns
- `number` - The index of the added directory entry.

### `__deleteEntry(index: number): void`

#### Description
Deletes an entry from the zip archive by its index.

#### Parameters
- **index** (number) - Required - The index of the entry to delete.

#### Returns
- `void`

### `__discard(): void`

#### Description
Discards the current zip archive content without saving.

#### Returns
- `void`

### `__getBufferAndClose(): Buffer<ArrayBufferLike>`

#### Description
Retrieves the zip archive content as a buffer and closes the archive.

#### Returns
- `Buffer<ArrayBufferLike>` - A buffer containing the zip archive data.

### `__getExternalAttributes(index: number): [opsys: number, attributes: number]`

#### Description
Retrieves the external attributes for a specific entry in the zip archive.

#### Parameters
- **index** (number) - Required - The index of the entry.

#### Returns
- `[opsys: number, attributes: number]` - A tuple containing the operating system and attributes.

### `__getFileSource(index: number): { compressionMethod: number; data: Buffer<ArrayBuffer> }`

#### Description
Retrieves the compressed data and compression method for a specific entry.

#### Parameters
- **index** (number) - Required - The index of the entry.

#### Returns
- `{ compressionMethod: number; data: Buffer<ArrayBuffer> }` - An object containing the compression method and data.

### `__getListings(): string[]`

#### Description
Returns a list of all entry names within the zip archive.

#### Returns
- `string[]` - An array of entry names.

### `__getSymlinkCount(): number`

#### Description
Returns the number of symbolic links present in the zip archive.

#### Returns
- `number` - The count of symbolic links.

### `__locate(name: string): number`

#### Description
Locates an entry in the zip archive by its name and returns its index.

#### Parameters
- **name** (string) - Required - The name of the entry to locate.

#### Returns
- `number` - The index of the found entry, or -1 if not found.

### `__setExternalAttributes(index: number, opsys: number, attributes: number): void`

#### Description
Sets the external attributes for a specific entry in the zip archive.

#### Parameters
- **index** (number) - Required - The index of the entry.
- **opsys** (number) - Required - The operating system identifier.
- **attributes** (number) - Required - The attributes to set.

#### Returns
- `void`

### `__setFileSource(target: PortablePath, compression: CompressionData, buffer: Buffer<ArrayBufferLike>): number`

#### Description
Sets the source data for a file entry in the zip archive.

#### Parameters
- **target** (PortablePath) - Required - The path of the target file entry.
- **compression** (CompressionData) - Required - The compression data for the file.
- **buffer** (Buffer<ArrayBufferLike>) - Required - The buffer containing the file data.

#### Returns
- `number` - The index of the created or updated entry.

### `__setMtime(index: number, mtime: number): void`

#### Description
Sets the modification time for a specific entry in the zip archive.

#### Parameters
- **index** (number) - Required - The index of the entry.
- **mtime** (number) - Required - The modification time (timestamp).

#### Returns
- `void`

### `__stat(index: number): Stat`

#### Description
Retrieves statistics for a specific entry in the zip archive.

#### Parameters
- **index** (number) - Required - The index of the entry.

#### Returns
- `Stat` - An object containing statistics about the entry.

### `__readZipSync(fd: number, baseFs: FakeFS<PortablePath>, fileSize: number): Entry[]`

#### Description
Reads a zip archive synchronously from a file descriptor.

#### Parameters
- **fd** (number) - Required - The file descriptor of the zip archive.
- **baseFs** (FakeFS<PortablePath>) - Required - The fake file system instance.
- **fileSize** (number) - Required - The size of the zip file.

#### Returns
- `Entry[]` - An array of entries found in the zip archive.

### Request Example
```json
{
  "path": "/path/to/directory"
}
```

### Response Example
```json
{
  "index": 0
}
```
```

--------------------------------

### Yarnpkg Report Constructor

Source: https://yarnpkg.com/api/yarnpkg-core/class/Report

Demonstrates the instantiation of a new Report object. This is the foundational step for utilizing any reporting functionalities within the Yarnpkg system.

```typescript
new Report(): Report
```

--------------------------------

### shouldPersistResolution API

Source: https://yarnpkg.com/api/plugin-file/class/FileResolver

Determines if a package definition for a given locator should be persisted between installations. This helps manage cache behavior for different package types, like workspaces.

```APIDOC
## GET /websites/yarnpkg/shouldPersistResolution

### Description
This function indicates whether the package definition for the specified locator must be kept between installs. It's typically true for cached packages and false for packages resolved directly from the filesystem (e.g., workspaces).

### Method
GET

### Endpoint
/websites/yarnpkg/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **boolean** - True if the resolution should be persisted, false otherwise.
```

--------------------------------

### Configure Immutable Patterns in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

An array of file patterns that are not allowed to change when `enableImmutableInstalls` is enabled. Ensures the integrity of specified files during installs.

```YAML
immutablePatterns:
  - "**/.pnp.*"
```

--------------------------------

### Get Extract Hint - getExtractHint

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Determines an extraction hint based on provided options. This function is deprecated and has been moved to jsInstallUtils. It returns a boolean value.

```typescript
/** @deprecated: Moved to jsInstallUtils */
declare function __getExtractHint(hints: ExtractHintOptions): boolean;
```

--------------------------------

### mkdirpSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Recursively creates a directory synchronously. Returns undefined or a string.

```APIDOC
## mkdirpSync

### Description
Recursively creates a directory synchronously.

### Method
Not applicable (function signature)

### Endpoint
Not applicable (function signature)

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path of the directory to create.
* **__namedParameters** (object) - Optional - Additional named parameters.
  * **chmod** (number) - Optional - The permission mode to set for the created directory.
  * **utimes** (Array<string | number | Date>) - Optional - The access and modification times to set for the created directory.

### Request Example
```json
{
  "p": "/path/to/directory",
  "__namedParameters": {
    "chmod": 438,
    "utimes": [1678886400000, 1678886400000]
  }
}
```

### Response
#### Success Response (undefined | string)
- **undefined | string**: Returns undefined if successful, or a string representing an error message.

#### Response Example
```json
null
```
```

--------------------------------

### Yarn Info with JSON Output

Source: https://yarnpkg.com/cli/info

This example illustrates how to format the output of the 'yarn info' command as an NDJSON stream using the '--json' flag. This is useful for programmatic processing of package information.

```bash
yarn info --json
```

--------------------------------

### opendirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously opens a directory and returns a directory iterator.

```APIDOC
## __opendirPromise

### Description
Asynchronously opens a directory and returns a directory iterator.

### Method
POST

### Endpoint
`/opendir` (Conceptual endpoint for the operation)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory.

#### Query Parameters
- **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The buffer size for reading directory entries.
  - **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Returns
`Promise<Dir<PortablePath>>` - A promise that resolves with a directory iterator.

```

--------------------------------

### Get Workspace Information - WorkspaceFetcher - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-core/class/WorkspaceFetcher

Retrieves workspace information for a given locator. This method is specific to the WorkspaceFetcher's handling of monorepo structures.

```typescript
__getWorkspace(locator: Locator, opts: FetchOptions): Workspace
```

--------------------------------

### AliasFS Constructor

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/AliasFS

Initializes a new instance of the AliasFS class.

```APIDOC
## new AliasFS<P>(target: P, __namedParameters: AliasFSOptions<P>): AliasFS<P>

### Description
Initializes a new instance of the AliasFS class.

### Parameters
* **target** (P) - The target path for the alias.
* **__namedParameters** (AliasFSOptions<P>) - Options for the AliasFS.
  * **automaticNewlines** (boolean) - Optional. Whether to automatically handle newlines.
  * **mode** (number) - Optional. The mode for file operations.

### Returns
* AliasFS<P> - A new instance of AliasFS.
```

--------------------------------

### Platform Compatibility (libc) in package.json

Source: https://yarnpkg.com/configuration/manifest

Lists the C standard libraries the package depends on. Yarn compares the host's standard library against this list at install time. Mismatches can result in skipped postinstall scripts or non-installation for optional dependencies.

```json
{
  "libc": [
    "glibc",
    "musl"
  ]
}
```

--------------------------------

### Yarn Workspaces Foreach Run Build Script in Parallel

Source: https://yarnpkg.com/cli/workspaces/foreach

Demonstrates running the 'build' script in parallel across current and descendant packages. '-Apt' flags enable all workspaces, parallel execution, and topological ordering respectively.

```bash
yarn workspaces foreach -Apt run build
```

--------------------------------

### Get Yarn Configuration Limit

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Retrieves a specific limit configuration for a given key. The key must be of a type that is a filter of `ConfigurationValueMap` to numbers.

```typescript
declare __getLimit <K>(key: K): Limit;

```

--------------------------------

### opendirSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Synchronously opens a directory and returns a directory iterator.

```APIDOC
## opendirSync

### Description
Synchronously opens a directory and returns a directory iterator (`Dir<PortablePath>`) which can be used to iterate over the directory's entries.

### Method
`opendirSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory to open.
#### Optional Parameters
- **opts** (Object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The size of the buffer to use for reading directory entries.
  - **recursive** (boolean) - Optional - Whether to recursively open subdirectories.

### Returns
`Dir<PortablePath>` - The directory iterator.
```

--------------------------------

### shouldPersistResolution

Source: https://yarnpkg.com/api/yarnpkg-core/class/WorkspaceResolver

Determines if a package definition for a given locator should be persisted between installs. Generally true for cached packages and false for those hydrated directly from the filesystem (like workspaces).

```APIDOC
## GET /shouldPersistResolution

### Description
Indicates whether the package definition for the specified locator must be kept between installs. Typically returns true for cached packages and false for packages hydrated directly from the filesystem.

### Method
GET

### Endpoint
/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The queried package.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **result** (boolean) - True if the resolution should be persisted, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### ZipFS Constructors

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D/class/ZipFS

Details on how to create new instances of the ZipFS class, either from a path or directly from buffer data.

```APIDOC
## Constructors

### `__constructor`

*   `new ZipFS(): ZipFS`
*   `new ZipFS(p: PortablePath, opts?: ZipPathOptions): ZipFS`
*   `new ZipFS(data: null | Buffer<ArrayBufferLike>, opts?: ZipBufferOptions): ZipFS`

#### Returns
`ZipFS`
```

--------------------------------

### Get Publish Registry Configuration

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Determines the appropriate registry for publishing a package based on its manifest and the current configuration. It requires a Manifest object and a Configuration object, returning the publish registry URL as a string.

```typescript
function __getPublishRegistry(manifest: Manifest, __namedParameters: { configuration: Configuration }): string {
  // implementation details
}
```

--------------------------------

### TypeScript Compatibility Fixes (Shell)

Source: https://yarnpkg.com/advanced/changelog

Addresses issues where TypeScript versions could not be installed due to patch conflicts. This highlights specific version fixes and future improvements for tolerance.

```shell
# TypeScript 4.2 compatibility fix
# Future Yarn releases (3.0+) will be more tolerant of patch conflicts.
```

```shell
# Patches for TypeScript <4.2 are now included.
```

--------------------------------

### Explain Peer Dependencies with Yarn

Source: https://yarnpkg.com/advanced/error-codes

Provides a command to get detailed explanations for peer dependency issues. It requires passing the 'p'-prefixed code from the original peer resolution error message.

```bash
yarn explain peer-requirements <p-prefixed-code>
```

--------------------------------

### Add Dependencies with Yarn

Source: https://context7.com/context7/yarnpkg/llms.txt

Adds new packages to your project's dependencies. Supports various version specifiers, dependency types (dev, peer, optional), and sources (npm, GitHub, local files). Includes interactive and cached installation options.

```bash
# Add a regular dependency to current workspace
yarn add lodash

# Add a specific version
yarn add lodash@4.17.21

# Add as dev dependency
yarn add --dev typescript

# Add from GitHub repository (master branch)
yarn add lodash@github:lodash/lodash

# Add from specific branch
yarn add lodash-es@lodash/lodash#es

# Add local package (tarball)
yarn add local-pkg@file:../path/to/package.tgz

# Add with exact version (no semver modifier)
yarn add react@18.2.0 --exact

# Add with tilde modifier
yarn add express@4.18.0 --tilde

# Add as peer dependency
yarn add react --peer

# Add as optional dependency
yarn add fsevents --optional

# Interactive mode - reuse versions from other workspaces
yarn add lodash --interactive

# Use highest cached version in project
yarn add lodash --cached

# Add to all workspaces
yarn add typescript --dev
```

--------------------------------

### mkdirpPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Asynchronously creates a directory, including any necessary parent directories. This is an abstract method.

```APIDOC
## mkdirpPromise

### Description
Asynchronously creates a directory, including any necessary parent directories. This is an abstract method.

### Method
Promise<string | undefined>

### Endpoint
N/A (Abstract method)

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "example": "Not applicable"
}
```

### Response
#### Success Response (Promise<string | undefined>)
- **Type**: Promise<string | undefined>
- **Description**: A promise that resolves with the path of the created directory, or undefined.

#### Response Example
```json
{
  "example": "Not applicable"
}
```
```

--------------------------------

### Yarn Dedupe Usage Example

Source: https://yarnpkg.com/cli/dedupe

Demonstrates the basic command-line usage for 'yarn dedupe'. This command is used to deduplicate dependencies with overlapping ranges within a Yarn project.

```bash
$ yarn dedupe ...
```

--------------------------------

### Basic Yarn Link Usage

Source: https://yarnpkg.com/cli/link

This demonstrates the basic command structure for linking local projects using yarn. It typically involves the 'yarn link' command followed by the path to the project to be linked.

```bash
yarn link ...
```

--------------------------------

### Constructor: __new TarballFileFetcher()

Source: https://yarnpkg.com/api/plugin-file/class/TarballFileFetcher

Initializes a new instance of the TarballFileFetcher. This constructor does not take any arguments and returns a TarballFileFetcher object.

```typescript
new TarballFileFetcher(): TarballFileFetcher
```

--------------------------------

### mkdirSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Synchronously creates a directory. This is an abstract method.

```APIDOC
## mkdirSync

### Description
Synchronously creates a directory. This is an abstract method.

### Method
string | undefined

### Endpoint
N/A (Abstract method)

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "example": "Not applicable"
}
```

### Response
#### Success Response (string | undefined)
- **Type**: string | undefined
- **Description**: The path of the created directory, or undefined.

#### Response Example
```json
{
  "example": "Not applicable"
}
```
```

--------------------------------

### PosixFS Constructors

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/PosixFS

Provides information about the constructors available for the PosixFS class.

```APIDOC
## Constructors

### `__constructor`

Initializes a new instance of the PosixFS class.

**Parameters:**
* `baseFs` (FakeFS<PortablePath>): The base file system to proxy.

**Returns:**
* `PosixFS`: A new instance of PosixFS.
```

--------------------------------

### GET /getSatisfying

Source: https://yarnpkg.com/api/plugin-exec/class/ExecResolver

Finds locators that potentially satisfy a given descriptor. This function statically computes which known references satisfy the descriptor without network access.

```APIDOC
## GET /getSatisfying

### Description
Given a descriptor and a list of locators, this function determines which of the locators potentially satisfy the descriptor. It differs from `getCandidates` by statically computing the satisfying locators without network interaction.

### Method
GET

### Endpoint
/getSatisfying

### Parameters
#### Query Parameters
- **descriptor** (Descriptor) - Required - The target descriptor.
- **dependencies** (Record<string, Package>) - Required - The resolution dependencies and their resolutions.
- **locators** (Locator[]) - Required - The candidate locators.
- **opts** (ResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **locators** (Locator[]) - A list of locators that satisfy the descriptor, sorted by preference.
- **sorted** (boolean) - Indicates if the returned locators are sorted.

#### Response Example
```json
{
  "locators": [
    {
      "name": "example-package",
      "range": "^1.0.0",
      "protocol": "",
      "scope": null,
      "source": "/path/to/package",
      "selector": null,
      "reference": "1.2.3"
    }
  ],
  "sorted": true
}
```
```

--------------------------------

### Get Task Pool for Configuration

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/tgzUtils

Obtains a task pool based on the provided configuration. If no configuration is given, it may return a default pool. This function returns a ZipWorkerPool.

```typescript
declare function getTaskPoolForConfiguration(configuration: void | Configuration): ZipWorkerPool;
```

--------------------------------

### Core Functions

Source: https://yarnpkg.com/api/yarnpkg-cli

Provides access to core CLI functionalities, dynamic library loading, plugin configuration, workspace management, and command execution.

```APIDOC
## GET /cli/getCli

### Description
Retrieves the Yarn CLI instance, optionally with a specified working directory and plugin configuration.

### Method
GET

### Endpoint
/cli/getCli

### Parameters
#### Query Parameters
- **cwd** (PortablePath) - Optional - The working directory for the CLI.
- **pluginConfiguration** (PluginConfiguration) - Optional - The configuration for plugins.

### Response
#### Success Response (200)
- **cliInstance** (Cli<CommandContext>) - The Yarn CLI instance.
- **defaultContext** (object) - The default context for the CLI, including cwd, plugins, quiet status, and I/O streams.

#### Response Example
```json
{
  "cliInstance": { ... },
  "defaultContext": {
    "cwd": "/path/to/project",
    "plugins": { ... },
    "quiet": false,
    "stderr": "<WriteStream>",
    "stdin": "<ReadStream>",
    "stdout": "<WriteStream>"
  }
}
```

## GET /cli/getDynamicLibs

### Description
Loads and returns all dynamic libraries available to the Yarn CLI.

### Method
GET

### Endpoint
/cli/getDynamicLibs

### Response
#### Success Response (200)
- **dynamicLibs** (Map<string, any>) - A map of dynamic library names to their loaded modules.

#### Response Example
```json
{
  "dynamicLibs": {
    "plugin-a": { ... },
    "plugin-b": { ... }
  }
}
```

## GET /cli/getPluginConfiguration

### Description
Retrieves the current plugin configuration for the Yarn CLI.

### Method
GET

### Endpoint
/cli/getPluginConfiguration

### Response
#### Success Response (200)
- **pluginConfiguration** (PluginConfiguration) - The plugin configuration object.

#### Response Example
```json
{
  "pluginConfiguration": {
    "enabled": ["core", "typescript"],
    "plugins": { ... }
  }
}
```

## POST /cli/openWorkspace

### Description
Opens a workspace within the Yarn project.

### Method
POST

### Endpoint
/cli/openWorkspace

### Parameters
#### Request Body
- **configuration** (Configuration) - Required - The project configuration.
- **cwd** (PortablePath) - Required - The current working directory.

### Response
#### Success Response (200)
- **workspace** (Workspace) - The opened workspace object.

#### Response Example
```json
{
  "workspace": {
    "cwd": "/path/to/workspace",
    "name": "my-package",
    "pkg": { ... }
  }
}
```

## POST /cli/runExit

### Description
Executes a CLI command and handles its exit.

### Method
POST

### Endpoint
/cli/runExit

### Parameters
#### Request Body
- **argv** (string[]) - Required - The command arguments.
- **cwd** (PortablePath) - Required - The current working directory.
- **pluginConfiguration** (PluginConfiguration) - Required - The plugin configuration.
- **selfPath** (null | PortablePath) - Optional - The path to the CLI executable.

### Response
#### Success Response (200)
- **status** (void) - Indicates successful execution.

#### Response Example
```json
{
  "status": "success"
}
```
```

--------------------------------

### Get Auth Configuration

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Retrieves the authentication configuration for a given registry. It takes the registry URL and an optional Ident, along with a Configuration object. It returns a MapLike object representing the auth configuration.

```typescript
function __getAuthConfiguration(registry: string, __namedParameters: { configuration: Configuration; ident?: Ident }): MapLike {
  // implementation details
}
```

--------------------------------

### Directory Open Operations

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/PortableNodeModulesFS

Provides asynchronous and synchronous methods for opening directories.

```APIDOC
## POST /fs/opendirPromise

### Description
Asynchronously opens a directory and returns a directory handle.

### Method
POST

### Endpoint
/fs/opendirPromise

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the directory.
- **opts** (object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The buffer size for reading directory entries.
  - **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Request Example
```json
{
  "p": "/path/to/directory",
  "opts": {
    "recursive": true
  }
}
```

### Response
#### Success Response (200)
- **dirHandle** (Dir<PortablePath>) - A handle to the opened directory.

#### Response Example
```json
{
  "dirHandle": { /* ... directory handle object ... */ }
}
```

---

## POST /fs/opendirSync

### Description
Synchronously opens a directory and returns a directory handle.

### Method
POST

### Endpoint
/fs/opendirSync

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the directory.
- **opts** (object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The buffer size for reading directory entries.
  - **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Request Example
```json
{
  "p": "/path/to/directory",
  "opts": {
    "recursive": true
  }
}
```

### Response
#### Success Response (200)
- **dirHandle** (Dir<PortablePath>) - A handle to the opened directory.

#### Response Example
```json
{
  "dirHandle": { /* ... directory handle object ... */ }
}
```
```

--------------------------------

### Yarn Unplug Examples: Unplug Recursively

Source: https://yarnpkg.com/cli/unplug

Illustrates the '-R' or '--recursive' flag, which unplugs a package and its transitive dependencies. This is helpful for debugging issues that might stem from nested package structures.

```bash
yarn unplug lodash -R
```

--------------------------------

### CustomDir Constructor

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CustomDir

Initializes a new instance of the CustomDir class.

```APIDOC
## new CustomDir<P>(path: P, nextDirent: () => null | DirentNoPath, opts?: CustomDirOptions): CustomDir<P>

### Description
Initializes a new instance of the CustomDir class.

### Method
CONSTRUCTOR

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
  "path": "/path/to/directory",
  "nextDirent": "() => null | DirentNoPath",
  "opts": {}
}
```

### Response
#### Success Response (200)
N/A (Constructor)

#### Response Example
N/A (Constructor)
```

--------------------------------

### Configure Package Hoisting Limits

Source: https://yarnpkg.com/migration/guide

Replaces the `nohoist` configuration with `nmHoistingLimits` in `.yarnrc.yml` for managing package hoisting. This is recommended for projects that previously used `nohoist`, particularly with workspaces.

```yaml
nmHoistingLimits: workspaces
```

--------------------------------

### Yarn CLI: Get Binary Path

Source: https://yarnpkg.com/cli/bin

This command-line interface usage demonstrates how to retrieve the path to a binary script managed by Yarn. It can be used to list all available binaries or fetch the path for a specific one.

```bash
yarn bin [name]
```

```bash
yarn bin
```

```bash
yarn bin eslint
```

--------------------------------

### Yarn Version Command Usage

Source: https://yarnpkg.com/cli/version

This snippet shows the basic usage of the 'yarn version' command, indicating that a strategy needs to be provided.

```bash
$ yarn version <strategy>
```

--------------------------------

### Run yarn explain peer-requirements with a hash

Source: https://yarnpkg.com/cli/explain/peer-requirements

This command explains a specific peer requirement identified by a given hash. It's useful for understanding the status of a particular peer dependency.

```bash
yarn explain peer-requirements p1a4ed
```

--------------------------------

### Yarn Add with Skip Build Mode

Source: https://yarnpkg.com/cli/add

Uses the '--mode=skip-build' option to add packages without executing their build scripts. This is useful for faster installations when build artifacts are not immediately needed.

```bash
yarn add <package-name> --mode=skip-build

```

--------------------------------

### GET /getSatisfying

Source: https://yarnpkg.com/api/yarnpkg-core/class/LegacyMigrationResolver

Finds which of the provided locators potentially satisfy a given descriptor. This function statically computes which known references potentially satisfy the target descriptor without network calls.

```APIDOC
## GET /getSatisfying

### Description
Given a descriptor and a list of locators, this function determines which of the locators potentially satisfy the descriptor. It differs from `getCandidates` as it statically computes potential satisfiers without network resolution.

### Method
GET

### Endpoint
/getSatisfying

### Parameters
#### Query Parameters
- **descriptor** (Descriptor) - Required - The target descriptor.
- **dependencies** (Record<string, Package>) - Required - The resolution dependencies and their resolutions.
- **locators** (Locator[]) - Required - The candidate locators.
- **opts** (ResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **locators** (Locator[]) - A list of locators that satisfy the descriptor, sorted by preference.
- **sorted** (boolean) - Indicates if the returned locators are sorted.

#### Response Example
```json
{
  "locators": [
    {
      "name": "example-package",
      "range": "1.0.0",
      "protocol": "",
      "source": "/path/to/package",
      "}:{hash": "sha1:abcdef123456"
    }
  ],
  "sorted": true
}
```
```

--------------------------------

### Get Extract Hint (TypeScript)

Source: https://yarnpkg.com/api/plugin-pnp/namespace/jsInstallUtils

Determines if an extract hint is available based on FetchResult. This utility function is useful for optimizing dependency extraction processes. It returns a boolean.

```TypeScript
declare function __getExtractHint(fetchResult: FetchResult): boolean;
```

--------------------------------

### Get Local Package Path - WorkspaceFetcher - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-core/class/WorkspaceFetcher

Retrieves the local filesystem path for a specified package locator. This path is used for resolving relative dependency sources, such as 'file:./foo'.

```typescript
__getLocalPath(locator: Locator, opts: FetchOptions): PortablePath
```

--------------------------------

### Yarnpkg PatchResolver Get Resolution Dependencies

Source: https://yarnpkg.com/api/plugin-patch/class/PatchResolver

Determines and returns a set of descriptors that need to be resolved before the target descriptor can be resolved. This is particularly useful for transform packages.

```typescript
__getResolutionDependencies(descriptor: Descriptor, opts: MinimalResolveOptions): { sourceDescriptor: Descriptor }
```

--------------------------------

### Get Default Task Pool

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/tgzUtils

Retrieves the default task pool for zip operations. This function returns a ZipWorkerPool instance, which can be used to manage concurrent zip-related tasks.

```typescript
declare function getDefaultTaskPool(): ZipWorkerPool;
```

--------------------------------

### Yarn Supported Architectures Configuration

Source: https://yarnpkg.com/configuration/yarnrc

Specifies the system architectures for which Yarn should install packages. This includes lists for operating systems (`os`), CPU architectures (`cpu`), and C standard libraries (`libc`). Each list can include specific values or use 'current' to refer to the host system's characteristics.

```javascript
supportedArchitectures: {
  os: [
    "current",
    "darwin",
    "linux",
    "win32",
  ],
  cpu: [
    "current",
    "x64",
    "ia32",
    "arm64",
  ],
  libc: [
    "current",
    "glibc",
    "musl",
  ],
}
```

--------------------------------

### CustomDir Constructor - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CustomDir

Defines the constructor for the CustomDir class, accepting a path, a function to get the next directory entry, and optional options. It initializes a new CustomDir instance with a generic path type P.

```typescript
new CustomDir<P>(path: P, nextDirent: () => null | DirentNoPath, opts?: CustomDirOptions): CustomDir<P>
```

--------------------------------

### Get Default Registry Configuration

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Retrieves the default registry configuration, which can be for fetching or publishing. It accepts a Configuration object and an optional RegistryType. It returns a string representing the default registry URL.

```typescript
function __getDefaultRegistry(__namedParameters: { configuration: Configuration; type?: RegistryType }): string {
  // implementation details
}
```

--------------------------------

### Run Node Script with Yarn

Source: https://yarnpkg.com/cli/node

Execute a Node.js script using the 'yarn node' command. This ensures the script runs within the project's environment, including proper setup for PnP and consistent Node.js versioning.

```bash
$ yarn node ...
```

```bash
yarn node ./my-script.js
```

--------------------------------

### Build CLI and Run Integration Tests with Yarn

Source: https://yarnpkg.com/advanced/contributing

This sequence of commands first builds the Yarn CLI and then runs the integration test suite. Integration tests simulate user experiences to ensure the application functions correctly as a whole. The CLI must be pre-built to avoid esbuild overhead during test execution.

```bash
yarn build:cli
yarn test:integration
```

--------------------------------

### Get Dynamic Libraries - @yarnpkg/cli

Source: https://yarnpkg.com/api/yarnpkg-cli

Loads and returns dynamic libraries used by the Yarn CLI. This function discovers and aggregates libraries that can be loaded at runtime, typically for extending CLI functionality.

```typescript
function __getDynamicLibs(): Map<string, any>
```

--------------------------------

### Get Report Tree - npmAuditUtils

Source: https://yarnpkg.com/api/plugin-npm-cli/namespace/npmAuditUtils

Generates a tree node representing the audit report from the provided extended audit response. This is useful for visualizing or processing audit results hierarchically.

```typescript
declare function __getReportTree(result: AuditExtendedResponse): TreeNode
```

--------------------------------

### Gitignore for Yarn Projects without Zero-Installs

Source: https://yarnpkg.com/getting-started/qa

This gitignore configuration is for Yarn projects that do not use Zero-Installs. It includes standard Yarn artifacts like .pnp files, along with exceptions for necessary patch and plugin directories.

```gitignore
.pnp.*
.yarn/*
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions

```

--------------------------------

### Get System Architecture Set in Node.js

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/nodeUtils

Retrieves a set of compatible architecture details, including arrays of possible CPU, libc, and OS values. This function returns an object conforming to the ArchitectureSet type.

```javascript
/**
 * @returns {ArchitectureSet}
 */
function __getArchitectureSet() {}
```

--------------------------------

### Run Build Script on Matching Workspaces with Yarn

Source: https://yarnpkg.com/features/workspaces

This command runs the `build` script on the current workspace and all dependent workspaces that match a specific pattern. The `--from .` flag selects workspaces starting from the current directory, and `-R` likely indicates a recursive or dependency-aware execution.

```bash
yarn workspaces foreach --from . -R run build
```

--------------------------------

### Yarnpkg Report Error Handling

Source: https://yarnpkg.com/api/yarnpkg-core/class/Report

Shows methods for reporting errors, including one-time error reporting with optional extra reporting callbacks. These are essential for diagnosing and communicating issues during package installation or build processes.

```typescript
__reportError(name: MessageName, text: string): void
```

```typescript
__reportErrorOnce(name: MessageName, text: string, opts?: { key?: any; reportExtra?: (report: Report) => void }): void
```

```typescript
__reportExceptionOnce(error: Error | ReportError): void
```

--------------------------------

### Get File Stats Synchronously

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Synchronously retrieves statistics for a file specified by its file descriptor. It can return either `Stats` or `BigIntStats` based on the `bigint` option. Returns `Stats` or `BigIntStats`.

```typescript
sync __fstatSync(fd: number): Stats
sync __fstatSync(fd: number, opts: { bigint: true }): BigIntStats
sync __fstatSync(fd: number, opts?: { bigint?: boolean }): Stats | BigIntStats
```

--------------------------------

### Yarn DLX Advanced Usage: Multiple Packages and Execution

Source: https://yarnpkg.com/cli/dlx

This snippet showcases advanced 'yarn dlx' usage, including installing multiple packages and executing a specific script with custom flags. It demonstrates how to use the '-p' flag to specify additional packages ('typescript', 'ts-node') required for the command, and then executes 'ts-node' with specific options.

```bash
yarn dlx -p typescript -p ts-node ts-node --transpile-only -e "console.log('hello!')"
```

--------------------------------

### statSync - Get File Stats Synchronously

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Synchronously retrieves statistics for a file. Can return either standard stats or big-endian stats, and can optionally throw an error if the entry does not exist.

```APIDOC
## POST /fs/statSync

### Description
Synchronously retrieves statistics for a file.

### Method
POST

### Endpoint
/fs/statSync

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **opts** (object) - Optional - Options for retrieving stats.
  - **bigint** (boolean) - If true, returns big-endian stats. Defaults to false.
  - **throwIfNoEntry** (boolean) - If true, throws an error if the entry does not exist. Defaults to true.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "bigint": true,
    "throwIfNoEntry": false
  }
}
```

### Response
#### Success Response (200)
- **stats** (Stats | BigIntStats | undefined) - File statistics or undefined if `throwIfNoEntry` is false and the entry does not exist.
```

--------------------------------

### Get Scope Configuration

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Retrieves the configuration for a specific npm scope. It accepts a scope (or null) and a Configuration object. It returns a MapLike object with the scope configuration or null if not found.

```typescript
function __getScopeConfiguration(scope: null | string, __namedParameters: { configuration: Configuration }): MapLike | null {
  // implementation details
}
```

--------------------------------

### Get Resolution Dependencies for Descriptor

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Resolver

Returns a set of descriptors that need to be resolved before the main descriptor can be resolved. This is typically used for transform packages where the original resolution context is important.

```typescript
declare function __getResolutionDependencies(descriptor: Descriptor, opts: MinimalResolveOptions): Record<string, Descriptor>
```

--------------------------------

### Use workspace: Protocol for Cross-References

Source: https://yarnpkg.com/features/workspaces

This example demonstrates how to use the special 'workspace:' protocol in a package.json to establish cross-references between packages within a Yarn workspace project. It allows a package to depend on another workspace package by name, simplifying inter-package dependency management.

```json
{
  "dependencies": {
    "@my-org/utils": "workspace:^"
  }
}
```

--------------------------------

### Get Real Path with Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/LazyFS

The getRealPath function resolves and returns the real path of a given file system entry. It does not take any parameters and returns the path of type P.

```typescript
__getRealPath(): P
```

--------------------------------

### CustomDir Methods

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CustomDir

Documentation for the asynchronous and synchronous methods of the CustomDir class.

```APIDOC
## CustomDir Methods

### `__[asyncIterator]()`

#### Description
Provides an asynchronous iterator for the directory entries.

#### Method
`ASYNC_ITERATOR`

#### Endpoint
N/A

#### Returns
`AsyncGenerator<DirentNoPath, void, unknown>`

### `__close()`

#### Description
Closes the directory stream asynchronously or accepts a callback for synchronous closure.

#### Method
`PROMISE` or `CALLBACK`

#### Endpoint
N/A

#### Parameters
- `cb` (NoParamCallback) - Optional callback function for synchronous closure.

#### Returns
`Promise<void>`

### `__closeSync()`

#### Description
Closes the directory stream synchronously.

#### Method
`SYNC`

#### Endpoint
N/A

#### Returns
`void`

### `__read()`

#### Description
Reads the next directory entry asynchronously or accepts a callback.

#### Method
`PROMISE` or `CALLBACK`

#### Endpoint
N/A

#### Parameters
- `cb` (function) - Optional callback function with parameters `(err: null | ErrnoException, dirent: null | DirentNoPath)`.

#### Returns
`Promise<DirentNoPath>`

### `__readSync()`

#### Description
Reads the next directory entry synchronously.

#### Method
`SYNC`

#### Endpoint
N/A

#### Returns
`null | DirentNoPath`

### `__throwIfClosed()`

#### Description
Throws an error if the directory stream is already closed.

#### Method
`SYNC`

#### Endpoint
N/A

#### Returns
`void`
```

--------------------------------

### Yarn Add with Cached Option

Source: https://yarnpkg.com/cli/add

Utilizes the '--cached' option to prioritize using the highest version of a package already present in the project, potentially speeding up installations.

```bash
yarn add <package-name> --cached

```

--------------------------------

### Get Extract Hint with Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/LazyFS

The getExtractHint function determines if an extraction hint is available. This function is deprecated and has been moved to jsInstallUtils. It takes ExtractHintOptions as input and returns a boolean value.

```typescript
__getExtractHint(hints: ExtractHintOptions): boolean
```

--------------------------------

### Get ESM Loader Template - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-pnp

Retrieves a template string for an ECMAScript Module (ESM) loader. This function is used to obtain the base structure for ESM-compatible PnP loaders.

```typescript
declare function getESMLoaderTemplate(): string;
```

--------------------------------

### mkdirpPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Recursively creates a directory. Returns a Promise that resolves with undefined or a string.

```APIDOC
## mkdirpPromise

### Description
Recursively creates a directory.

### Method
Not applicable (function signature)

### Endpoint
Not applicable (function signature)

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path of the directory to create.
* **__namedParameters** (object) - Optional - Additional named parameters.
  * **chmod** (number) - Optional - The permission mode to set for the created directory.
  * **utimes** (Array<string | number | Date>) - Optional - The access and modification times to set for the created directory.

### Request Example
```json
{
  "p": "/path/to/directory",
  "__namedParameters": {
    "chmod": 438,
    "utimes": [1678886400000, 1678886400000]
  }
}
```

### Response
#### Success Response (Promise<undefined | string>)
- **undefined | string**: Resolves with undefined if successful, or a string representing an error message.

#### Response Example
```json
null
```
```

--------------------------------

### Yarn Add with Update Lockfile Mode

Source: https://yarnpkg.com/cli/add

Employs the '--mode=update-lockfile' option to update the lockfile without performing a full install. This is beneficial for automated dependency updating tools.

```bash
yarn add <package-name> --mode=update-lockfile

```

--------------------------------

### shouldPersistResolution API

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Resolver

Determines if the package definition for a given locator should be persisted between installs. Typically returns true for cached packages and false for those hydrated directly from the filesystem (e.g., workspaces).

```APIDOC
## GET /shouldPersistResolution

### Description
Indicates whether the package definition for a specified locator should be persisted between installs. This is generally true for cached packages and false for packages resolved directly from the filesystem, like those in workspaces. Packages returning false are still stored in the lockfile but will be re-resolved in subsequent installs.

### Method
GET

### Endpoint
/shouldPersistResolution

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The package locator being queried.
- **opts** (MinimalResolveOptions) - Required - The resolution options.

### Response
#### Success Response (200)
- **persist** (boolean) - True if the resolution should be persisted, false otherwise.

#### Response Example
```json
{
  "persist": true
}
```
```

--------------------------------

### Get Subprocess Streams for Logging in Yarn

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Configures and returns writable streams for stdout and stderr for subprocess logging. Requires a log file path and specific naming parameters.

```typescript
declare __getSubprocessStreams(logFile: PortablePath, __namedParameters: { header?: string; prefix: string; report: Report }): { stderr: Writable; stdout: Writable };

```

--------------------------------

### openPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Asynchronously opens a file and returns a file descriptor.

```APIDOC
## openPromise

### Description
Asynchronously opens a file given a path and flags, returning a file descriptor.

### Method
POST

### Endpoint
/websites/yarnpkg/openPromise

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **flags** (string) - Required - The flags to use when opening the file (e.g., 'r', 'w', 'a').
- **mode** (number) - Optional - The file mode to use if the file is created.

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (200)
- **result** (number) - The file descriptor.

#### Response Example
```json
{
  "result": 3
}
```
```

--------------------------------

### Yarn PnP Package Location Path

Source: https://yarnpkg.com/advanced/pnp-spec

Specifies the location of a package on disk, relative to the PnP manifest. Paths must start with `./` or `../` and end with a trailing `/`.

```javascript
packageLocation: "./.yarn/cache/react-npm-18.0.0-a0b1c2d3.zip"
```

--------------------------------

### GitFetcher Constructor - Yarnpkg

Source: https://yarnpkg.com/api/plugin-git/class/GitFetcher

Initializes a new GitFetcher instance. This constructor is part of the GitFetcher class, responsible for managing the fetching of package data.

```typescript
new GitFetcher(): GitFetcher
```

--------------------------------

### mkdirPromise API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NoFS

Asynchronously creates a directory. The current implementation returns `Promise<never>`.

```APIDOC
## mkdirPromise API

### Description
Asynchronously creates a directory. Currently returns `Promise<never>`.

### Method
`Promise<never>`
```

--------------------------------

### Yarn Command - Skip Build Mode

Source: https://yarnpkg.com/cli/up

Utilizes the '--mode skip-build' option to upgrade dependencies without running their associated build scripts. This can speed up installations when build steps are not critical.

```bash
yarn up --mode skip-build
```

--------------------------------

### Access Filesystem with fslib - JavaScript

Source: https://yarnpkg.com/advanced/pnpapi

Demonstrates how to use the `@yarnpkg/fslib` library to access files, including those within zip archives. It sets up virtual file systems for cross-platform compatibility and reading zip contents.

```javascript
const {PosixFS, ZipOpenFS} = require(`@yarnpkg/fslib`);  
const libzip = require(`@yarnpkg/libzip`).getLibzipSync();  

// This will transparently open zip archives  
const zipOpenFs = new ZipOpenFS({libzip});  

// This will convert all paths into a Posix variant, required for cross-platform compatibility  
const crossFs = new PosixFS(zipOpenFs);  

console.log(crossFs.readFileSync(`C:\\path\\to\\archive.zip\\package.json`));  

```

--------------------------------

### Add Package from JSR Registry using Yarn

Source: https://yarnpkg.com/protocol/jsr

This command uses Yarn to add a package from the JSR registry. The `jsr:` protocol specifies the registry, and the version is appended after the colon. This is useful for installing packages that are distributed via JSR.

```bash
yarn add @luca/flag@jsr:2.0.0
```

--------------------------------

### Code Formatting Example: Long Function Call

Source: https://yarnpkg.com/package_name=prettier&version=3.6

Demonstrates how Prettier formats a long function call by wrapping arguments to adhere to a maximum line length. This showcases Prettier's ability to automatically reformat code for better readability.

```javascript
### Input
```
foo(reallyLongArg(), omgSoManyParameters(), IShouldRefactorThis(), isThereSeriouslyAnotherOne());

```

### Output
```
foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne(),
);

```
```

--------------------------------

### Get File Stats - lstatPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously retrieves statistics about a file (not following symbolic links). Supports returning either Stats or BigIntStats based on the provided options. Requires a PortablePath as input.

```typescript
declare function __lstatPromise(p: PortablePath): Promise<Stats>;
declare function __lstatPromise(p: PortablePath, opts: undefined | (StatOptions & { bigint?: false })): Promise<Stats>;
declare function __lstatPromise(p: PortablePath, opts: StatOptions & { bigint: true }): Promise<BigIntStats>;
```

--------------------------------

### Get Scope Registry

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmConfigUtils

Determines the registry URL associated with a specific npm scope. It takes the scope (or null) and an optional RegistryType, along with a Configuration object. It returns the registry URL as a string.

```typescript
function __getScopeRegistry(scope: null | string, __namedParameters: { configuration: Configuration; type?: RegistryType }): string {
  // implementation details
}
```

--------------------------------

### __fetch Method

Source: https://yarnpkg.com/api/plugin-exec/class/ExecFetcher

Fetches package data for a given locator.

```APIDOC
## Method __fetch

### Description
Fetches package data for a given locator. This function must return an object describing where the package manager can find the data for the specified package on disk.

### Method
POST

### Endpoint
/fetch

### Parameters
#### Request Body
- **locator** (Locator) - Required - The source locator.
- **opts** (FetchOptions) - Required - The fetch options.

### Request Example
```json
{
  "locator": {
    "type": "npm",
    "name": "my-package",
    "range": ">=1.0.0"
  },
  "opts": {
    "registry": "https://registry.npmjs.org/"
  }
}
```

### Response
#### Success Response (200)
- **checksum** (string | null) - The checksum of the fetched package.
- **localPath** (PortablePath | null) - The local path to the package data.
- **packageFs** (FakeFS<PortablePath>) - A filesystem object representing the package contents.
- **prefixPath** (PortablePath) - The prefix path for the package.
- **releaseFs** (function) - A function to release the filesystem resources.

#### Response Example
```json
{
  "checksum": "sha512-examplechecksum",
  "localPath": "/tmp/fetch/my-package-1.0.0",
  "packageFs": { ... },
  "prefixPath": "/tmp/fetch/my-package-1.0.0",
  "releaseFs": "<function>"
}
```
```

--------------------------------

### Get Resolution Dependencies - Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-core/class/LockfileResolver

Determines and returns a set of descriptors that must be resolved before the primary descriptor can be transformed into a locator. This is crucial for transform packages where the original resolution needs to be preserved.

```typescript
__getResolutionDependencies(descriptor: Descriptor, opts: MinimalResolveOptions): Record<string, Descriptor>
```

--------------------------------

### Yarn Error Code: YN0004 - DISABLED_BUILD_SCRIPTS

Source: https://yarnpkg.com/advanced/error-codes

YN0004 indicates that a package contains build scripts, but these scripts have been globally disabled for the project. A warning is issued to ensure the installation is complete.

```text
YN0004 - `DISABLED_BUILD_SCRIPTS`​
A package has build scripts, but they've been disabled across the project.
Build scripts can be disabled on a global basis through the use of the `enableScripts` settings. When it happens, a warning is still emitted to let you know that the installation might not be complete.
The safest way to downgrade the warning into a notification is to explicitly disable build scripts for the affected packages through the use of the `dependenciesMeta[].built` key.
```

--------------------------------

### Package Manifest: Update Resolutions Field Syntax

Source: https://yarnpkg.com/advanced/changelog

Demonstrates the removal of glob syntax in the 'resolutions' field within package.json. The example shows how to update a specific package version without using a wildcard path.

```json
{
  "resolutions": {
    "**/@babel/core": "7.5.5",
    "@babel/core": "7.5.5"
  }
}
```

--------------------------------

### File Opening API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/PosixFS

Provides methods for opening files both synchronously and asynchronously.

```APIDOC
## POST /openPromise

### Description
Opens a file asynchronously and returns a promise that resolves with the file descriptor.

### Method
POST

### Endpoint
/openPromise

### Parameters
#### Path Parameters
- **p** (NativePath) - Required - The path to the file to open.
- **flags** (string) - Required - Flags to determine how the file should be opened (e.g., 'r', 'w', 'a').
- **mode** (number) - Optional - The mode to use when creating the file if it does not exist. Defaults to 0o666.

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (200)
- **fileDescriptor** (number) - The file descriptor for the opened file.

#### Response Example
```json
{
  "fileDescriptor": 3
}
```

## POST /openSync

### Description
Opens a file synchronously and returns the file descriptor.

### Method
POST

### Endpoint
/openSync

### Parameters
#### Path Parameters
- **p** (NativePath) - Required - The path to the file to open.
- **flags** (string) - Required - Flags to determine how the file should be opened (e.g., 'r', 'w', 'a').
- **mode** (number) - Optional - The mode to use when creating the file if it does not exist. Defaults to 0o666.

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (200)
- **fileDescriptor** (number) - The file descriptor for the opened file.

#### Response Example
```json
{
  "fileDescriptor": 3
}
```
```

--------------------------------

### Get Resolution Dependencies for Descriptor

Source: https://yarnpkg.com/api/plugin-file/class/FileResolver

Returns a set of dependent descriptors that need to be resolved before the primary descriptor can be transformed into a locator. This is crucial for transform packages where the original resolution must be preserved.

```javascript
__getResolutionDependencies(descriptor: Descriptor, opts: MinimalResolveOptions): {}
```

--------------------------------

### Get Caller Information in Node.js

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/nodeUtils

Retrieves information about the caller of the current function, including method name, arguments, file, line, and column. Returns null if caller information is unavailable.

```javascript
/**
 * @returns {null | Caller}
 */
function __getCaller() {}
```

--------------------------------

### Configure PnP Ignore Patterns in .yarnrc.yml

Source: https://yarnpkg.com/getting-started/recipes

Defines patterns in the `.yarnrc.yml` file to ignore specific directories or files from Yarn's Plug'n'Play (PnP) resolution. This is crucial for hybrid setups where some projects use `node_modules`.

```yaml
pnpIgnorePatterns:
  - "./nm-packages/**"
```

--------------------------------

### TarballFileFetcher Methods

Source: https://yarnpkg.com/api/plugin-file/class/TarballFileFetcher

Details on the methods available in the TarballFileFetcher class.

```APIDOC
## __fetch

### Description
Fetches the file data for a given locator and options.

### Method
GET

### Endpoint
`/fetch`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The source locator.
- **opts** (FetchOptions) - Required - The fetch options.

### Request Example
```json
{
  "locator": {"type": "npm", "name": "example-package"},
  "opts": {}
}
```

### Response
#### Success Response (200)
- **checksum** (string | null) - The checksum of the fetched package, or null if not available.
- **packageFs** (FakeFS<PortablePath>) - A virtual filesystem representing the package contents.
- **prefixPath** (PortablePath) - The path prefix within the package filesystem.
- **releaseFs** (function) - A function to release the resources used by the package filesystem.

#### Response Example
```json
{
  "checksum": "sha1:abcdef1234567890",
  "packageFs": "<FakeFS instance>",
  "prefixPath": "/package/files",
  "releaseFs": "<function>"
}
```

---

## __fetchFromDisk

### Description
Fetches package data directly from the disk.

### Method
GET

### Endpoint
`/fetchFromDisk`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The source locator.
- **opts** (FetchOptions) - Required - The fetch options.

### Request Example
```json
{
  "locator": {"type": "file", "path": "./local-package"},
  "opts": {}
}
```

### Response
#### Success Response (200)
- **ZipFS** (ZipFS) - A ZipFS instance representing the package data.

#### Response Example
```json
{
  "example": "<ZipFS instance>"
}
```

---

## __getLocalPath

### Description
Retrieves the local path for a given package locator.

### Method
GET

### Endpoint
`/getLocalPath`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The source locator.
- **opts** (FetchOptions) - Required - The fetch options.

### Request Example
```json
{
  "locator": {"type": "file", "path": "./local-package"},
  "opts": {}
}
```

### Response
#### Success Response (200)
- **null** - Returns null as this fetcher does not provide a direct local path.

#### Response Example
```json
{
  "example": null
}
```

---

## __supports

### Description
Checks if the fetcher supports the given locator syntax.

### Method
GET

### Endpoint
`/supports`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The locator to validate.
- **opts** (MinimalFetchOptions) - Required - The fetch options.

### Request Example
```json
{
  "locator": {"type": "tarball", "url": "http://example.com/package.tgz"},
  "opts": {}
}
```

### Response
#### Success Response (200)
- **boolean** - True if the locator is supported, false otherwise.

#### Response Example
```json
{
  "example": true
}
```
```

--------------------------------

### Get username for the publish registry

Source: https://yarnpkg.com/cli/npm/whoami

This command specifically displays the npm username configured for publishing packages. It uses the `--publish` flag to target the registry settings used for package distribution.

```bash
yarn npm whoami --publish
```

--------------------------------

### opendirSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Synchronously opens a directory for reading its entries.

```APIDOC
## opendirSync

### Description
Synchronously opens a directory for reading its entries.

### Method
POST

### Endpoint
/websites/yarnpkg/opendirSync

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path to the directory.
- **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The size of the buffer to use.
  - **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Request Example
```json
{
  "p": "/path/to/directory",
  "opts": {
    "bufferSize": 4096,
    "recursive": true
  }
}
```

### Response
#### Success Response (200)
- **result** (Dir<PortablePath>) - A directory handle object.

#### Response Example
```json
{
  "result": {
    "path": "/path/to/directory"
  }
}
```
```

--------------------------------

### Get Specific Configuration Value in Yarn

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Retrieves a specific configuration value from Yarn using its key. This method is generic and can return a specific type based on the `ConfigurationValueMap`.

```typescript
declare __get <K>(key: K): ConfigurationValueMap[K];
declare __get(key: string): unknown;

```

--------------------------------

### openPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Asynchronously opens a file and returns a file descriptor.

```APIDOC
## openPromise

### Description
Asynchronously opens a file and returns a file descriptor (a number) that can be used for subsequent read/write operations. The `flags` argument specifies how the file should be opened.

### Method
`openPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to open.
- **flags** (string) - Required - A string indicating how the file is to be opened (e.g., 'r' for read, 'w' for write).
#### Optional Parameters
- **mode** (number) - Optional - The file mode to use when creating the file if it does not exist.

### Returns
`Promise<number>` - A promise that resolves with the file descriptor.
```

--------------------------------

### AliasFS Constructor - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/AliasFS

Initializes a new instance of the AliasFS class. It takes a target path and optional configuration options.

```typescript
new AliasFS<P>(target: P, __namedParameters: AliasFSOptions<P>): AliasFS<P>
```

--------------------------------

### Get File Stats - fstatSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Retrieves statistics about a file descriptor synchronously. Supports returning either Stats or BigIntStats based on the provided options. Requires a file descriptor (fd) as input.

```typescript
declare function __fstatSync(fd: number): Stats;
declare function __fstatSync(fd: number, opts: { bigint: true }): BigIntStats;
declare function __fstatSync(fd: number, opts?: { bigint: boolean }): Stats | BigIntStats;
```

--------------------------------

### File System Operations (rm, rmdir, stat, symlink, truncate, writeFile, watch)

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NodeFS

This section details synchronous and asynchronous methods for interacting with the file system, including removing files and directories, retrieving file status, creating symbolic links, truncating files, writing files, and watching for file changes.

```APIDOC
## `rmSync(p: PortablePath, opts?: Partial<{ force: boolean; maxRetries: number; recursive: boolean; retryDelay: number }>): void`

### Description
Synchronously removes a file or directory.

### Method
`rmSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file or directory to remove.
- **opts** (Partial<object>) - Optional - Options for removal.
  - **force** (boolean) - Optional - If true, will attempt to force removal.
  - **maxRetries** (number) - Optional - Maximum number of retries for removal.
  - **recursive** (boolean) - Optional - If true, will attempt to remove recursively.
  - **retryDelay** (number) - Optional - Delay in milliseconds between retries.

### Returns void

## `rmdirPromise(p: PortablePath, opts?: Partial<{ maxRetries: number; recursive: boolean; retryDelay: number }>): Promise<void>`

### Description
Asynchronously removes a directory.

### Method
`rmdirPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory to remove.
- **opts** (Partial<object>) - Optional - Options for removal.
  - **maxRetries** (number) - Optional - Maximum number of retries for removal.
  - **recursive** (boolean) - Optional - If true, will attempt to remove recursively.
  - **retryDelay** (number) - Optional - Delay in milliseconds between retries.

### Returns Promise<void>

## `rmdirSync(p: PortablePath, opts?: Partial<{ maxRetries: number; recursive: boolean; retryDelay: number }>): void`

### Description
Synchronously removes a directory.

### Method
`rmdirSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory to remove.
- **opts** (Partial<object>) - Optional - Options for removal.
  - **maxRetries** (number) - Optional - Maximum number of retries for removal.
  - **recursive** (boolean) - Optional - If true, will attempt to remove recursively.
  - **retryDelay** (number) - Optional - Delay in milliseconds between retries.

### Returns void

## `statPromise(p: PortablePath): Promise<Stats>`
## `statPromise(p: PortablePath, opts: undefined | (StatOptions & { bigint?: false })): Promise<Stats>`
## `statPromise(p: PortablePath, opts: StatOptions & { bigint: true }): Promise<BigIntStats>`

### Description
Asynchronously retrieves the status of a file.

### Method
`statPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (StatOptions & { bigint?: false | true }) - Optional - Options for retrieving stats.

### Returns Promise<Stats> or Promise<BigIntStats>

## `statSync(p: PortablePath): Stats`
## `statSync(p: PortablePath, opts?: StatSyncOptions & { bigint?: false; throwIfNoEntry: false }): undefined | Stats`
## `statSync(p: PortablePath, opts: StatSyncOptions & { bigint: true; throwIfNoEntry: false }): undefined | BigIntStats`
## `statSync(p: PortablePath, opts?: StatSyncOptions & { bigint?: false }): Stats`
## `statSync(p: PortablePath, opts: StatSyncOptions & { bigint: true }): BigIntStats`
## `statSync(p: PortablePath, opts: StatSyncOptions & { bigint: boolean; throwIfNoEntry?: false }): Stats | BigIntStats`

### Description
Synchronously retrieves the status of a file.

### Method
`statSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **opts** (StatSyncOptions & { bigint?: false | true; throwIfNoEntry?: false }) - Optional - Options for retrieving stats.

### Returns Stats or BigIntStats or undefined

## `symlinkPromise(target: PortablePath, p: PortablePath, type?: SymlinkType): Promise<void>`

### Description
Asynchronously creates a symbolic link.

### Method
`symlinkPromise`

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The target of the symbolic link.
- **p** (PortablePath) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of the symbolic link.

### Returns Promise<void>

## `symlinkSync(target: PortablePath, p: PortablePath, type?: SymlinkType): void`

### Description
Synchronously creates a symbolic link.

### Method
`symlinkSync`

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The target of the symbolic link.
- **p** (PortablePath) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of the symbolic link.

### Returns void

## `truncatePromise(p: PortablePath, len?: number): Promise<void>`

### Description
Asynchronously truncates a file to a specified length.

### Method
`truncatePromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to truncate.
- **len** (number) - Optional - The new length of the file. If not provided, the file will be truncated to zero length.

### Returns Promise<void>

## `truncateSync(p: PortablePath, len?: number): void`

### Description
Synchronously truncates a file to a specified length.

### Method
`truncateSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to truncate.
- **len** (number) - Optional - The new length of the file. If not provided, the file will be truncated to zero length.

### Returns void

## `unlinkPromise(p: PortablePath): Promise<void>`

### Description
Asynchronously removes a file.

### Method
`unlinkPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to remove.

### Returns Promise<void>

## `unlinkSync(p: PortablePath): void`

### Description
Synchronously removes a file.

### Method
`unlinkSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to remove.

### Returns void

## `unwatchFile(p: PortablePath, cb?: WatchFileCallback): void`

### Description
Stops watching for changes on a file.

### Method
`unwatchFile`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to stop watching.
- **cb** (WatchFileCallback) - Optional - The callback function to remove.

### Returns void

## `utimesPromise(p: PortablePath, atime: string | number | Date, mtime: string | number | Date): Promise<void>`

### Description
Asynchronously changes the access and modification times of a file.

### Method
`utimesPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **atime** (string | number | Date) - Required - The new access time.
- **mtime** (string | number | Date) - Required - The new modification time.

### Returns Promise<void>

## `utimesSync(p: PortablePath, atime: string | number | Date, mtime: string | number | Date): void`

### Description
Synchronously changes the access and modification times of a file.

### Method
`utimesSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **atime** (string | number | Date) - Required - The new access time.
- **mtime** (string | number | Date) - Required - The new modification time.

### Returns void

## `watch(p: PortablePath, cb?: WatchCallback): Watcher`
## `watch(p: PortablePath, opts: WatchOptions, cb?: WatchCallback): Watcher`

### Description
Watches for changes on a file or directory.

### Method
`watch`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to watch.
- **opts** (WatchOptions) - Optional - Options for watching.
- **cb** (WatchCallback) - Optional - The callback function to execute when a change occurs.

### Returns Watcher

## `watchFile(p: PortablePath, cb: WatchFileCallback): StatWatcher`
## `watchFile(p: PortablePath, opts: Partial<{ bigint: boolean; interval: number; persistent: boolean }>, cb: WatchFileCallback): StatWatcher`

### Description
Watches for changes on a file using polling.

### Method
`watchFile`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to watch.
- **opts** (Partial<object>) - Optional - Options for watching.
  - **bigint** (boolean) - Optional - Use BigInt for file stats.
  - **interval** (number) - Optional - The polling interval in milliseconds.
  - **persistent** (boolean) - Optional - Keep the process running as long as files are being watched.
- **cb** (WatchFileCallback) - Required - The callback function to execute when a change occurs.

### Returns StatWatcher

## `writeFilePromise(p: FSPath<PortablePath>, content: string | ArrayBufferView<ArrayBufferLike>, opts?: WriteFileOptions): Promise<void>`

### Description
Asynchronously writes data to a file.

### Method
`writeFilePromise`

### Parameters
#### Path Parameters
- **p** (FSPath<PortablePath>) - Required - The path to the file to write to.
- **content** (string | ArrayBufferView<ArrayBufferLike>) - Required - The data to write to the file.
- **opts** (WriteFileOptions) - Optional - Options for writing the file.

### Returns Promise<void>

```

--------------------------------

### Yarn Link Command Usage

Source: https://yarnpkg.com/advanced/changelog

Demonstrates how to use the `yarn link` command to manage local package dependencies. This command creates a symbolic link, adding the linked package as a dependency with the `portal:` protocol. To disable a link, remove its resolution entry and run `yarn install`.

```bash
yarn link <package>
yarn link
yarn install
```

--------------------------------

### Create Symbolic Link Synchronously

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Creates a symbolic link synchronously.

```APIDOC
## __symlinkSync

### Description
Creates a symbolic link synchronously.

### Method
Not Applicable (Synchronous function)

### Endpoint
Not Applicable (Local file system operation)

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **p** (PortablePath) - Required - The path where the symbolic link should be created.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "target": "/path/to/original/file",
  "p": "/path/to/symlink"
}
```

### Response
#### Success Response (void)
This function does not return a value upon successful execution.

#### Response Example
None
```

--------------------------------

### Yarn Dedupe: Deduplicate Scoped Packages

Source: https://yarnpkg.com/cli/dedupe

Demonstrates deduplicating packages within a specific scope, such as all packages starting with '@babel/*'. This requires proper shell escaping for the glob pattern.

```bash
yarn dedupe @babel/*
```

--------------------------------

### Get File Stats Asynchronously (Promise)

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Asynchronously retrieves statistics for a file specified by its file descriptor. It can return either `Stats` or `BigIntStats` based on the `bigint` option. Returns a Promise<Stats | BigIntStats>.

```typescript
async __fstatPromise(fd: number): Promise<Stats>
async __fstatPromise(fd: number, opts: { bigint: true }): Promise<BigIntStats>
async __fstatPromise(fd: number, opts?: { bigint?: boolean }): Promise<Stats | BigIntStats>
```

--------------------------------

### makeScriptEnv

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/scriptUtils

Sets up the environment variables for executing scripts, including base environment, bin folder, and optional configurations like corepack ignoring, lifecycle script name, locator, and project.

```APIDOC
## makeScriptEnv

### Description
Sets up the environment variables for executing scripts. It takes an object with base environment, bin folder, and optional parameters.

### Method
Internal Function (details not specified in original text, assume programmatic call)

### Endpoint
N/A (Internal function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
*   **__namedParameters** (Object) - Required
    *   **baseEnv** (Record<string, undefined | string>) - Optional - Base environment variables.
    *   **binFolder** (PortablePath) - Required - The path to the bin folder.
    *   **ignoreCorepack** (boolean) - Optional - Whether to ignore Corepack.
    *   **lifecycleScript** (string) - Optional - The name of the lifecycle script.
    *   **locator** (Locator) - Optional - The locator for the package.
    *   **project** (Project) - Optional - The project instance.

### Request Example
```json
{
  "__namedParameters": {
    "baseEnv": {},
    "binFolder": "/path/to/bin",
    "ignoreCorepack": false,
    "lifecycleScript": "test",
    "locator": null,
    "project": null
  }
}
```

### Response
#### Success Response (200)
*   **ProcessEnv & { BERRY_BIN_FOLDER: string }** - The environment object with added BERRY_BIN_FOLDER.

#### Response Example
```json
{
  "PATH": "/usr/local/bin:/usr/bin:/bin:/path/to/bin",
  "BERRY_BIN_FOLDER": "/path/to/bin",
  "NODE_ENV": "test"
}
```
```

--------------------------------

### NodeModulesFS Constructor

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/NodeModulesFS

Initializes a new instance of NodeModulesFS. It requires a PnpApi instance and optionally accepts NodeModulesFSOptions for configuration.

```typescript
new NodeModulesFS(pnp: PnpApi, __namedParameters?: NodeModulesFSOptions): NodeModulesFS
```

--------------------------------

### Language Name/Linker Setting in package.json

Source: https://yarnpkg.com/configuration/manifest

An internal setting used to select the linker for dependency installation. This field is intended for advanced users and should not be modified without a thorough understanding of its implications.

```json
{
  "languageName": "node"
}
```

--------------------------------

### Configure Yarn to Use PNPM-Style Node Linker

Source: https://yarnpkg.com/blog/release/3

This YAML configuration enables a symlink-based install strategy for Yarn, mimicking the approach used by the pnpm package manager. This setting should be added to your `.yarnrc.yml` file to activate this node linker. It offers an alternative to Yarn's default PnP.

```yaml
nodeLinker: pnpm
```

--------------------------------

### File System Operations (mkdir)

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Provides synchronous and asynchronous methods to create directories.

```APIDOC
## __mkdirSync / __mkdirPromise

### Description
Synchronously or asynchronously creates a directory.

### Method
`__mkdirSync(p: PortablePath, opts?: Partial<{ mode: number; recursive: boolean }>): undefined | string`
`__mkdirPromise(p: PortablePath, opts?: Partial<{ mode: number; recursive: boolean }>): Promise<undefined | string>`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory to create.
- **opts** (object) - Optional - Options for creating the directory.
  - **mode** (number) - Optional - The permission mode for the directory.
  - **recursive** (boolean) - Optional - If true, creates parent directories as needed.

### Response
#### Success Response
- **string** - The path to the created directory if `recursive` is true and parent directories were created.
- **undefined** - If the directory already exists or no parent directories were created.

#### Response Example
```json
"/path/to/created/directory"
```
```

--------------------------------

### Specify Commit Pinning with Git Protocol

Source: https://yarnpkg.com/protocol/git

These examples show how to pin a specific version or branch when fetching a package using the git protocol. This allows for precise control over the package version used. You can specify a tag, commit hash, or branch name.

```bash
git@github.com:yarnpkg/berry.git#tag=@yarnpkg/cli/2.2.0
```

```bash
git@github.com:yarnpkg/berry.git#commit=a806c88
```

```bash
git@github.com:yarnpkg/berry.git#head=master
```

--------------------------------

### Generator Script for Dynamic Package Creation (JavaScript)

Source: https://yarnpkg.com/api/plugin-exec

This JavaScript code demonstrates a generator script executed by the `exec:` protocol. It writes `package.json` and `index.js` into the `buildDir` provided by the `execEnv`. The script uses global `fs` and `path` variables, which are made available in the special execution context. This script creates a simple Node.js package.

```javascript
const {buildDir} = execEnv;

fs.writeFileSync(path.join(buildDir, `package.json`), JSON.stringify({
  name: `pkg`,
  version: `1.0.0`,
}));

fs.writeFileSync(path.join(buildDir, `index.js`), `module.exports = ${Date.now()};
`);
```

--------------------------------

### ExecResolver: Get Candidates

Source: https://yarnpkg.com/api/plugin-exec/class/ExecResolver

The __getCandidates method returns a sorted list of locators that potentially satisfy a given descriptor. The preferred locators should appear first in the returned array to influence the resolution algorithm's prioritization.

```typescript
__getCandidates(descriptor: Descriptor, dependencies: Record<string, Package>, opts: ResolveOptions): Promise<Locator[]>
```

--------------------------------

### Yarnpkg: Workspace Syntax in Peer Dependencies (JSON)

Source: https://yarnpkg.com/blog/release/3

Demonstrates the usage of the `workspace:^` syntax within the `peerDependencies` field of a package.json file. This allows for flexible versioning of local workspace dependencies.

```json
{
  "peerDependencies": {
    "@my/other-package": "workspace:^"
  }
}
```

--------------------------------

### Strict Package Boundaries - Dependency Error Example (JavaScript)

Source: https://yarnpkg.com/blog/release/2

Demonstrates an error scenario in Yarn 2+ where a package attempts to require another package that is not declared in its dependencies. This enforces strict package boundaries.

```javascript
// Error: Something that got detected as your top-level application
// (because it doesn't seem to belong to any package) tried to access
// a package that is not declared in your dependencies
//
// Required package: not-a-dependency (via "not-a-dependency")
// Required by: /Users/mael/my-app/
require(`not-a-dependency`);

```

--------------------------------

### ExecFetcher Constructor

Source: https://yarnpkg.com/api/plugin-exec/class/ExecFetcher

Initializes a new instance of the ExecFetcher. This constructor is essential for creating ExecFetcher objects that can then be used to fetch package data.

```typescript
new ExecFetcher(): ExecFetcher
```

--------------------------------

### opendirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Opens a directory for reading and returns a directory iterator asynchronously. Returns a Promise that resolves with a Dir object.

```APIDOC
## opendirPromise

### Description
Opens a directory for reading and returns a directory iterator asynchronously.

### Method
Not applicable (function signature)

### Endpoint
Not applicable (function signature)

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path to the directory.
* **opts** (object) - Optional - Options for opening the directory.
  * **bufferSize** (number) - Optional - The buffer size for reading directory entries.
  * **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Request Example
```json
{
  "p": "/path/to/directory",
  "opts": {
    "bufferSize": 4096,
    "recursive": true
  }
}
```

### Response
#### Success Response (Promise<Dir<PortablePath>>)
- **Dir<PortablePath>**: An object that can be used to iterate over directory entries.

#### Response Example
```json
{
  "__typename": "Dir"
}
```
```

--------------------------------

### Yarnpkg Report Finalization and Length Recommendation

Source: https://yarnpkg.com/api/yarnpkg-core/class/Report

Details methods for finalizing a report and getting a recommended length for display. `__finalize` is called when a report is complete, and `__getRecommendedLength` suggests an optimal width for output.

```typescript
__finalize(): void
```

```typescript
__getRecommendedLength(): number
```

--------------------------------

### mkdirpSync

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D/class/ZipOpenFS

Synchronously creates a directory, including any necessary parent directories.

```APIDOC
## mkdirpSync

### Description
Synchronously creates a directory, including any necessary parent directories. It can optionally set file permissions and modification/access times.

### Method
`mkdirpSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path of the directory to create.
- **__namedParameters** (object) - Optional - An object containing optional parameters.
  - **chmod** (number) - Optional - The file mode to set for the created directory.
  - **utimes** (Array<string | number | Date>) - Optional - An array containing the access and modification times to set for the directory.

### Returns
`undefined | string` - Returns undefined on success, or a string representing an error message if an error occurs.
```

--------------------------------

### Get username for a specific npm scope

Source: https://yarnpkg.com/cli/npm/whoami

This command retrieves the npm username for a specified scope. It uses the `--scope` option to target a particular registry configuration, outputting the relevant username.

```bash
yarn npm whoami --scope company
```

--------------------------------

### Initialize a named package with yarn init

Source: https://yarnpkg.com/cli/init

Initializes a new package with a specified name using the '-n' or '--name' option.

```bash
yarn init -n "my-package"
```

--------------------------------

### EntryCommand Constructor - yarnpkg

Source: https://yarnpkg.com/api/plugin-essentials/class/EntryCommand

Initializes a new instance of the EntryCommand class. This constructor is the default way to create an EntryCommand object.

```typescript
new EntryCommand(): default
```

--------------------------------

### Portable Script Execution with $npm_execpath (Shell)

Source: https://yarnpkg.com/advanced/rulebook

Provides a portable solution for executing scripts within package scripts, such as `postinstall`. Using the `$npm_execpath` environment variable ensures that the correct package manager's run command is invoked, regardless of whether npm or Yarn is used by the consumer. This avoids issues with package manager interchangeability.

```shell
$npm_execpath run <name>
```

--------------------------------

### Add Package from GitHub URL with Yarn

Source: https://yarnpkg.com/cli/add

Shows how to add a package directly from a GitHub repository URL. This is useful for including packages not published to a registry.

```bash
yarn add lodash@https://github.com/lodash/lodash

```

--------------------------------

### Find Package Location

Source: https://yarnpkg.com/api/plugin-nm/class/NodeModulesLinker

Asynchronously finds the file system location of an installed package given its locator. This method is restricted to returning a file path and is essential for resolving package whereabouts on disk, potentially within archives.

```typescript
__findPackageLocation(locator: Locator, opts: LinkOptions): Promise<PortablePath>
```

--------------------------------

### Get Candidate Locators for Descriptor

Source: https://yarnpkg.com/api/plugin-file/class/FileResolver

Retrieves a list of locators that potentially satisfy a given descriptor. The returned array should be sorted with preferred locators first to influence the resolution algorithm's prioritization.

```javascript
__getCandidates(descriptor: Descriptor, dependencies: unknown, opts: ResolveOptions): Promise<Locator[]>
```

--------------------------------

### Get Candidate Locators from Descriptor

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Resolver

Retrieves a list of candidate locators that satisfy a given descriptor. The array must be sorted with preferred locators first to influence the resolution algorithm's prioritization.

```typescript
declare function __getCandidates(descriptor: Descriptor, dependencies: Record<string, Package>, opts: ResolveOptions): Promise<Locator[]>
```

--------------------------------

### Portable Shell Execution in Yarn Scripts

Source: https://yarnpkg.com/features/scripting

Yarn provides a Posix-like shell interpreter that ensures script portability across different operating systems, including Windows. This allows for standard shell scripting syntax within package.json scripts without requiring external Posix shell installations.

```bash
$ NODE_ENV=production webpack
```

--------------------------------

### Open Workspace - @yarnpkg/cli

Source: https://yarnpkg.com/api/yarnpkg-cli

Opens and returns a workspace instance based on the provided configuration and current working directory. This is crucial for interacting with the project's workspace structure.

```typescript
function __openWorkspace(configuration: Configuration, cwd: PortablePath): Promise<Workspace>
```

--------------------------------

### Install Dependencies Offline with Yarn

Source: https://yarnpkg.com/blog/2016/11/24/offline-mirror

The '--offline' flag instructs Yarn to only use the local cache and avoid network requests. This is useful for testing offline functionality or working in environments without internet access.

```bash
yarn install --offline
```

--------------------------------

### Add local package using file: protocol

Source: https://yarnpkg.com/protocol/file

Adds a package from a local directory using the file: protocol. This is useful for testing local packages before publishing or for using specific local dependencies. The path specified is relative to the project's root. No special dependencies are required beyond Yarn.

```bash
yarn add my-pkg@file:./relative/path/to/dependency/folder
```

--------------------------------

### Add External Directory Dependency with Yarn Link

Source: https://yarnpkg.com/protocol/link

This command uses Yarn's `link:` protocol to add an external directory as a dependency. The target directory, `./static/imgs` in this example, must not contain a `package.json` file. This is useful for referencing local assets or directories that are not intended to be managed as separate packages.

```bash
yarn add imgs@link:./static/imgs
```

--------------------------------

### Build Node Modules Tree - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-nm

Constructs an in-memory representation of the hoisted node_modules directories. It takes a PnP API instance and options as input and returns potential errors, a flag indicating if symlinks are required, and the generated tree structure. This function is crucial for understanding the layout of installed packages.

```typescript
import {PnpApi} from '@yarnpkg/core';
import {NodeModulesTreeOptions, NodeModulesTree} from './index';

function buildNodeModulesTree(pnp: PnpApi, options: NodeModulesTreeOptions): {
  errors: any;
  preserveSymlinksRequired: boolean;
  tree: NodeModulesTree | null;
} {
  // Implementation details...
  return { errors: [], preserveSymlinksRequired: false, tree: null };
}
```

--------------------------------

### Manage Project Constraints with Yarn CLI

Source: https://context7.com/context7/yarnpkg/llms.txt

Illustrates the command-line interface commands for managing project constraints. This includes checking for violations, automatically fixing them, querying the constraint database, and viewing the source code of constraints.

```bash
# Check constraints
yarn constraints

# Auto-fix constraint violations
yarn constraints --fix

# Query constraints database
yarn constraints query

# Show constraint source code
yarn constraints source
```

--------------------------------

### Workspace Get Recursive Workspace Children Method - Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-core/class/Workspace

Retrieves all child workspaces of a given root workspace recursively. This is essential for understanding the hierarchical structure of a monorepo and managing nested workspaces.

```typescript
__getRecursiveWorkspaceChildren(): Workspace[]
```

--------------------------------

### Yarn Plugin with a Custom Command (JavaScript)

Source: https://yarnpkg.com/advanced/plugin-tutorial

Demonstrates how to add a new command to Yarn using a plugin. It utilizes the `clipanion` library to define a `BaseCommand` with a specific path (`hello`) and an `execute` function that writes a message to standard output.

```javascript
module.exports = {
  name: `plugin-hello-world`,
  factory: require => {
    const {BaseCommand} = require(`@yarnpkg/cli`);

    class HelloWorldCommand extends BaseCommand {
      static paths = [[`hello`]];

      async execute() {
        this.context.stdout.write(`This is my very own plugin 😎\n`);
      }
    }

    return {
      commands: [
        HelloWorldCommand,
      ],
    };
  }
};

```

--------------------------------

### AddCommand Properties - Yarnpkg

Source: https://yarnpkg.com/api/plugin-essentials/class/AddCommand

Defines the properties of the AddCommand class, which control various aspects of package addition, such as caching, dependency types (dev, peer, optional), installation modes, and package name resolution. These properties allow fine-grained control over how packages are added.

```typescript
__cached :  boolean = ...
```

```typescript
__caret :  boolean = ...
```

```typescript
__cwd :  undefined | string = ...
```

```typescript
__dev :  boolean = ...
```

```typescript
__exact :  boolean = ...
```

```typescript
__fixed :  boolean = ...
```

```typescript
__interactive :  undefined | boolean = ...
```

```typescript
__json :  boolean = ...
```

```typescript
__mode :  undefined | InstallMode = ...
```

```typescript
__optional :  boolean = ...
```

```typescript
__packages :  string[] = ...
```

```typescript
__peer :  boolean = ...
```

```typescript
__preferDev :  boolean = ...
```

```typescript
__silent :  undefined | boolean = ...
```

```typescript
__tilde :  boolean = ...
```

--------------------------------

### Method: __fetchFromDisk() - Fetch from Local Disk

Source: https://yarnpkg.com/api/plugin-file/class/TarballFileFetcher

Fetches package data directly from the local disk, presumably from a tarball file. It returns a promise that resolves to a ZipFS object, representing the file system structure of the tarball.

```typescript
__fetchFromDisk(locator: Locator, opts: FetchOptions): Promise<ZipFS>
```

--------------------------------

### Enforce Node Engine Version (CJS)

Source: https://yarnpkg.com/features/constraints

This example shows how to configure `yarn.config.cjs` to enforce a specific Node.js engine version across all workspaces. It iterates through each workspace and sets the `engines.node` field to '20.0.0'.

```javascript
module.exports = {
  async constraints({Yarn}) {
    for (const workspace of Yarn.workspaces()) {
      workspace.set('engines.node', `20.0.0`);
    }
  },
};
```

--------------------------------

### Find Package Location - Linker Method

Source: https://yarnpkg.com/api/yarnpkg-core/interface/Linker

The `findPackageLocation` method is responsible for locating the installed path of a given package based on its locator. It must return a `PortablePath` and is distinct from fetchers in that it only returns a path, though the interpretation of this path is flexible and can point to locations within zip archives.

```TypeScript
/**
 * @param {Locator} locator The queried package.
 * @param {LinkOptions} opts The link options.
 * @returns {Promise<PortablePath>} The path where the package is installed.
 */
__findPackageLocation(locator: Locator, opts: LinkOptions): Promise<PortablePath>
```

--------------------------------

### File System Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

This section details various file system operations, including changing ownership, closing files, copying files, creating streams, checking existence, and retrieving file statistics.

```APIDOC
## chownSync /websites/yarnpkg

### Description
Changes the owner and group of a file.

### Method
`chownSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **p** (PortablePath) - Description: The path to the file.
- **uid** (number) - Description: The user ID to set.
- **gid** (number) - Description: The group ID to set.

### Returns void

```

```APIDOC
## closePromise /websites/yarnpkg

### Description
Closes a file descriptor asynchronously.

### Method
`closePromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor to close.

### Returns Promise<void>

```

```APIDOC
## closeSync /websites/yarnpkg

### Description
Closes a file descriptor synchronously.

### Method
`closeSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor to close.

### Returns void

```

```APIDOC
## copyFilePromise /websites/yarnpkg

### Description
Copies a file asynchronously.

### Method
`copyFilePromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **sourceP** (PortablePath) - Description: The path to the source file.
- **destP** (PortablePath) - Description: The path to the destination file.
- **flags** (number) - Optional - Description: Flags to control the copy operation.

### Returns Promise<void>

```

```APIDOC
## copyFileSync /websites/yarnpkg

### Description
Copies a file synchronously.

### Method
`copyFileSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **sourceP** (PortablePath) - Description: The path to the source file.
- **destP** (PortablePath) - Description: The path to the destination file.
- **flags** (number) - Optional - Description: Flags to control the copy operation.

### Returns void

```

```APIDOC
## copyPromise /websites/yarnpkg

### Description
Copies a file or directory. This is the preferred method for copying operations.

### Method
`copyPromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **destination** (PortablePath) - Description: The destination path.
- **source** (PortablePath) - Description: The source path.
- **options** (object) - Optional - Description: Options for the copy operation.
  - **baseFs** (undefined) - Optional - Description: Base filesystem to use.
  - **linkStrategy** (null | LinkStrategy<PortablePath>) - Optional - Description: Strategy for handling symbolic links.
  - **overwrite** (boolean) - Optional - Description: Whether to overwrite existing files.
  - **stableSort** (boolean) - Optional - Description: Whether to use stable sorting.
  - **stableTime** (boolean) - Optional - Description: Whether to preserve modification times.

### Returns Promise<void>

```

```APIDOC
## copySync /websites/yarnpkg

### Description
Copies a file or directory synchronously. Prefer using `copyPromise` instead.

### Method
`copySync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **destination** (PortablePath) - Description: The destination path.
- **source** (PortablePath) - Description: The source path.
- **options** (object) - Optional - Description: Options for the copy operation.
  - **baseFs** (undefined) - Optional - Description: Base filesystem to use.
  - **overwrite** (boolean) - Optional - Description: Whether to overwrite existing files.

### Returns void

```

```APIDOC
## createReadStream /websites/yarnpkg

### Description
Creates a readable stream for a file.

### Method
`createReadStream`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **p** (null | PortablePath) - Description: The path to the file.
- **opts** (Partial<{ encoding: BufferEncoding; fd: number }>) - Optional - Description: Options for the read stream.
  - **encoding** (BufferEncoding) - Description: The encoding of the file.
  - **fd** (number) - Description: The file descriptor.

### Returns ReadStream

```

```APIDOC
## createWriteStream /websites/yarnpkg

### Description
Creates a writable stream for a file.

### Method
`createWriteStream`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **p** (null | PortablePath) - Description: The path to the file.
- **opts** (Partial<{ encoding: BufferEncoding; fd: number; flags: a }>) - Optional - Description: Options for the write stream.
  - **encoding** (BufferEncoding) - Description: The encoding of the file.
  - **fd** (number) - Description: The file descriptor.
  - **flags** (a) - Description: Flags to control the write operation.

### Returns WriteStream

```

```APIDOC
## existsPromise /websites/yarnpkg

### Description
Checks if a file or directory exists asynchronously.

### Method
`existsPromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **p** (PortablePath) - Description: The path to check.

### Returns Promise<boolean>

```

```APIDOC
## existsSync /websites/yarnpkg

### Description
Checks if a file or directory exists synchronously.

### Method
`existsSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **p** (PortablePath) - Description: The path to check.

### Returns boolean

```

```APIDOC
## fchmodPromise /websites/yarnpkg

### Description
Changes the permissions of a file asynchronously.

### Method
`fchmodPromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor.
- **mask** (number) - Description: The permission mask.

### Returns Promise<void>

```

```APIDOC
## fchmodSync /websites/yarnpkg

### Description
Changes the permissions of a file synchronously.

### Method
`fchmodSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor.
- **mask** (number) - Description: The permission mask.

### Returns void

```

```APIDOC
## fchownPromise /websites/yarnpkg

### Description
Changes the owner and group of a file asynchronously.

### Method
`fchownPromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor.
- **uid** (number) - Description: The user ID to set.
- **gid** (number) - Description: The group ID to set.

### Returns Promise<void>

```

```APIDOC
## fchownSync /websites/yarnpkg

### Description
Changes the owner and group of a file synchronously.

### Method
`fchownSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor.
- **uid** (number) - Description: The user ID to set.
- **gid** (number) - Description: The group ID to set.

### Returns void

```

```APIDOC
## fstatPromise /websites/yarnpkg

### Description
Retrieves the status of a file asynchronously.

### Method
`fstatPromise`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor.
- **opts** (object) - Optional - Description: Options for the stat operation.
  - **bigint** (boolean) - Optional - Description: Whether to return BigInt stats.

### Returns Promise<Stats | BigIntStats>

```

```APIDOC
## fstatSync /websites/yarnpkg

### Description
Retrieves the status of a file synchronously.

### Method
`fstatSync`

### Endpoint
`/websites/yarnpkg

### Parameters
#### Path Parameters
- **fd** (number) - Description: The file descriptor.
- **opts** (object) - Optional - Description: Options for the stat operation.
  - **bigint** (boolean) - Optional - Description: Whether to return BigInt stats.

### Returns Stats | BigIntStats

```

--------------------------------

### Yarn Performance Benchmark Command

Source: https://yarnpkg.com/blog/release/4

The command used to benchmark Yarn 3.6.0 against Yarn 4.0.0 for installing the Gatsby package. It utilizes hyperfine for performance comparison, preparing the environment by cleaning the cache and setting up a new project with a specific Yarn version.

```shell
hyperfine -L v stable,canary --prepare 'rm -rf ~/.yarn/berry/cache' 'cd $(mktemp -d) && yarn init -2 && yarn set version {v} && yarn && yarn add gatsby --mode=skip-build'
```

--------------------------------

### NewPluginCommand Properties

Source: https://yarnpkg.com/api/yarnpkg-builder/class/NewPluginCommand

Details the properties of the NewPluginCommand, including target (string), paths (string[][]), and usage (Usage). These properties likely store configuration and operational data for the command.

```typescript
__target : string = ...
```

```typescript
__paths : string[][] = ...
```

```typescript
__usage : Usage = ...
```

--------------------------------

### openSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Synchronously opens a file and returns a file descriptor.

```APIDOC
## openSync

### Description
Synchronously opens a file and returns a file descriptor (a number) that can be used for subsequent read/write operations. The `flags` argument specifies how the file should be opened.

### Method
`openSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file to open.
- **flags** (string) - Required - A string indicating how the file is to be opened (e.g., 'r' for read, 'w' for write).
#### Optional Parameters
- **mode** (number) - Optional - The file mode to use when creating the file if it does not exist.

### Returns
`number` - The file descriptor.
```

--------------------------------

### Create Symbolic Link Asynchronously

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Creates a symbolic link asynchronously.

```APIDOC
## __symlinkPromise

### Description
Creates a symbolic link asynchronously.

### Method
Not Applicable (Asynchronous function)

### Endpoint
Not Applicable (Local file system operation)

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **p** (PortablePath) - Required - The path where the symbolic link should be created.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "target": "/path/to/original/file",
  "p": "/path/to/symlink"
}
```

### Response
#### Success Response (Promise<void>)
Returns a Promise that resolves when the symbolic link has been created.

#### Response Example
```json
null
```
```

--------------------------------

### Get File Stats - lstatSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Synchronously retrieves statistics about a file (not following symbolic links). Supports various options including bigint and throwIfNoEntry, allowing for flexible return types (Stats, BigIntStats, or undefined). Requires a PortablePath as input.

```typescript
declare function __lstatSync(p: PortablePath): Stats;
declare function __lstatSync(p: PortablePath, opts?: StatSyncOptions & { bigint?: false; throwIfNoEntry: false }): undefined | Stats;
declare function __lstatSync(p: PortablePath, opts: StatSyncOptions & { bigint: true; throwIfNoEntry: false }): undefined | BigIntStats;
declare function __lstatSync(p: PortablePath, opts?: StatSyncOptions & { bigint?: false }): Stats;
declare function __lstatSync(p: PortablePath, opts: StatSyncOptions & { bigint: true }): BigIntStats;
declare function __lstatSync(p: PortablePath, opts: StatSyncOptions & { bigint: boolean; throwIfNoEntry?: false }): Stats | BigIntStats;
```

--------------------------------

### Yarn Dedupe: Check for Duplicates (CI Step)

Source: https://yarnpkg.com/cli/dedupe

Provides an example of using the '--check' flag with 'yarn dedupe'. This mode only reports duplicates without modifying the lockfile, making it suitable for continuous integration pipelines.

```bash
yarn dedupe --check
```

--------------------------------

### mkdirpPromise API

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Asynchronously creates a directory and its parents if they don't exist. Supports setting permissions and modification times.

```APIDOC
## mkdirpPromise

### Description
Asynchronously creates a directory and its parents if they do not exist. This function allows for optional `chmod` and `utimes` parameters to set file permissions and modification times.

### Method
* N/A (Asynchronous function call)

### Endpoint
* N/A (This is a library function, not a web endpoint)

### Parameters
#### Path Parameters
* None

#### Query Parameters
* None

#### Request Body
* **p** (PortablePath) - Required - The path of the directory to create.
* **__namedParameters** (object) - Optional - An object containing optional parameters.
  * **chmod** (number) - Optional - The permission mode to set for the created directory.
  * **utimes** (Array<string | number | Date>) - Optional - An array containing the access and modification times to set for the directory.

### Request Example
*N/A (This is a function signature, not a request body)*

### Response
#### Success Response
* Returns `Promise<undefined | string>`.
  * `undefined` if the operation was successful.
  * `string` if an error occurred (e.g., path already exists and is not a directory).

#### Response Example
*N/A (Asynchronous function, result is returned via Promise)*
```

--------------------------------

### Get First Hook in Yarn Configuration

Source: https://yarnpkg.com/api/yarnpkg-core/class/Configuration

Retrieves the result of the first hook that matches the provided getter function. It handles asynchronous operations and returns null if no hook is found or if the hook returns void.

```typescript
declare __firstHook <U, V, HooksDefinition>(get: (hooks: HooksDefinition) => undefined | ((...args: U) => Promise<V>), ...args: U): Promise<null | Exclude<V, void>>;

```

--------------------------------

### Yarnpkg: Get Workspace (Current or Filtered)

Source: https://yarnpkg.com/api/yarnpkg-types/namespace/Yarn

Selects a unique workspace. If no filter is provided, it returns the current workspace. Otherwise, it returns a workspace matching the provided filter. Returns null if no workspace matches the filter.

```typescript
/**
 * Select a unique workspace according to the provided filter.
 * @param filter Optional filter to apply to find the workspace.
 * @returns A Workspace object or null.
 */
__workspace(filter?: WorkspaceFilter): null | Workspace;

/**
 * Select the current workspace.
 * @returns The current Workspace object.
 */
__workspace(): Workspace;
```

--------------------------------

### FileFetcher __fetch Method

Source: https://yarnpkg.com/api/plugin-file/class/FileFetcher

Fetches package data for a given locator and options. It returns a promise with details about the package's location on disk, potentially including virtual paths, and a function to release resources.

```typescript
__fetch(locator: Locator, opts: FetchOptions): Promise<{ checksum: null | string; localPath: null | PortablePath; packageFs: FakeFS<PortablePath>; prefixPath: PortablePath; releaseFs: () => void }>
```

--------------------------------

### Yarn Command - Update Lockfile Mode

Source: https://yarnpkg.com/cli/up

Employs the '--mode update-lockfile' option to update the lockfile without performing a full installation. This mode is ideal for CI/CD pipelines or automated dependency management tools.

```bash
yarn up --mode update-lockfile
```

--------------------------------

### Yarn Dedupe: JSON Output Mode

Source: https://yarnpkg.com/cli/dedupe

Example of how to use the '--json' flag to format the output of 'yarn dedupe' as an NDJSON stream. This is useful for programmatic processing of the command's results.

```bash
yarn dedupe --json
```

--------------------------------

### PnP API Overview

Source: https://yarnpkg.com/advanced/pnpapi

The `pnpapi` module is a built-in module available in Plug'n'Play environments. It exposes constants and functions for interacting with the PnP system.

```APIDOC
## `require('pnpapi')`

When operating under a Plug'n'Play environment, a new builtin module will appear in your tree and will be made available to all your packages: `pnpapi`. It exposes the constants and functions described in this document.

The `pnpapi` builtin is contextual, meaning each package from different dependency trees will get different instances.
```

--------------------------------

### execvp Function

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/execUtils

Executes a command using execvp, handling different encoding options.

```APIDOC
## Function: execvp

### Description
Executes a command using execvp.

### Signature
- `execvp(fileName: string, args: string[], opts: ExecvpOptions & { encoding: buffer }): Promise<{ code: number; stderr: Buffer; stdout: Buffer }>`
- `execvp(fileName: string, args: string[], opts: ExecvpOptions & { encoding: string }): Promise<{ code: number; stderr: string; stdout: string }>`
- `execvp(fileName: string, args: string[], opts: ExecvpOptions): Promise<{ code: number; stderr: string; stdout: string }>`

### Parameters
- `fileName` (string): The name of the file to execute.
- `args` (string[]): An array of arguments for the command.
- `opts` (ExecvpOptions): Options for the execution, including encoding.
```

--------------------------------

### Directory Creation API

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipOpenFS

Provides functions to synchronously create directories.

```APIDOC
## mkdirpSync /websites/yarnpkg

### Description
Creates a directory recursively. If the directory already exists, it does nothing.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirpSync

### Parameters
#### Path Parameters
None

#### Query Parameters
* **p** (PortablePath) - Required - The path of the directory to create.
* **chmod** (number) - Optional - The file mode to use when creating the directory.
* **utimes** ([string | number | Date, string | number | Date]) - Optional - The access and modification times to use when creating the directory.

#### Request Body
None

### Request Example
```json
{
  "p": "/path/to/new/directory",
  "chmod": 755,
  "utimes": ["2023-01-01T00:00:00Z", "2023-01-01T00:00:00Z"]
}
```

### Response
#### Success Response (200)
- **result** (string | undefined) - Returns the path of the created directory if successful, otherwise undefined.
```

--------------------------------

### Yarn Dedupe: Skip Build Scripts Mode

Source: https://yarnpkg.com/cli/dedupe

Demonstrates the '--mode skip-build' option for 'yarn dedupe'. This mode prevents build scripts from running during the deduplication process, potentially speeding up installations.

```bash
yarn dedupe --mode skip-build
```

--------------------------------

### JavaScript Using findPnpApi to Resolve Dependencies

Source: https://yarnpkg.com/advanced/pnpapi

Shows how to use `findPnpApi` from the `module` built-in to locate the PnP API for a given module path, and then use `createRequire` to load resolved dependencies.

```javascript
const {createRequire, findPnpApi} = require(`module`);

// We'll be able to inspect the dependencies of the module passed as first argument
const targetModule = process.argv[2];

const targetPnp = findPnpApi(targetModule);
const targetRequire = createRequire(targetModule);

const resolved = targetPnp.resolveRequest(`eslint`, targetModule);
const instance = targetRequire(resolved); // <-- important! don't use `require`!

```

--------------------------------

### opendirPromise API

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Asynchronously opens a directory for reading its entries. Supports buffer size and recursive options.

```APIDOC
## opendirPromise

### Description
Asynchronously opens a directory for reading its entries. This function supports options to control the buffer size for reading entries and whether to perform a recursive read.

### Method
* N/A (Asynchronous function call)

### Endpoint
* N/A (This is a library function, not a web endpoint)

### Parameters
#### Path Parameters
* None

#### Query Parameters
* None

#### Request Body
* **p** (PortablePath) - Required - The path to the directory to open.
* **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - An object containing options for opening the directory.
  * **bufferSize** (number) - Optional - The size of the buffer to use for reading directory entries.
  * **recursive** (boolean) - Optional - If true, reads entries recursively.

### Request Example
*N/A (This is a function signature, not a request body)*

### Response
#### Success Response
* Returns `Promise<Dir<PortablePath>>` - An object representing the opened directory stream.

#### Response Example
*N/A (Asynchronous function, result is returned via Promise)*
```

--------------------------------

### Instantiate PluginRuntimeCommand (TypeScript)

Source: https://yarnpkg.com/api/plugin-essentials/class/PluginRuntimeCommand

Demonstrates how to create a new instance of PluginRuntimeCommand. This is the default constructor and requires no arguments.

```typescript
new PluginRuntimeCommand(): default
```

--------------------------------

### JavaScript Using createRequire.resolve to Find Dependencies

Source: https://yarnpkg.com/advanced/pnpapi

Illustrates an alternative method to resolve dependencies using only `createRequire` and its `resolve` function, which can often replace the need for `findPnpApi`.

```javascript
const {createRequire} = require(`module`);

// We'll be able to inspect the dependencies of the module passed as first argument
const targetModule = process.argv[2];

const targetRequire = createRequire(targetModule);

const resolved = targetRequire.resolve(`eslint`);
const instance = targetRequire(resolved); // <-- still important

```

--------------------------------

### TypeScript: Hook for after dependency removal from workspace

Source: https://yarnpkg.com/api/plugin-essentials/interface/Hooks

This hook is called when a dependency range is removed from a workspace. It is only triggered by CLI commands such as 'yarn remove'. Manually altering the manifest and running 'yarn install' will not activate this hook.

```typescript
afterWorkspaceDependencyRemoval?: (workspace: Workspace, target: Target, descriptor: Descriptor) => Promise<void>
```

--------------------------------

### Gitignore for Yarn Projects with Zero-Installs

Source: https://yarnpkg.com/getting-started/qa

This configuration is for projects utilizing Yarn's Zero-Installs feature. It specifies files and directories that should be ignored by Git, with exceptions for essential cache and plugin directories.

```gitignore
.yarn/*
!.yarn/cache
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions

```

--------------------------------

### pipevp Function

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/execUtils

Executes a command using pipevp with specified options.

```APIDOC
## Function: pipevp

### Description
Executes a command using pipevp.

### Signature
- `pipevp(fileName: string, args: string[], namedParameters: PipevpOptions): Promise<{ code: number }>`

### Parameters
- `fileName` (string): The name of the file to execute.
- `args` (string[]): An array of arguments for the command.
- `namedParameters` (PipevpOptions): Options for the pipe operation, including streams and end strategy.
```

--------------------------------

### Fix Missing Dependencies with packageExtensions in YAML

Source: https://yarnpkg.com/migration/pnp

Allows you to declare missing dependencies or peer dependencies for packages. This is useful when a package doesn't list all its required dependencies, preventing installation or runtime errors. It's configured in the `.yarnrc.yml` file.

```yaml
packageExtensions:
  "react@*":
    dependencies:
      prop-types: "*"

packageExtensions:
  "@babel/plugin-something@*":
    peerDependencies:
      "@babel/core": "*"
```

--------------------------------

### TypeScript: Hook for after dependency replacement in workspace

Source: https://yarnpkg.com/api/plugin-essentials/interface/Hooks

This hook is executed when a dependency range is replaced within a workspace. It is specifically triggered by CLI commands like 'yarn add'. Manual updates to the manifest followed by 'yarn install' will not invoke this hook.

```typescript
afterWorkspaceDependencyReplacement?: (workspace: Workspace, target: Target, fromDescriptor: Descriptor, toDescriptor: Descriptor) => Promise<void>
```

--------------------------------

### Yarn dependenciesMeta Configuration (unplugged)

Source: https://yarnpkg.com/configuration/manifest

Configures whether a package must be unplugged during installation. If true, the specified package will be automatically unplugged. This is typically needed for packages containing scripts in languages other than JavaScript, such as C++ headers in the 'nan' package.

```json
{
  "dependenciesMeta": {
    "fsevents": {
      "unplugged": true
    }
  }
}
```

--------------------------------

### NpmHttpFetcher Constructor

Source: https://yarnpkg.com/api/plugin-npm/class/NpmHttpFetcher

Initializes a new instance of the NpmHttpFetcher. This is the primary way to create a fetcher object for interacting with the npm registry.

```typescript
new NpmHttpFetcher(): NpmHttpFetcher
```

--------------------------------

### Configure Yarn Offline Mirror Directory

Source: https://yarnpkg.com/blog/2016/11/24/offline-mirror

This command sets a local directory path where Yarn will store compressed package tarballs. This directory acts as a mirror of the packages downloaded from the registry, enabling offline installations. It's a crucial step for ensuring repeatable builds.

```bash
$ yarn config set yarn-offline-mirror ./npm-packages-offline-cache
yarn config v0.23.2
success Set "yarn-offline-mirror" to "./npm-packages-offline-cache".
✨  Done in 0.06s.
```

--------------------------------

### opendirSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Synchronously opens a directory and returns a directory iterator.

```APIDOC
## __opendirSync

### Description
Synchronously opens a directory and returns a directory iterator.

### Method
POST

### Endpoint
`/opendir` (Conceptual endpoint for the operation)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory.

#### Query Parameters
- **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The buffer size for reading directory entries.
  - **recursive** (boolean) - Optional - Whether to read the directory recursively.

### Returns
`Dir<PortablePath>` - A directory iterator.

```

--------------------------------

### Workspace Get Recursive Workspace Dependencies Method - Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-core/class/Workspace

Finds workspaces marked as dependencies or devDependencies of the current workspace recursively. It allows filtering by specific dependency types, returning a set of related workspaces.

```typescript
__getRecursiveWorkspaceDependencies(__namedParameters?: { dependencies?: HardDependencies[] }): Set<Workspace>
```

--------------------------------

### Convert TreeNode to Treeify Format

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/treeUtils

The __treeNodeToTreeify function transforms a TreeNode into a format compatible with the 'treeify' library. It requires a TreeNode and a Configuration object to guide the transformation. The function returns an object representing the tree in treeify format.

```typescript
declare function __treeNodeToTreeify(printTree: TreeNode, __namedParameters: { configuration: Configuration }): {};
```

--------------------------------

### Yarn Error Code: YN0005 - BUILD_DISABLED

Source: https://yarnpkg.com/advanced/error-codes

The YN0005 error code signifies that a package's build scripts have been explicitly disabled within its own configuration. A notification is emitted, indicating the installation may not be fully complete.

```text
YN0005 - `BUILD_DISABLED`​
A package has build scripts, but they've been disabled through its configuration.
Build scripts can be disabled on a per-project basis through the use of the `dependenciesMeta` settings from the `package.json` file. When it happens, a notification is still emitted to let you know that the installation might not be complete.
```

--------------------------------

### Function: __hydratePnpFile

Source: https://yarnpkg.com/api/yarnpkg-pnp

Hydrates a Plug'n'Play file from a given location.

```APIDOC
## __hydratePnpFile

### Description
Asynchronously hydrates a Plug'n'Play API object from a file located at the specified path, using a provided fake filesystem and PnP API resolution path.

### Method
N/A (This is a function, not an HTTP endpoint)

### Endpoint
N/A

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
  "location": "/path/to/.pnp.cjs",
  "__namedParameters": {
    "fakeFs": "FakeFS object",
    "pnpapiResolution": "/node_modules/.yarn/pnpapi.cjs"
  }
}
```

### Response
#### Success Response (Promise<PnpApi>)
- **return value** (Promise<PnpApi>) - A promise that resolves to the PnpApi object.

#### Response Example
```json
{
  "example": "// PnpApi object structure..."
}
```
```

--------------------------------

### Specify Yarn Binary Path in Yarn Configuration

Source: https://yarnpkg.com/configuration/yarnrc

Sets a custom path to a Yarn binary to be used instead of the globally installed one. If the file has a `.js` extension, it will be required; otherwise, it will be spawned. Using Corepack is now recommended for managing Yarn versions.

```json
yarnPath: "./scripts/yarn-2.0.0-rc001.js"
```

--------------------------------

### Pass All Script Arguments using $@ in Yarn

Source: https://yarnpkg.com/features/scripting

The $@ variable in Yarn scripts represents an array of all arguments passed to the script. This allows for reusing all arguments in multiple commands within a single script, as demonstrated in the example for a 'build-and-test' script.

```json
{
  "scripts": {
    "build-and-test": "yarn build \"$@\" && yarn test \"$@\""
  }
}
```

--------------------------------

### Enable Hardened Mode via Environment Variable

Source: https://yarnpkg.com/blog/release/4

This snippet demonstrates how to enable Yarn's Hardened Mode for specific CI jobs using an environment variable. Hardened Mode performs extra validations for enhanced security but can slow down installations.

```shell
export YARN_ENABLE_HARDENED_MODE=1  

```

--------------------------------

### File System Operations (Abstract)

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

This section details abstract asynchronous and synchronous file system operations provided by Yarnpkg.

```APIDOC
## chownSync /api/chownSync

### Description
Changes the ownership of a file.

### Method
`POST`

### Endpoint
`/api/chownSync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **uid** (number) - Required - The new user ID.
- **gid** (number) - Required - The new group ID.

### Request Example
```json
{
  "p": "/path/to/file",
  "uid": 1000,
  "gid": 1000
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## closePromise /api/closePromise

### Description
Asynchronously closes a file descriptor.

### Method
`POST`

### Endpoint
`/api/closePromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **fd** (number) - Required - The file descriptor to close.

### Request Example
```json
{
  "fd": 3
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## closeSync /api/closeSync

### Description
Synchronously closes a file descriptor.

### Method
`POST`

### Endpoint
`/api/closeSync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **fd** (number) - Required - The file descriptor to close.

### Request Example
```json
{
  "fd": 3
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## copyFilePromise /api/copyFilePromise

### Description
Asynchronously copies a file from a source path to a destination path.

### Method
`POST`

### Endpoint
`/api/copyFilePromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **sourceP** (PortablePath) - Required - The path to the source file.
- **destP** (PortablePath) - Required - The path to the destination file.
- **flags** (number) - Optional - File copy flags.

### Request Example
```json
{
  "sourceP": "/path/to/source",
  "destP": "/path/to/destination",
  "flags": 1
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## copyFileSync /api/copyFileSync

### Description
Synchronously copies a file from a source path to a destination path.

### Method
`POST`

### Endpoint
`/api/copyFileSync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **sourceP** (PortablePath) - Required - The path to the source file.
- **destP** (PortablePath) - Required - The path to the destination file.
- **flags** (number) - Optional - File copy flags.

### Request Example
```json
{
  "sourceP": "/path/to/source",
  "destP": "/path/to/destination",
  "flags": 1
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## copyPromise /api/copyPromise

### Description
Asynchronously copies a directory or file from a source to a destination.

### Method
`POST`

### Endpoint
`/api/copyPromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **destination** (PortablePath) - Required - The destination path.
- **source** (PortablePath) - Required - The source path.
- **options** (object) - Optional - Copy options.
  - **baseFs** (undefined) - Optional - Base file system.
  - **linkStrategy** (null | LinkStrategy<PortablePath>) - Optional - Link strategy.
  - **overwrite** (boolean) - Optional - Whether to overwrite existing files.
  - **stableSort** (boolean) - Optional - Whether to use stable sorting.
  - **stableTime** (boolean) - Optional - Whether to use stable timestamps.

### Request Example
```json
{
  "destination": "/path/to/destination",
  "source": "/path/to/source",
  "options": {
    "overwrite": true,
    "stableSort": true
  }
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## copySync /api/copySync

### Description
Synchronously copies a directory or file from a source to a destination. Prefer using `copyPromise` instead.

### Method
`POST`

### Endpoint
`/api/copySync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **destination** (PortablePath) - Required - The destination path.
- **source** (PortablePath) - Required - The source path.
- **options** (object) - Optional - Copy options.
  - **baseFs** (undefined) - Optional - Base file system.
  - **overwrite** (boolean) - Optional - Whether to overwrite existing files.

### Request Example
```json
{
  "destination": "/path/to/destination",
  "source": "/path/to/source",
  "options": {
    "overwrite": true
  }
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## createReadStream /api/createReadStream

### Description
Creates a readable stream for a file.

### Method
`POST`

### Endpoint
`/api/createReadStream`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **p** (null | PortablePath) - The path to the file.
- **opts** (Partial<{ encoding: BufferEncoding; fd: number }>) - Optional - Stream options.
  - **encoding** (BufferEncoding) - Optional - File encoding.
  - **fd** (number) - Optional - File descriptor.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "encoding": "utf8"
  }
}
```

### Response
#### Success Response (200)
- **ReadStream** - The readable stream.

#### Response Example
(Stream output)
```

```APIDOC
## createWriteStream /api/createWriteStream

### Description
Creates a writable stream for a file.

### Method
`POST`

### Endpoint
`/api/createWriteStream`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **p** (null | PortablePath) - The path to the file.
- **opts** (Partial<{ encoding: BufferEncoding; fd: number; flags: a }>) - Optional - Stream options.
  - **encoding** (BufferEncoding) - Optional - File encoding.
  - **fd** (number) - Optional - File descriptor.
  - **flags** (a) - Optional - File flags.

### Request Example
```json
{
  "p": "/path/to/file",
  "opts": {
    "flags": "w"
  }
}
```

### Response
#### Success Response (200)
- **WriteStream** - The writable stream.

#### Response Example
(Stream output)
```

```APIDOC
## discardAndClose /api/discardAndClose

### Description
Discards and closes resources.

### Method
`POST`

### Endpoint
`/api/discardAndClose`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
(No request body)

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## existsPromise /api/existsPromise

### Description
Asynchronously checks if a path exists.

### Method
`GET`

### Endpoint
`/api/existsPromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- **p** (PortablePath) - Required - The path to check.

#### Request Body
- None

### Request Example
```
/api/existsPromise?p=/path/to/check
```

### Response
#### Success Response (200)
- **boolean** - `true` if the path exists, `false` otherwise.

#### Response Example
```json
{
  "exists": true
}
```
```

```APIDOC
## existsSync /api/existsSync

### Description
Synchronously checks if a path exists.

### Method
`GET`

### Endpoint
`/api/existsSync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- **p** (PortablePath) - Required - The path to check.

#### Request Body
- None

### Request Example
```
/api/existsSync?p=/path/to/check
```

### Response
#### Success Response (200)
- **boolean** - `true` if the path exists, `false` otherwise.

#### Response Example
```json
{
  "exists": true
}
```
```

```APIDOC
## fchmodPromise /api/fchmodPromise

### Description
Asynchronously changes the permissions of a file descriptor.

### Method
`POST`

### Endpoint
`/api/fchmodPromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **fd** (number) - Required - The file descriptor.
- **mask** (number) - Required - The permission mask.

### Request Example
```json
{
  "fd": 3,
  "mask": 777
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## fchmodSync /api/fchmodSync

### Description
Synchronously changes the permissions of a file descriptor.

### Method
`POST`

### Endpoint
`/api/fchmodSync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **fd** (number) - Required - The file descriptor.
- **mask** (number) - Required - The permission mask.

### Request Example
```json
{
  "fd": 3,
  "mask": 777
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## fchownPromise /api/fchownPromise

### Description
Asynchronously changes the ownership of a file descriptor.

### Method
`POST`

### Endpoint
`/api/fchownPromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **fd** (number) - Required - The file descriptor.
- **uid** (number) - Required - The new user ID.
- **gid** (number) - Required - The new group ID.

### Request Example
```json
{
  "fd": 3,
  "uid": 1000,
  "gid": 1000
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## fchownSync /api/fchownSync

### Description
Synchronously changes the ownership of a file descriptor.

### Method
`POST`

### Endpoint
`/api/fchownSync`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **fd** (number) - Required - The file descriptor.
- **uid** (number) - Required - The new user ID.
- **gid** (number) - Required - The new group ID.

### Request Example
```json
{
  "fd": 3,
  "uid": 1000,
  "gid": 1000
}
```

### Response
#### Success Response (200)
- **None** (void) - Indicates successful completion.

#### Response Example
(No response body on success)
```

```APIDOC
## fstatPromise /api/fstatPromise

### Description
Asynchronously retrieves file status information for a file descriptor.

### Method
`GET`

### Endpoint
`/api/fstatPromise`

### Parameters
#### Path Parameters
- None

#### Query Parameters
- **fd** (number) - Required - The file descriptor.
- **opts.bigint** (boolean) - Optional - Whether to return bigint stats.

#### Request Body
- None

### Request Example
```
/api/fstatPromise?fd=3&opts.bigint=true
```

### Response
#### Success Response (200)
- **Stats | BigIntStats** - File status information.

#### Response Example
```json
{
  "dev": 2050,
  "ino": 25,
  "mode": 33188,
  "nlink": 1,
  "uid": 1000,
  "gid": 1000,
  "rdev": 0,
  "size": 1024,
  "blksize": 4096,
  "blocks": 8,
  "atimeMs": 1678886400000,
  "mtimeMs": 1678886400000,
  "ctimeMs": 1678886400000,
  "birthtimeMs": 1678886400000
}
```
```

--------------------------------

### Handle Deprecated CLI Settings (Yarn v2+)

Source: https://yarnpkg.com/advanced/error-codes

This example illustrates how Yarn v2+ discourages passing CLI command options as arguments (e.g., `--cache-folder`), favoring configuration via `yarnrc` files. For Netlify users, `--cache-folder` is ignored and treated as a warning due to existing automatic passing of this flag. Future releases may remove this special handling.

```bash
# Avoid: yarn install --cache-folder .yarn/cache
# Preferred: Configure in .yarnrc.yml
```

--------------------------------

### Create Directory Recursively - mkdirpPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously creates a directory recursively, ensuring all parent directories exist. Supports optional chmod and utimes options. Returns a Promise that resolves with the created directory path or undefined.

```typescript
declare function __mkdirpPromise(p: PortablePath, __namedParameters?: { chmod?: number; utimes?: [string | number | Date, string | number | Date] }): Promise<undefined | string>;
```

--------------------------------

### NpmSemverFetcher Constructor - TypeScript

Source: https://yarnpkg.com/api/plugin-npm/class/NpmSemverFetcher

Initializes a new NpmSemverFetcher instance. This constructor sets up the fetcher to retrieve package data from the npm registry using semantic versioning.

```typescript
new NpmSemverFetcher(): NpmSemverFetcher
```

--------------------------------

### Directory Creation API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CwdFS

Provides functions to create directories, including recursive creation and setting permissions.

```APIDOC
## mkdirPromise API

### Description
Asynchronously creates a directory. Can create parent directories if they do not exist.

### Method
ASYNC

### Endpoint
N/A (asynchronous function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Create a directory without recursive option
await mkdirPromise('/path/to/new/directory');

// Create a directory recursively with specific mode
await mkdirPromise('/path/to/recursive/directory', { mode: 0o755, recursive: true });
```

### Response
#### Success Response
- **string | undefined** - Returns the path if created, otherwise undefined.

#### Response Example
```json
"/path/to/new/directory"
```
```

```APIDOC
## mkdirSync API

### Description
Synchronously creates a directory. Can create parent directories if they do not exist.

### Method
SYNCHRONOUS

### Endpoint
N/A (synchronous function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Create a directory without recursive option
mkdirSync('/path/to/new/directory');

// Create a directory recursively with specific mode
mkdirSync('/path/to/recursive/directory', { mode: 0o755, recursive: true });
```

### Response
#### Success Response
- **string | undefined** - Returns the path if created, otherwise undefined.

#### Response Example
```json
"/path/to/new/directory"
```
```

```APIDOC
## mkdirpPromise API

### Description
Asynchronously creates a directory, ensuring all parent directories exist. Allows setting mode and utimes for the directory.

### Method
ASYNC

### Endpoint
N/A (asynchronous function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Create directory with default options
await mkdirpPromise('/path/to/deeply/nested/directory');

// Create directory with custom mode and utimes
await mkdirpPromise('/path/to/another/dir', { chmod: 0o700, utimes: ['2023-01-01T12:00:00Z', '2023-01-01T13:00:00Z'] });
```

### Response
#### Success Response
- **string | undefined** - Returns the path if created, otherwise undefined.

#### Response Example
```json
"/path/to/deeply/nested/directory"
```
```

--------------------------------

### Symbolic Link Creation

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/NodeModulesFS

Asynchronously or synchronously create symbolic links.

```APIDOC
## POST /fs/symlinkPromise

### Description
Asynchronously creates a symbolic link. Allows specifying the type of symbolic link.

### Method
POST

### Endpoint
/fs/symlinkPromise

### Parameters
#### Request Body
- **target** (NativePath) - Required - The path the symbolic link should point to.
- **p** (NativePath) - Required - The path where the symbolic link should be created.
- **type** (SymlinkType) - Optional - The type of symbolic link (e.g., 'file', 'dir', 'junction').

### Request Example
```json
{
  "target": "/path/to/original",
  "p": "/path/to/symlink",
  "type": "file"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates successful creation.

#### Response Example
```json
{
  "status": "Symbolic link created successfully."
}
```

## POST /fs/symlinkSync

### Description
Synchronously creates a symbolic link. Allows specifying the type of symbolic link.

### Method
POST

### Endpoint
/fs/symlinkSync

### Parameters
#### Request Body
- **target** (NativePath) - Required - The path the symbolic link should point to.
- **p** (NativePath) - Required - The path where the symbolic link should be created.
- **type** (SymlinkType) - Optional - The type of symbolic link (e.g., 'file', 'dir', 'junction').

### Request Example
```json
{
  "target": "/path/to/original",
  "p": "/path/to/symlink",
  "type": "file"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates successful creation.

#### Response Example
```json
{
  "status": "Symbolic link created successfully."
}
```
```

--------------------------------

### Workspace Get Recursive Workspace Dependents Method - Yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-core/class/Workspace

Finds workspaces that include the current workspace as a dependency or devDependency recursively. Similar to dependencies, it allows filtering and returns a set of workspaces that depend on the current one.

```typescript
__getRecursiveWorkspaceDependents(__namedParameters?: { dependencies?: HardDependencies[] }): Set<Workspace>
```

--------------------------------

### Yarn Dedupe: Update Lockfile Mode

Source: https://yarnpkg.com/cli/dedupe

Shows the usage of '--mode update-lockfile' for 'yarn dedupe'. This mode updates the lockfile without performing the full install and link steps, useful for automated dependency updates.

```bash
yarn dedupe --mode update-lockfile
```

--------------------------------

### Report Creation Methods

Source: https://yarnpkg.com/api/yarnpkg-core/class/Report

Methods for creating report streams and handling progress reporting.

```APIDOC
## Report Creation Methods

### `__createStreamReporter`

*   `__createStreamReporter(prefix?: null | string): PassThrough`

    Creates a stream reporter that can be used to pipe output to.

    #### Parameters
    *   `prefix` (string | null) - Optional. A prefix to be added to the report output.

    #### Returns
    *   `PassThrough` - A stream object for reporting.

### `__startProgressPromise`

*   `__startProgressPromise <T, P>(progressIt: P, cb: (progressIt: P) => Promise<T>): Promise<T>`

    Starts a progress reporting operation that returns a Promise.

    #### Type Parameters
    *   `T` - The return type of the callback function.
    *   `P` - The type of the progress iterable, must extend `ProgressIterable`.

    #### Parameters
    *   `progressIt` (P) - The progress iterable to monitor.
    *   `cb` ((progressIt: P) => Promise<T>) - The callback function to execute, which returns a Promise.

    #### Returns
    *   `Promise<T>` - A Promise that resolves with the result of the callback.

### `__startProgressSync`

*   `__startProgressSync <T, P>(progressIt: P, cb: (progressIt: P) => T): T`

    Starts a synchronous progress reporting operation.

    #### Type Parameters
    *   `T` - The return type of the callback function.
    *   `P` - The type of the progress iterable, must extend `ProgressIterable`.

    #### Parameters
    *   `progressIt` (P) - The progress iterable to monitor.
    *   `cb` ((progressIt: P) => T) - The callback function to execute synchronously.

    #### Returns
    *   `T` - The result of the callback function.
```

--------------------------------

### Yarn sdks Command Usage

Source: https://yarnpkg.com/cli/sdks/default

This snippet shows the general usage of the 'yarn sdks' command. It is used to manage editor SDKs and settings within a Yarn project. The command can be run with various arguments to customize the generation process.

```bash
$ yarn sdks ...
```

--------------------------------

### Get Semantic Version Comparator - JavaScript

Source: https://yarnpkg.com/api/yarnpkg-core-semverUtils

The `getComparator` function takes a `Comparator` object and returns it. This function appears to be a simple pass-through or a utility for type checking/ensuring a Comparator object conforms to the expected structure. Its primary use is likely within the semver utility set.

```javascript
function getComparator(comparators: Comparator): Comparator {
  // Parameters:
  // comparators: Comparator
  // Returns:
  // Comparator
}
```

--------------------------------

### GitFetcher __fetch Method - Yarnpkg

Source: https://yarnpkg.com/api/plugin-git/class/GitFetcher

Fetches package data from a specified locator. This method returns a Promise resolving to a FetchResult, which describes the location of the package data on disk, potentially including virtual paths.

```typescript
__fetch(locator: Locator, opts: FetchOptions): Promise<FetchResult>
```

--------------------------------

### LibZipImpl Constructor

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/LibZipImpl

Initializes a new instance of the LibZipImpl class. It accepts an options object of type ZipImplInput. This constructor is essential for creating and configuring a zip archive handler.

```typescript
__new LibZipImpl(opts: ZipImplInput): LibZipImpl
```

--------------------------------

### GetSetMap Interface Methods - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/miscUtils

Defines the GetSetMap interface, which provides basic get and set operations for a map-like structure. It's generic over key type K and value type V, offering a simple key-value storage pattern.

```typescript
interface GetSetMap<K, V> {
  get(k: K): undefined | V;
  set(k: K, v: V): void;
}
```

--------------------------------

### File System Operations (link)

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Provides synchronous and asynchronous methods to create a hard link.

```APIDOC
## __linkSync / __linkPromise

### Description
Creates a hard link from an existing path to a new path.

### Method
`__linkSync(existingP: PortablePath, newP: PortablePath): void`
`__linkPromise(existingP: PortablePath, newP: PortablePath): Promise<void>`

### Parameters
#### Path Parameters
- **existingP** (PortablePath) - Required - The path to the existing file.
- **newP** (PortablePath) - Required - The path for the new hard link.

### Response
#### Success Response
- **void** - Operation completed successfully.

#### Response Example
```json
// No response body for success
```
```

--------------------------------

### Method: __fetch() - Fetch Package Data

Source: https://yarnpkg.com/api/plugin-file/class/TarballFileFetcher

Fetches the package data for a given locator. It returns a promise that resolves to an object containing the package's file system representation (packageFs), prefix path, an optional checksum, and a function to release the file system resources. This method is crucial for providing package data to the package manager.

```typescript
__fetch(locator: Locator, opts: FetchOptions): Promise<{ checksum: null | string; packageFs: FakeFS<PortablePath>; prefixPath: PortablePath; releaseFs: () => void }>
```

--------------------------------

### PortalFetcher __fetch Method

Source: https://yarnpkg.com/api/plugin-link/class/PortalFetcher

Fetches package data for a given locator. It returns a Promise containing either a local path and package file system, or a virtual package file system. The return type is complex to handle virtual paths.

```typescript
__fetch(locator: Locator, opts: FetchOptions): Promise<{ localPath: PortablePath; packageFs: CwdFS; prefixPath: PortablePath; releaseFs: undefined | () => void } | { localPath?: undefined; packageFs: JailFS; prefixPath: PortablePath; releaseFs: undefined | () => void }>
```

--------------------------------

### Variables

Source: https://yarnpkg.com/api/yarnpkg-cli

Information about globally available variables within the CLI context.

```APIDOC
## Variables

### pluginCommands

`pluginCommands` is a Map that stores command names associated with their respective plugins.
```

--------------------------------

### Prepare for Pack Operation (TypeScript)

Source: https://yarnpkg.com/api/plugin-pack/namespace/packUtils

Prepares a workspace for a packing operation, potentially involving reporting and callback execution. It takes the workspace, a report object, and a callback function as parameters. The callback is executed asynchronously after preparation is complete. This function is designed for advanced control over the packing process.

```TypeScript
declare function __prepareForPack(workspace: Workspace, __namedParameters: { report: Report }, cb: () => Promise<void>): Promise<void>
```

--------------------------------

### Set Minimum Package Age Gate in Yarn

Source: https://yarnpkg.com/configuration/yarnrc

Configures the minimum age (in minutes) a package version must have, based on its npm registry publish date, to be considered for installation. This helps mitigate risks from newly published, potentially compromised packages.

```yaml
npmMinimalAgeGate: 0
```

--------------------------------

### Create Symbolic Link - linkPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously creates a symbolic link. It takes the existing path and the new path as arguments and returns a Promise that resolves when the link is created.

```typescript
declare function __linkPromise(existingP: PortablePath, newP: PortablePath): Promise<void>;
```

--------------------------------

### File Copying

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Offers methods for copying files, including both promise-based and synchronous operations, with options for the destination and source.

```APIDOC
## `copyFilePromise`

### Description
Asynchronously copies a file from a source path to a destination path.

### Method
`Promise<void>`

### Parameters
- **sourceP** (`PortablePath`) - The path to the source file.
- **destP** (`PortablePath`) - The path to the destination file.
- **flags** (`number`, optional) - Flags to control the copy operation. Defaults to 0.

### Returns
`Promise<void>`

## `copyFileSync`

### Description
Synchronously copies a file from a source path to a destination path.

### Method
`void`

### Parameters
- **sourceP** (`PortablePath`) - The path to the source file.
- **destP** (`PortablePath`) - The path to the destination file.
- **flags** (`number`, optional) - Flags to control the copy operation. Defaults to 0.

### Returns
`void`

## `copyPromise`

### Description
Asynchronously copies a file or directory. Supports advanced options like `baseFs`, `linkStrategy`, `overwrite`, `stableSort`, and `stableTime`.

### Method
`Promise<void>`

### Parameters
- **destination** (`PortablePath`) - The destination path.
- **source** (`PortablePath` or `P2`) - The source path.
- **options** (object, optional) - Configuration options for the copy operation.
  - **baseFs** (`undefined` or `FakeFS<P2>`) - The base file system to use.
  - **linkStrategy** (`null | LinkStrategy<PortablePath>`, optional) - Strategy for handling symbolic links.
  - **overwrite** (`boolean`, optional) - Whether to overwrite existing files.
  - **stableSort** (`boolean`, optional) - Whether to use stable sorting.
  - **stableTime** (`boolean`, optional) - Whether to preserve file timestamps.

### Returns
`Promise<void>`

## `copySync`

### Description
Synchronously copies a file or directory. Supports basic options like `baseFs` and `overwrite`. This method is deprecated and `copyPromise` is recommended.

### Method
`void`

### Parameters
- **destination** (`PortablePath`) - The destination path.
- **source** (`PortablePath` or `P2`) - The source path.
- **options** (object, optional) - Configuration options for the copy operation.
  - **baseFs** (`undefined` or `FakeFS<P2>`) - The base file system to use.
  - **overwrite** (`boolean`, optional) - Whether to overwrite existing files.

### Returns
`void`
```

--------------------------------

### FileFetcher Constructor

Source: https://yarnpkg.com/api/plugin-file/class/FileFetcher

Initializes a new instance of the FileFetcher. This constructor is fundamental for creating FileFetcher objects.

```typescript
new FileFetcher(): FileFetcher
```

--------------------------------

### AddCommand Class Documentation

Source: https://yarnpkg.com/api/plugin-essentials/class/AddCommand

Details about the AddCommand class, its properties, and methods.

```APIDOC
## AddCommand Class

### Description
Represents a command for adding packages to a project in Yarn.

### Hierarchy
* `BaseCommand`
  * `AddCommand`

### Constructors
#### `__constructor()`
* **`new AddCommand()`**: Creates a new instance of the AddCommand.
* **Returns**: `default` (an instance of AddCommand)

### Properties
* **`__cached`** (boolean): Indicates if caching is enabled.
* **`__caret`** (boolean): Controls the use of caret versioning.
* **`__cwd`** (undefined | string): The current working directory.
* **`__dev`** (boolean): Flags if the package should be installed as a dev dependency.
* **`__exact`** (boolean): Enforces exact version matching.
* **`__fixed`** (boolean): Indicates if the version should be fixed.
* **``__interactive`** (undefined | boolean): Enables interactive mode.
* **`__json`** (boolean): Outputs results in JSON format.
* **`__mode`** (undefined | InstallMode): The installation mode.
* **`__optional`** (boolean): Flags if the package is an optional dependency.
* **`__packages`** (string[]): An array of package names to add.
* **`__peer`** (boolean): Flags if the package should be installed as a peer dependency.
* **`__preferDev`** (boolean): Prefers dev dependencies.
* **`__silent`** (undefined | boolean): Suppresses output.
* **`__tilde`** (boolean): Controls the use of tilde versioning.
* **`__paths`** (string[][]): Paths associated with the command.
* **`__usage`** (Usage): The usage information for the command.

### Methods
#### `__execute()`
* **Description**: Executes the add command.
* **Returns**: `Promise<0 | 1>` - A promise that resolves to 0 on success or 1 on failure.

#### `__validateAndExecute()`
* **Description**: Validates the command and then executes it.
* **Returns**: `Promise<number>` - A promise that resolves to a number indicating the result of the validation and execution.
```

--------------------------------

### TypeScript: Hook for after dependency addition in workspace

Source: https://yarnpkg.com/api/plugin-essentials/interface/Hooks

This hook is invoked after a new dependency is added to a workspace. It's triggered by CLI commands like 'yarn add'. Dependencies must be explicitly managed by the CLI to activate this hook; manual manifest edits followed by 'yarn install' will not trigger it.

```typescript
afterWorkspaceDependencyAddition?: (workspace: Workspace, target: Target, descriptor: Descriptor, strategies: Strategy[]) => Promise<void>
```

--------------------------------

### Create Symbolic Link

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/BasePortableFakeFS

Create a symbolic link pointing to a target path.

```APIDOC
## POST /fs/symlink

### Description
Creates a symbolic link at a specified path that points to a target. Supports asynchronous and synchronous creation.

### Method
POST

### Endpoint
/fs/symlink

### Parameters
#### Request Body
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **path** (PortablePath) - Required - The path where the symbolic link will be created.
- **type** (SymlinkType) - Optional - The type of symbolic link to create (e.g., 'dir', 'file', 'junction').

### Request Example
```json
{
  "target": "/path/to/original/file",
  "path": "/path/to/symlink",
  "type": "file"
}
```

### Response
#### Success Response (200)
- **message** (string) - Indicates successful creation of the symbolic link.

#### Response Example
```json
{
  "message": "Symbolic link created successfully."
}
```
```

--------------------------------

### Pass Script Arguments using $0 in Yarn

Source: https://yarnpkg.com/features/scripting

Yarn allows explicit referencing of script arguments using variables like $0, $1, etc. When these variables are used, the automatic appending of arguments is disabled, providing granular control over argument passing. The example shows fetching the latest version tag from a registry.

```json
{
  "scripts": {
    "get-latest": "curl https://registry.yarnpkg.com/$0 | jq .['dist-tags'].latest"
  }
}
```

--------------------------------

### File Open Operations

Source: https://yarnpkg.com/api/yarnpkg-pnpify-utils/class/PortableNodeModulesFS

Provides asynchronous and synchronous methods for opening files with specified flags and modes.

```APIDOC
## POST /fs/openPromise

### Description
Asynchronously opens a file and returns a file descriptor.

### Method
POST

### Endpoint
/fs/openPromise

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **flags** (string) - Required - The flags to use when opening the file (e.g., 'r', 'w', 'a').
- **mode** (number) - Optional - The mode to use when creating the file (only applicable if the file does not exist).

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (200)
- **fileDescriptor** (number) - The file descriptor for the opened file.

#### Response Example
```json
{
  "fileDescriptor": 3
}
```

---

## POST /fs/openSync

### Description
Synchronously opens a file and returns a file descriptor.

### Method
POST

### Endpoint
/fs/openSync

### Parameters
#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **flags** (string) - Required - The flags to use when opening the file (e.g., 'r', 'w', 'a').
- **mode** (number) - Optional - The mode to use when creating the file (only applicable if the file does not exist).

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (200)
- **fileDescriptor** (number) - The file descriptor for the opened file.

#### Response Example
```json
{
  "fileDescriptor": 3
}
```
```

--------------------------------

### VirtualFS Constructor - yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/VirtualFS

Initializes a new instance of the VirtualFS class. It accepts optional named parameters of type VirtualFSOptions. This constructor is fundamental for creating VirtualFS objects to manage virtual file systems.

```typescript
new VirtualFS(__namedParameters?: VirtualFSOptions): VirtualFS
```

--------------------------------

### List All Workspaces

Source: https://context7.com/context7/yarnpkg/llms.txt

Lists all the workspaces defined within the project. This command is helpful for understanding the project's structure and identifying available packages.

```bash
yarn workspaces list
```

--------------------------------

### Add a package using the portal protocol

Source: https://yarnpkg.com/protocol/portal

This command demonstrates how to add a local package, 'my-react-dom', using the 'portal:' protocol. The 'react-dom' package will reference the local 'my-react-dom' folder, making its contents available without copying. This requires the target folder to exist at resolution time.

```bash
yarn add react-dom@portal:./my-react-dom
```

--------------------------------

### PortalFetcher - __fetch

Source: https://yarnpkg.com/api/plugin-link/class/PortalFetcher

Fetches package file data from a specified location based on a locator and fetch options. It can return virtual paths.

```APIDOC
## POST /__fetch

### Description
Fetches package file data from a specified location based on a locator and fetch options. It can return virtual paths.

### Method
POST

### Endpoint
/__fetch

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **locator** (Locator) - Required - The source locator.
- **opts** (FetchOptions) - Required - The fetch options.

### Request Example
```json
{
  "locator": "some_locator_value",
  "opts": {}
}
```

### Response
#### Success Response (200)
- **localPath** (PortablePath) - The local path to the package data.
- **packageFs** (CwdFS | JailFS) - The filesystem object for the package.
- **prefixPath** (PortablePath) - The prefix path for the package.
- **releaseFs** (function | undefined) - A function to release the filesystem resources.

#### Response Example
```json
{
  "localPath": "/path/to/package",
  "packageFs": { /* CwdFS or JailFS object */ },
  "prefixPath": "/prefix",
  "releaseFs": function() { /* ... */ }
}
```
```

--------------------------------

### mkdirpSync API

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipFS

Synchronously creates a directory and its parents if they don't exist. Supports setting permissions and modification times.

```APIDOC
## mkdirpSync

### Description
Synchronously creates a directory and its parents if they do not exist. This function allows for optional `chmod` and `utimes` parameters to set file permissions and modification times.

### Method
* N/A (Synchronous function call)

### Endpoint
* N/A (This is a library function, not a web endpoint)

### Parameters
#### Path Parameters
* None

#### Query Parameters
* None

#### Request Body
* **p** (PortablePath) - Required - The path of the directory to create.
* **__namedParameters** (object) - Optional - An object containing optional parameters.
  * **chmod** (number) - Optional - The permission mode to set for the created directory.
  * **utimes** (Array<string | number | Date>) - Optional - An array containing the access and modification times to set for the directory.

### Request Example
*N/A (This is a function signature, not a request body)*

### Response
#### Success Response
* Returns `undefined | string`.
  * `undefined` if the operation was successful.
  * `string` if an error occurred (e.g., path already exists and is not a directory).

#### Response Example
*N/A (Synchronous function, result is returned directly)*
```

--------------------------------

### ZipOpenFS Constructor - yarnpkg

Source: https://yarnpkg.com/api/yarnpkg-libzip/class/ZipOpenFS

Initializes a new instance of the ZipOpenFS class. It accepts an optional configuration object for options. This constructor is used to create file system interfaces for zip archives.

```typescript
new ZipOpenFS(opts?: ZipOpenFSOptions): ZipOpenFS
```

--------------------------------

### Yarn Plugin System Commands

Source: https://context7.com/context7/yarnpkg/llms.txt

Commands for managing Yarn plugins, including listing, importing from various sources (official, versioned, URL, local), removing, and checking integrity.

```bash
# List available official plugins
yarn plugin list

# Import official plugin
yarn plugin import typescript
yarn plugin import workspace-tools
yarn plugin import interactive-tools

# Import from specific version
yarn plugin import workspace-tools@latest

# Import from URL
yarn plugin import https://example.com/plugin.js

# Build plugin from sources
yarn plugin import from sources @yarnpkg/plugin-exec

# List active plugins
yarn plugin runtime

# Remove plugin
yarn plugin remove @yarnpkg/plugin-typescript

# Check plugin integrity
yarn plugin check

```

--------------------------------

### Create Symbolic Link - linkSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Synchronously creates a symbolic link. It takes the existing path and the new path as arguments. This operation blocks until the link is created.

```typescript
declare function __linkSync(existingP: PortablePath, newP: PortablePath): void;
```

--------------------------------

### Properties of abstractProxiedFS

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/ProxiedFS

This section details the properties available on the abstractProxiedFS class.

```APIDOC
## Properties of abstractProxiedFS

### `__pathUtils`

*   **Type**: `PathUtils<P>`
*   **Description**: Provides utility functions for path manipulation.

### `__accessPromise`

*   **Description**: Asynchronously checks for file access permissions.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to check.
        *   `mode` (number) - Optional - The access mode to check.
*   **Returns**: `Promise<void>`

### `__accessSync`

*   **Description**: Synchronously checks for file access permissions.
*   **Method**: `sync`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to check.
        *   `mode` (number) - Optional - The access mode to check.
*   **Returns**: `void`

### `__appendFilePromise`

*   **Description**: Asynchronously appends content to a file.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (FSPath<P>) - Required - The path to the file.
        *   `content` (string | Uint8Array<ArrayBufferLike>) - Required - The content to append.
        *   `opts` (WriteFileOptions) - Optional - Options for writing the file.
*   **Returns**: `Promise<void>`

### `__appendFileSync`

*   **Description**: Synchronously appends content to a file.
*   **Method**: `sync`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (FSPath<P>) - Required - The path to the file.
        *   `content` (string | Uint8Array<ArrayBufferLike>) - Required - The content to append.
        *   `opts` (WriteFileOptions) - Optional - Options for writing the file.
*   **Returns**: `void`

### `__changeFilePromise`

*   **Description**: Asynchronously changes the content of a file.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to the file.
        *   `content` (Buffer<ArrayBufferLike> | string) - Required - The new content for the file.
        *   `opts` (Partial<{ automaticNewlines: boolean; mode: number }>) - Optional - Options for changing the file content.
*   **Returns**: `Promise<void>`

### `__changeFileSync`

*   **Description**: Synchronously changes the content of a file.
*   **Method**: `sync`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to the file.
        *   `content` (Buffer<ArrayBufferLike> | string) - Required - The new content for the file.
        *   `opts` (Partial<{ automaticNewlines: boolean; mode: number }>) - Optional - Options for changing the file content.
*   **Returns**: `void`

### `__checksumFilePromise`

*   **Description**: Asynchronously calculates the checksum of a file.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `path` (P) - Required - The path to the file.
        *   `__namedParameters` (object) - Optional - Named parameters for checksum calculation.
            *   `algorithm` (string) - Optional - The algorithm to use for checksum calculation (defaults to a standard algorithm).
*   **Returns**: `Promise<string>` - The checksum of the file.

### `__chmodPromise`

*   **Description**: Asynchronously changes the permissions of a file.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to the file.
        *   `mask` (number) - Required - The new permission mask.
*   **Returns**: `Promise<void>`

### `__chmodSync`

*   **Description**: Synchronously changes the permissions of a file.
*   **Method**: `sync`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to the file.
        *   `mask` (number) - Required - The new permission mask.
*   **Returns**: `void`

### `__chownPromise`

*   **Description**: Asynchronously changes the owner and group of a file.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to the file.
        *   `uid` (number) - Required - The new user ID.
        *   `gid` (number) - Required - The new group ID.
*   **Returns**: `Promise<void>`

### `__chownSync`

*   **Description**: Synchronously changes the owner and group of a file.
*   **Method**: `sync`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `p` (P) - Required - The path to the file.
        *   `uid` (number) - Required - The new user ID.
        *   `gid` (number) - Required - The new group ID.
*   **Returns**: `void`

### `__closePromise`

*   **Description**: Asynchronously closes a file descriptor.
*   **Method**: `async`
*   **Endpoint**: Not applicable (method on class)
*   **Parameters**:
    *   **Path Parameters**:
        *   `fd` (number) - Required - The file descriptor to close.
*   **Returns**: `Promise<void>`
```

--------------------------------

### Remove Yarn Plugin by Name

Source: https://yarnpkg.com/cli/plugin/remove

Removes a specified Yarn plugin from the project. The plugin can be installed from the Yarn repository (e.g., '@yarnpkg/plugin-typescript') or a local file. This command targets the '.yarn/plugins' directory and updates the configuration. Shorthands are not permitted; the exact 'name' property of the plugin must be used.

```shell
yarn plugin remove <name>
```

```shell
yarn plugin remove @yarnpkg/plugin-typescript
```

```shell
yarn plugin remove my-local-plugin
```

--------------------------------

### opendirPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CwdFS

Asynchronously opens a directory for reading its entries.

```APIDOC
## opendirPromise

### Description
Asynchronously opens a directory for reading its entries.

### Method
`opendirPromise`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the directory.
- **opts** (object) - Optional - Options for opening the directory.
  - **bufferSize** (number) - Optional - The size of the buffer to use for reading entries.
  - **recursive** (boolean) - Optional - Whether to read entries recursively.

#### Response
#### Success Response (Promise<Dir<PortablePath>>)
Returns a promise that resolves with a directory handle object.
```

--------------------------------

### LinkFetcher Constructor

Source: https://yarnpkg.com/api/plugin-link/class/LinkFetcher

Initializes a new instance of the LinkFetcher. This constructor is part of the LinkFetcher class, which is responsible for fetching package data.

```typescript
new LinkFetcher(): LinkFetcher
```

--------------------------------

### LockfileResolver Constructor

Source: https://yarnpkg.com/api/yarnpkg-core/class/LockfileResolver

Initializes a new instance of the LockfileResolver with a given Resolver.

```APIDOC
## Constructor

### `__constructor`

- **Description**: Initializes a new LockfileResolver.
- **Method**: NEW
- **Endpoint**: N/A

#### Parameters
- **resolver** (Resolver) - Required - The resolver instance to use.

#### Returns
- **LockfileResolver** - A new instance of LockfileResolver.
```

--------------------------------

### Get NPM Authentication Header Hook

Source: https://yarnpkg.com/api/plugin-npm/interface/Hooks

The `getNpmAuthenticationHeader` hook is called when retrieving the authentication header for requests to the npm registry. It enables dynamic querying of CLI credentials for specific registries. It accepts the current header, registry, and configuration details, returning a promise that resolves to the authentication header string or undefined.

```typescript
getNpmAuthenticationHeader?: (currentHeader: undefined | string, registry: string, __namedParameters: { configuration: Configuration; ident?: Ident }) => Promise<undefined | string>
```

--------------------------------

### openPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/interface/MountableFS

Opens a file and returns its file descriptor asynchronously. Returns a Promise that resolves with the file descriptor.

```APIDOC
## openPromise

### Description
Opens a file and returns its file descriptor asynchronously.

### Method
Not applicable (function signature)

### Endpoint
Not applicable (function signature)

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path to the file.
* **flags** (string) - Required - The flags to use for opening the file (e.g., 'r', 'w', 'a').
* **mode** (number) - Optional - The mode to use when creating the file if it does not exist.

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (Promise<number>)
- **number**: The file descriptor for the opened file.

#### Response Example
```json
3
```
```

--------------------------------

### Registering a Yarn Plugin in .yarnrc.yml

Source: https://yarnpkg.com/advanced/plugin-tutorial

Shows how to register a local plugin file by adding its path to the `plugins` array in the `.yarnrc.yml` configuration file. This step is necessary for Yarn to load and recognize the custom plugin.

```yaml
plugins:  
  - ./plugin-hello-world.js  

```

--------------------------------

### prepareExternalProject

Source: https://yarnpkg.com/api/yarnpkg-core/namespace/scriptUtils

Prepares an external project for use within the current Yarn environment, copying necessary files and configurations.

```APIDOC
## prepareExternalProject

### Description
Prepares an external project by copying its contents and configurations to a specified output path. This is typically used when integrating projects managed by different package managers or in specific build scenarios.

### Method
Internal Function (details not specified in original text, assume programmatic call)

### Endpoint
N/A (Internal function)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
*   **cwd** (PortablePath) - Required - The current working directory.
*   **outputPath** (PortablePath) - Required - The path where the external project should be prepared.
*   **__namedParameters** (Object) - Required
    *   **configuration** (Configuration) - Required - The project's configuration object.
    *   **locator** (null | Locator) - Optional - The locator for the external project, defaults to null.
    *   **report** (Report) - Required - The report object for logging progress and errors.
    *   **workspace** (null | string) - Optional - The name of the workspace, defaults to null.

### Request Example
```json
{
  "cwd": "/path/to/current/dir",
  "outputPath": "/path/to/output/dir",
  "__namedParameters": {
    "configuration": {},
    "locator": null,
    "report": {},
    "workspace": null
  }
}
```

### Response
#### Success Response (200)
*   **void** - This function does not return a value upon successful execution.

#### Response Example
(No response body for void function)
```

--------------------------------

### LinkFetcher.__fetch Method

Source: https://yarnpkg.com/api/plugin-link/class/LinkFetcher

Fetches package data for a given locator. It returns a promise that resolves to an object describing the location of the package data on disk, potentially including virtual paths. Dependencies: FetchOptions, Locator, CwdFS, JailFS.

```typescript
__fetch(locator: Locator, opts: FetchOptions): Promise<{ discardFromLookup: boolean; localPath: PortablePath; packageFs: CwdFS; prefixPath: PortablePath; releaseFs: undefined | () => void } | { discardFromLookup: boolean; localPath?: undefined; packageFs: JailFS; prefixPath: PortablePath; releaseFs: undefined | () => void }>
```

--------------------------------

### openPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Asynchronously opens a file and returns a file descriptor. This is an abstract method.

```APIDOC
## openPromise

### Description
Asynchronously opens a file and returns a file descriptor. This is an abstract method.

### Method
Promise<number>

### Endpoint
N/A (Abstract method)

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- None

### Request Example
```json
{
  "example": "Not applicable"
}
```

### Response
#### Success Response (Promise<number>)
- **Type**: Promise<number>
- **Description**: A promise that resolves with the file descriptor.

#### Response Example
```json
{
  "example": "Not applicable"
}
```
```

--------------------------------

### CreateCommand Constructor

Source: https://yarnpkg.com/api/plugin-dlx/class/CreateCommand

Initializes a new instance of the CreateCommand class. This is the default constructor.

```typescript
new CreateCommand(): default
```

--------------------------------

### mkdirpPromise API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NoFS

Asynchronously creates a directory with the given path, supporting optional chmod and utimes configurations.

```APIDOC
## mkdirpPromise API

### Description
Asynchronously creates a directory with the given path. Supports optional chmod and utimes configurations.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirpPromise

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path of the directory to create.

#### Query Parameters
- **__namedParameters** (object) - Optional - Additional options for directory creation.
  - **chmod** (number) - Optional - Permissions to set on the created directory.
  - **utimes** (Array<string | number | Date>) - Optional - User and modification times for the directory.

### Request Example
```json
{
  "p": "/path/to/directory",
  "__namedParameters": {
    "chmod": 448,
    "utimes": ["2023-10-27T10:00:00Z", "2023-10-27T10:00:00Z"]
  }
}
```

### Response
#### Success Response (200)
- **result** (string | undefined) - Returns the path if successful, otherwise undefined.

#### Response Example
```json
{
  "result": "/path/to/directory"
}
```
```

--------------------------------

### symlinkPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/VirtualFS

Asynchronously creates a symbolic link.

```APIDOC
## symlinkPromise /websites/yarnpkg

### Description
Asynchronously creates a symbolic link.

### Method
`symlinkPromise`

### Endpoint
`/websites/yarnpkg` (This is a conceptual representation, as this is a library function, not a REST endpoint)

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **p** (PortablePath) - Required - The path where the symbolic link should be created.
- **type** (SymlinkType) - Optional - The type of symlink to create (e.g., 'file', 'dir').

### Response
#### Success Response (Promise<void>)
A promise that resolves when the symbolic link has been successfully created.

#### Response Example
N/A (void return type within promise)
```

--------------------------------

### abstractFakeFS Methods

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

This section details the various methods available on the abstractFakeFS class, categorized by their function (e.g., file access, manipulation, I/O operations).

```APIDOC
## Methods __

### ____abstract accessPromise

#### Description
  * Asynchronously checks for file accessibility.

#### Method
  * `__accessPromise(p: P, mode?: number): Promise<void>`

#### Parameters
* **p** (`P`) - The path to the file.
* **mode** (`number`, optional) - The mode to check accessibility against.

#### Returns
* `Promise<void>` - A promise that resolves when the access check is successful.
```

```APIDOC
### ____abstract accessSync

#### Description
  * Synchronously checks for file accessibility.

#### Method
  * `__accessSync(p: P, mode?: number): void`

#### Parameters
* **p** (`P`) - The path to the file.
* **mode** (`number`, optional) - The mode to check accessibility against.

#### Returns
* `void`
```

```APIDOC
### ____abstract appendFilePromise

#### Description
  * Asynchronously appends content to a file.

#### Method
  * `__appendFilePromise(p: FSPath<P>, content: string | Uint8Array<ArrayBufferLike>, opts?: WriteFileOptions): Promise<void>`

#### Parameters
* **p** (`FSPath<P>`) - The path to the file.
* **content** (`string | Uint8Array<ArrayBufferLike>`) - The content to append.
* **opts** (`WriteFileOptions`, optional) - Options for writing the file.

#### Returns
* `Promise<void>` - A promise that resolves when the content has been appended.
```

```APIDOC
### ____abstract appendFileSync

#### Description
  * Synchronously appends content to a file.

#### Method
  * `__appendFileSync(p: FSPath<P>, content: string | Uint8Array<ArrayBufferLike>, opts?: WriteFileOptions): void`

#### Parameters
* **p** (`FSPath<P>`) - The path to the file.
* **content** (`string | Uint8Array<ArrayBufferLike>`) - The content to append.
* **opts** (`WriteFileOptions`, optional) - Options for writing the file.

#### Returns
* `void`
```

```APIDOC
### ________changeFilePromise

#### Description
  * Asynchronously changes the content of a file.

#### Method
  * `__changeFilePromise(p: P, content: Buffer<ArrayBufferLike>): Promise<void>`
  * `__changeFilePromise(p: P, content: string, opts?: Partial<{ automaticNewlines: boolean; mode: number }>): Promise<void>`

#### Parameters
* **p** (`P`) - The path to the file.
* **content** (`Buffer<ArrayBufferLike>` or `string`) - The new content for the file.
* **opts** (`Partial<{ automaticNewlines: boolean; mode: number }>`, optional) - Options for changing the file content.

#### Returns
* `Promise<void>` - A promise that resolves when the file content has been changed.
```

```APIDOC
### ________changeFileSync

#### Description
  * Synchronously changes the content of a file.

#### Method
  * `__changeFileSync(p: P, content: Buffer<ArrayBufferLike>): void`
  * `__changeFileSync(p: P, content: string, opts?: Partial<{ automaticNewlines: boolean; mode: number }>): void`

#### Parameters
* **p** (`P`) - The path to the file.
* **content** (`Buffer<ArrayBufferLike>` or `string`) - The new content for the file.
* **opts** (`Partial<{ automaticNewlines: boolean; mode: number }>`, optional) - Options for changing the file content.

#### Returns
* `void`
```

```APIDOC
### ____checksumFilePromise

#### Description
  * Asynchronously calculates a checksum for a file.

#### Method
  * `__checksumFilePromise(path: P, __namedParameters?: { algorithm?: string }): Promise<string>`

#### Parameters
* **path** (`P`) - The path to the file.
* **__namedParameters** (`{ algorithm?: string }`, optional) - Named parameters for checksum calculation.
    * **algorithm** (`string`, optional) - The checksum algorithm to use (e.g., 'md5', 'sha1'). Defaults to a system default.

#### Returns
* `Promise<string>` - A promise that resolves with the file's checksum.
```

```APIDOC
### ____abstract chmodPromise

#### Description
  * Asynchronously changes the permissions of a file.

#### Method
  * `__chmodPromise(p: P, mask: number): Promise<void>`

#### Parameters
* **p** (`P`) - The path to the file.
* **mask** (`number`) - The new permission mask.

#### Returns
* `Promise<void>` - A promise that resolves when the permissions have been changed.
```

```APIDOC
### ____abstract chmodSync

#### Description
  * Synchronously changes the permissions of a file.

#### Method
  * `__chmodSync(p: P, mask: number): void`

#### Parameters
* **p** (`P`) - The path to the file.
* **mask** (`number`) - The new permission mask.

#### Returns
* `void`
```

```APIDOC
### ____abstract chownPromise

#### Description
  * Asynchronously changes the ownership of a file.

#### Method
  * `__chownPromise(p: P, uid: number, gid: number): Promise<void>`

#### Parameters
* **p** (`P`) - The path to the file.
* **uid** (`number`) - The new user ID.
* **gid** (`number`) - The new group ID.

#### Returns
* `Promise<void>` - A promise that resolves when the ownership has been changed.
```

```APIDOC
### ____abstract chownSync

#### Description
  * Synchronously changes the ownership of a file.

#### Method
  * `__chownSync(p: P, uid: number, gid: number): void`

#### Parameters
* **p** (`P`) - The path to the file.
* **uid** (`number`) - The new user ID.
* **gid** (`number`) - The new group ID.

#### Returns
* `void`
```

```APIDOC
### ____abstract closePromise

#### Description
  * Asynchronously closes a file descriptor.

#### Method
  * `__closePromise(fd: number): Promise<void>`

#### Parameters
* **fd** (`number`) - The file descriptor to close.

#### Returns
* `Promise<void>` - A promise that resolves when the file descriptor is closed.
```

--------------------------------

### __makeEmptyArchive

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D

Creates an empty zip archive.

```APIDOC
## POST /__makeEmptyArchive

### Description
Creates and returns an empty zip archive as a Buffer.

### Method
POST

### Endpoint
`/__makeEmptyArchive`

### Parameters
None

### Request Body
None

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **Buffer<ArrayBuffer>** - A buffer representing the empty zip archive.
```

--------------------------------

### File System Operations - Copying

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/VirtualFS

Provides methods for copying files or directories, both asynchronously and synchronously, with various options.

```APIDOC
## Promise-based File Copy

### Description
Copies a file from a source path to a destination path asynchronously.

### Method
`Promise<void>`

### Endpoint
`/copyFilePromise`

### Parameters
- **sourceP** (PortablePath) - The path to the source file.
- **destP** (PortablePath) - The path to the destination file.
- **flags** (number, optional) - Flags for the copy operation. Defaults to 0.

### Response Example
(No response body on success)
```

```APIDOC
## Synchronous File Copy

### Description
Copies a file from a source path to a destination path synchronously.

### Method
`void`

### Endpoint
`/copyFileSync`

### Parameters
- **sourceP** (PortablePath) - The path to the source file.
- **destP** (PortablePath) - The path to the destination file.
- **flags** (number, optional) - Flags for the copy operation. Defaults to 0.

### Response Example
(No response body on success)
```

```APIDOC
## Promise-based Directory/File Copy (Deprecated)

### Description
Copies a file or directory from a source to a destination asynchronously. Prefer `copyPromise`.

### Method
`Promise<void>`

### Endpoint
`/copyPromise`

### Parameters
- **destination** (PortablePath) - The destination path.
- **source** (PortablePath) - The source path.
- **options** (object, optional) - Options for the copy operation:
  - **baseFs** (undefined, optional)
  - **linkStrategy** (null | LinkStrategy<PortablePath>, optional)
  - **overwrite** (boolean, optional)
  - **stableSort** (boolean, optional)
  - **stableTime** (boolean, optional)

### Response Example
(No response body on success)
```

```APIDOC
## Synchronous Directory/File Copy (Deprecated)

### Description
Copies a file or directory from a source to a destination synchronously. Prefer `copySync`.

### Method
`void`

### Endpoint
`/copySync`

### Parameters
- **destination** (PortablePath) - The destination path.
- **source** (PortablePath) - The source path.
- **options** (object, optional) - Options for the copy operation:
  - **baseFs** (undefined, optional)
  - **overwrite** (boolean, optional)

### Response Example
(No response body on success)
```

--------------------------------

### Directory Creation API

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D/class/ZipFS

Provides functions for creating directories recursively, both asynchronously and synchronously.

```APIDOC
## mkdirpPromise / __mkdirpPromise

### Description
Creates a directory recursively. Returns a Promise that resolves to `undefined` or the directory path string.

### Method
`mkdirpPromise(p: PortablePath, __namedParameters?: { chmod?: number; utimes?: [string | number | Date, string | number | Date] }): Promise<undefined | string>

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path of the directory to create.
* **__namedParameters** (object) - Optional - Configuration options.
  * **chmod** (number) - Optional - The permission mode for the directory.
  * **utimes** ([string | number | Date, string | number | Date]) - Optional - The access and modification times for the directory.

### Response
#### Success Response (Promise<undefined | string>)
Resolves with `undefined` or the directory path string upon successful creation.

```

```APIDOC
## mkdirpSync / __mkdirpSync

### Description
Creates a directory recursively synchronously. Returns `undefined` or the directory path string.

### Method
`mkdirpSync(p: PortablePath, __namedParameters?: { chmod?: number; utimes?: [string | number | Date, string | number | Date] }): undefined | string

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path of the directory to create.
* **__namedParameters** (object) - Optional - Configuration options.
  * **chmod** (number) - Optional - The permission mode for the directory.
  * **utimes** ([string | number | Date, string | number | Date]) - Optional - The access and modification times for the directory.

### Response
#### Success Response (undefined | string)
Returns `undefined` or the directory path string upon successful creation.

```

--------------------------------

### Directory Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Provides methods for opening, reading, and listing directory contents.

```APIDOC
## opendirPromise / opendirSync

### Description
Opens a directory for reading its entries asynchronously or synchronously.

### Method
`opendirPromise(p: P, opts?: Partial<{ bufferSize: number; recursive: boolean }>): Promise<Dir<P>>`
`opendirSync(p: P, opts?: Partial<{ bufferSize: number; recursive: boolean }>): Dir<P>`

### Endpoint
N/A (Local filesystem operation)

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the directory.
- **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - Options for opening the directory.
  - **bufferSize** (number) - The buffer size to use.
  - **recursive** (boolean) - Whether to read recursively.

### Request Example
```json
{
  "p": "/path/to/directory"
}
```

### Response
#### Success Response (200)
- **Dir<P>** - A directory handle object.

#### Response Example
```json
{
  "dirHandle": "..."
}
```
```

```APIDOC
## readdirPromise

### Description
Reads the contents of a directory asynchronously.

### Method
`readdirPromise(p: P, opts?: null | Partial<{ recursive: boolean; withFileTypes: boolean }>): Promise<(P | DirentNoPath | Dirent<P>)[]>`

### Endpoint
N/A (Local filesystem operation)

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the directory.
- **opts** (null | Partial<{ recursive: boolean; withFileTypes: boolean }>) - Optional - Options for reading the directory.
  - **recursive** (boolean) - Whether to read recursively.
  - **withFileTypes** (boolean) - Whether to return file type information.

### Request Example
```json
{
  "p": "/path/to/directory",
  "recursive": true,
  "withFileTypes": true
}
```

### Response
#### Success Response (200)
- **(P | DirentNoPath | Dirent<P>)[]** - An array of filenames or directory entry objects.

#### Response Example
```json
{
  "entries": [
    "file1.txt",
    {
      "name": "subdir",
      "isDirectory": true
    }
  ]
}
```
```

--------------------------------

### Fix Git Conflicts in yarn.lock (Yarn v2/v1 Merge)

Source: https://yarnpkg.com/advanced/error-codes

This code snippet demonstrates how to resolve Git conflicts in the `yarn.lock` file when merging branches using different Yarn versions (v2 and v1). It involves checking out the `yarn.lock` file from the 'theirs' branch, followed by running `yarn install` to re-import the lockfile. A `yarn cache clean` can optionally be used to clear unnecessary cache entries. This process may lose v2 resolutions but will trigger Yarn to re-resolve them.

```bash
git checkout --theirs yarn.lock
yarn install
# Optional: yarn cache clean
```

--------------------------------

### PnpLinker Constructor

Source: https://yarnpkg.com/api/plugin-pnp/class/PnpLinker

Initializes a new PnpLinker instance. This constructor is used to create a PnpLinker object, which is the fundamental unit for managing package linking within the Yarn dependency resolution system.

```typescript
new PnpLinker(): PnpLinker
```

--------------------------------

### openPromise

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/JailFS

Asynchronously opens a file and returns a file descriptor.

```APIDOC
## __openPromise

### Description
Asynchronously opens a file and returns a file descriptor.

### Method
POST

### Endpoint
`/open` (Conceptual endpoint for the operation)

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path to the file.
- **flags** (string) - Required - The flags to use when opening the file (e.g., 'r', 'w', 'a').

#### Query Parameters
- **mode** (number) - Optional - The mode to use when creating the file if it does not exist.

### Returns
`Promise<number>` - A promise that resolves with the file descriptor.

```

--------------------------------

### mkdirpSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CwdFS

Synchronously creates a directory, including any necessary parent directories. It can also set file permissions and modification times.

```APIDOC
## mkdirpSync

### Description
Synchronously creates a directory, including any necessary parent directories. It can also set file permissions and modification times.

### Method
`mkdirpSync`

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path of the directory to create.
- **__namedParameters** (object) - Optional - An object containing optional parameters.
  - **chmod** (number) - Optional - The file mode to set on the created directory.
  - **utimes** (Array<string | number | Date>) - Optional - The access and modification times to set on the created directory.

#### Response
#### Success Response (undefined | string)
Returns `undefined` on success, or a string representing an error if an issue occurs.
```

--------------------------------

### opendirPromise and opendirSync - Open a Directory

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/VirtualFS

Asynchronously or synchronously opens a directory at the specified path, returning a directory iterator.

```APIDOC
## opendirPromise and opendirSync

### Description
Asynchronously or synchronously opens a directory at the specified path, returning a directory iterator.

### Method
`opendirPromise` (async), `opendirSync` (sync)

### Parameters
#### Path Parameters
* **p** (PortablePath) - Required - The path to the directory to open.
* **opts** (Partial<{ bufferSize: number; recursive: boolean }>) - Optional - Options for opening the directory.
  * **bufferSize** (number) - Optional - The buffer size to use for reading directory entries.
  * **recursive** (boolean) - Optional - Whether to read the directory recursively.

#### Returns
`Promise<Dir<PortablePath>>` for `opendirPromise`, `Dir<PortablePath>` for `opendirSync` - A directory iterator object.
```

--------------------------------

### openSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/MountFS

Synchronously opens a file and returns a file descriptor.

```APIDOC
## openSync

### Description
Synchronously opens a file given a path and flags, returning a file descriptor.

### Method
POST

### Endpoint
/websites/yarnpkg/openSync

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **p** (PortablePath) - Required - The path to the file.
- **flags** (string) - Required - The flags to use when opening the file (e.g., 'r', 'w', 'a').
- **mode** (number) - Optional - The file mode to use if the file is created.

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r",
  "mode": 438
}
```

### Response
#### Success Response (200)
- **result** (number) - The file descriptor.

#### Response Example
```json
{
  "result": 3
}
```
```

--------------------------------

### SetVersionCommand Constructor

Source: https://yarnpkg.com/api/plugin-essentials/class/SetVersionCommand

Demonstrates the instantiation of the SetVersionCommand class. This constructor is used to create new instances of the command for setting package versions.

```typescript
new SetVersionCommand(): default
```

--------------------------------

### AddCommand Constructor - Yarnpkg

Source: https://yarnpkg.com/api/plugin-essentials/class/AddCommand

Initializes a new instance of the AddCommand class. This constructor sets up the command with default parameters, ready to be configured and executed for adding packages to a project.

```typescript
new AddCommand(): default
```

--------------------------------

### PnpmLinker Constructor

Source: https://yarnpkg.com/api/plugin-pnpm/class/PnpmLinker

Instantiates a new PnpmLinker object. This is the primary way to create an instance of the linker.

```typescript
new PnpmLinker(): PnpmLinker
```

--------------------------------

### Yarn Plugin with Validated Command Options (JavaScript)

Source: https://yarnpkg.com/advanced/plugin-tutorial

Extends a Yarn plugin to include a command with input validation using `clipanion` and `typanion`. The `AdditionCommand` accepts two string options (`a` and `b`) which are validated to be numbers, and then performs addition, printing the result.

```javascript
module.exports = {
  name: `plugin-addition`,
  factory: require => {
    const {BaseCommand} = require(`@yarnpkg/cli`);
    const {Command, Option} = require(`clipanion`);
    const t = require(`typanion`);

    class AdditionCommand extends BaseCommand {
      static paths = [[`addition`]];

      static usage = Command.Usage({
        description: `hello world!`,
        details: `  
          This command will print a nice message.  
        `,
        examples: [[  
          `Add two numbers together`,
          `yarn addition 42 10`,
        ]],
      });

      a = Option.String({validator: t.isNumber()});
      b = Option.String({validator: t.isNumber()});

      async execute() {
        this.context.stdout.write(`${this.a}+${this.b}=${this.a + this.b}\n`);
      }
    }

    return {
      commands: [
        AdditionCommand,
      ],
    };
  },
};

```

--------------------------------

### Make Publish Body (TypeScript)

Source: https://yarnpkg.com/api/plugin-npm/namespace/npmPublishUtils

Constructs the body for a package publish operation. Takes a workspace, buffer of package data, and additional publishing parameters. Returns a Promise that resolves to the publish body object.

```typescript
declare function __makePublishBody(workspace: Workspace, buffer: Buffer<ArrayBufferLike>, __namedParameters: PublishAdditionalParams): Promise<{ _attachments: {}; _id: string; access: string; "dist-tags": {}; name: string; readme: string; versions: {} }>;

```

--------------------------------

### File Operations

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/FakeFS

Provides synchronous and asynchronous methods for opening, reading, and writing files.

```APIDOC
## openSync / openPromise

### Description
Opens a file synchronously or asynchronously.

### Method
`openSync(p: P, flags: string, mode?: number): number`
`openPromise(p: P, flags: string, mode?: number): Promise<number>`

### Endpoint
N/A (Local filesystem operation)

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the file.
- **flags** (string) - Required - Flags to use when opening the file (e.g., 'r', 'w').
- **mode** (number) - Optional - The file mode (permissions).

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "flags": "r"
}
```

### Response
#### Success Response (200)
- **number** - The file descriptor.

#### Response Example
```json
{
  "fileDescriptor": 3
}
```
```

```APIDOC
## readFilePromise / readFileSync

### Description
Reads the content of a file asynchronously or synchronously.

### Method
`readFilePromise(p: FSPath<P>, encoding?: null | BufferEncoding): Promise<string | NonSharedBuffer>`
`readFileSync(p: FSPath<P>, encoding?: null | BufferEncoding): string | NonSharedBuffer`

### Endpoint
N/A (Local filesystem operation)

### Parameters
#### Path Parameters
- **p** (FSPath<P>) - Required - The path to the file.
- **encoding** (null | BufferEncoding) - Optional - The encoding to use for reading the file. If null, returns a buffer.

### Request Example
```json
{
  "p": "/path/to/file.txt",
  "encoding": "utf8"
}
```

### Response
#### Success Response (200)
- **string | NonSharedBuffer** - The content of the file, as a string or a buffer.

#### Response Example
```json
{
  "content": "File content here"
}
```
```

```APIDOC
## readJsonPromise / readJsonSync

### Description
Reads and parses a JSON file asynchronously or synchronously.

### Method
`readJsonPromise(p: P): Promise<any>`
`readJsonSync(p: P): any`

### Endpoint
N/A (Local filesystem operation)

### Parameters
#### Path Parameters
- **p** (P) - Required - The path to the JSON file.

### Request Example
```json
{
  "p": "/path/to/data.json"
}
```

### Response
#### Success Response (200)
- **any** - The parsed JSON object.

#### Response Example
```json
{
  "data": {
    "key": "value"
  }
}
```
```

```APIDOC
## readPromise / readSync

### Description
Reads data from a file descriptor into a buffer asynchronously or synchronously.

### Method
`readPromise(fd: number, buffer: Buffer<ArrayBufferLike>, offset?: number, length?: number, position?: null | number): Promise<number>`
`readSync(fd: number, buffer: Buffer<ArrayBufferLike>, offset?: number, length?: number, position?: null | number): number`

### Endpoint
N/A (Local filesystem operation)

### Parameters
#### Path Parameters
- **fd** (number) - Required - The file descriptor.
- **buffer** (Buffer<ArrayBufferLike>) - Required - The buffer to read data into.
- **offset** (number) - Optional - The offset in the buffer to start reading at.
- **length** (number) - Optional - The number of bytes to read.
- **position** (null | number) - Optional - The position in the file to start reading from.

### Request Example
```json
{
  "fd": 3,
  "buffer": "...", 
  "length": 100
}
```

### Response
#### Success Response (200)
- **number** - The number of bytes read.

#### Response Example
```json
{
  "bytesRead": 100
}
```
```

--------------------------------

### symlinkSync

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/VirtualFS

Synchronously creates a symbolic link.

```APIDOC
## symlinkSync /websites/yarnpkg

### Description
Synchronously creates a symbolic link.

### Method
`symlinkSync`

### Endpoint
`/websites/yarnpkg` (This is a conceptual representation, as this is a library function, not a REST endpoint)

### Parameters
#### Path Parameters
- **target** (PortablePath) - Required - The path the symbolic link should point to.
- **p** (PortablePath) - Required - The path where the symbolic link should be created.
- **type** (SymlinkType) - Optional - The type of symlink to create (e.g., 'file', 'dir').

### Response
#### Success Response (void)
This function does not return a value upon successful completion.

#### Response Example
N/A (void return type)
```

--------------------------------

### Yarn 2 Normalized Shell for Cross-Platform Scripts

Source: https://yarnpkg.com/blog/release/2

This JSON configuration illustrates the use of Yarn 2's normalized shell interpreter for defining scripts. It ensures that scripts like 'redirect' and 'no-cross-env' function consistently across different operating systems (OSX, Windows) by providing a compatible shell environment.

```json
{
  "scripts": {
    "redirect": "node ./something.js > hello.md",
    "no-cross-env": "NODE_ENV=prod webpack"
  }
}
```

--------------------------------

### mkdirSync API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NoFS

Synchronously creates a directory. The current implementation returns `never`.

```APIDOC
## mkdirSync API

### Description
Synchronously creates a directory. Currently returns `never`.

### Method
`never`
```

--------------------------------

### Generate Inline Script for PnP - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-pnp

Generates an inlined script for the Plug'n'Play system. This function takes PnpSettings as input and returns a string representing the script. It's useful for embedding the PnP logic directly into a project's startup files.

```typescript
declare function generateInlinedScript(settings: PnpSettings): string;
```

--------------------------------

### __mountMemoryDrive

Source: https://yarnpkg.com/api/yarnpkg-libzip-%5Bbrowser%5D

Mounts a memory drive with optional source and options.

```APIDOC
## POST /__mountMemoryDrive

### Description
Mounts a memory drive using the provided file system, mount point, and optional source buffer and options.

### Method
POST

### Endpoint
`/__mountMemoryDrive`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **origFs** (object) - Required - The original file system module.
- **mountPoint** (PortablePath) - Required - The path where the memory drive will be mounted.
- **source** (Buffer<ArrayBufferLike> | null) - Optional - The source buffer for the memory drive.
- **opts** (MemoryDriveOpts) - Optional - Options for configuring the memory drive.
```

--------------------------------

### LinkFetcher __fetch API

Source: https://yarnpkg.com/api/plugin-link/class/LinkFetcher

Fetches package data from a given locator and options. It returns an object describing the location of the package data on disk, potentially including virtual paths.

```APIDOC
## GET /fetch

### Description
Fetches package data from a given locator and options. It returns an object describing the location of the package data on disk, potentially including virtual paths.

### Method
GET

### Endpoint
/fetch

### Parameters
#### Query Parameters
- **locator** (Locator) - Required - The source locator.
- **opts** (FetchOptions) - Required - The fetch options.

### Response
#### Success Response (200)
- **discardFromLookup** (boolean) - Indicates if the fetched item should be discarded from lookup.
- **localPath** (PortablePath) - The local path to the fetched package data (if available).
- **packageFs** (CwdFS | JailFS) - The filesystem object for the package.
- **prefixPath** (PortablePath) - The prefix path for the fetched package.
- **releaseFs** (function | undefined) - A function to release the filesystem resources (if applicable).

#### Response Example
```json
{
  "discardFromLookup": true,
  "localPath": "/path/to/package",
  "packageFs": { "type": "CwdFS" },
  "prefixPath": "/prefix"
}
```
```

--------------------------------

### Yarn Command - Basic Usage

Source: https://yarnpkg.com/cli/up

Demonstrates the fundamental usage of the 'yarn up' command to upgrade dependencies. This command is used to update packages to their latest versions across the entire project.

```bash
yarn up ...
```

--------------------------------

### Core Functions

Source: https://yarnpkg.com/api/yarnpkg-core

Provides documentation for core utility functions like parsing and stringifying message names.

```APIDOC
## Functions

### `parseMessageName`

Parses a string into a `MessageName` object.

### Method

```
parseMessageName(messageName: string): MessageName
```

### Parameters

#### Path Parameters

- **messageName** (string) - Required - The string to parse.

### Response

#### Success Response (200)

- **MessageName** - The parsed message name object.

### `stringifyMessageName`

Stringifies a `MessageName` object into a string.

### Method

```
stringifyMessageName(name: number): string
```

### Parameters

#### Path Parameters

- **name** (number) - Required - The message name number to stringify.

### Response

#### Success Response (200)

- **string** - The stringified message name.

```

--------------------------------

### Hydrate PnP File - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-pnp

Asynchronously hydrates the Plug'n'Play API from a file located at a specified path. It requires a FakeFS instance and the resolution path for the 'pnpapi' file, returning a Promise that resolves to the PnpApi object.

```typescript
declare function hydratePnpFile(location: PortablePath, { fakeFs, pnpapiResolution }: { fakeFs: FakeFS<PortablePath>; pnpapiResolution: string }): Promise<PnpApi>;
```

--------------------------------

### mkdirpSync API

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/NoFS

Synchronously creates a directory with the given path, supporting optional chmod and utimes configurations.

```APIDOC
## mkdirpSync API

### Description
Synchronously creates a directory with the given path. Supports optional chmod and utimes configurations.

### Method
POST

### Endpoint
/websites/yarnpkg/mkdirpSync

### Parameters
#### Path Parameters
- **p** (PortablePath) - Required - The path of the directory to create.

#### Query Parameters
- **__namedParameters** (object) - Optional - Additional options for directory creation.
  - **chmod** (number) - Optional - Permissions to set on the created directory.
  - **utimes** (Array<string | number | Date>) - Optional - User and modification times for the directory.

### Request Example
```json
{
  "p": "/path/to/directory",
  "__namedParameters": {
    "chmod": 448,
    "utimes": ["2023-10-27T10:00:00Z", "2023-10-27T10:00:00Z"]
  }
}
```

### Response
#### Success Response (200)
- **result** (string | undefined) - Returns the path if successful, otherwise undefined.

#### Response Example
```json
{
  "result": "/path/to/directory"
}
```
```

--------------------------------

### CwdFS Constructor - TypeScript

Source: https://yarnpkg.com/api/yarnpkg-fslib/class/CwdFS

Initializes a new instance of the CwdFS class. It takes a target path and optional CwdFSOptions. The target path is the base directory for file system operations.

```typescript
new CwdFS(target: PortablePath, __namedParameters?: CwdFSOptions): CwdFS
```

--------------------------------

### TelemetryManager Methods

Source: https://yarnpkg.com/api/yarnpkg-core/class/TelemetryManager

Documentation for the various methods available on the TelemetryManager.

```APIDOC
## TelemetryManager Methods

### Description
Methods for reporting various telemetry events and managing tip displays.

### Methods
#### `__commitTips()`
* **Description**: Prevents the tip from being displayed today, but doesn't actually display it. Used when replacing the tip by something else (like an upgrade prompt).
* **Method**: `__commitTips`
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__commitTips();
```

#### `__reportCommandName(value: string)`
* **Description**: Reports the name of a command that was executed.
* **Method**: `__reportCommandName`
* **Parameters**:
    * **value** (string) - Required - The name of the command.
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportCommandName("install");
```

#### `__reportDependencyCount(count: number)`
* **Description**: Reports the number of dependencies in the project.
* **Method**: `__reportDependencyCount`
* **Parameters**:
    * **count** (number) - Required - The number of dependencies.
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportDependencyCount(150);
```

#### `__reportInstall(nodeLinker: string)`
* **Description**: Reports details about an installation process, including the node linker used.
* **Method**: `__reportInstall`
* **Parameters**:
    * **nodeLinker** (string) - Required - The type of node linker used (e.g., 'pnpm', 'node-modules').
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportInstall("pnpm");
```

#### `__reportPackageExtension(value: string)`
* **Description**: Reports information about a package extension.
* **Method**: `__reportPackageExtension`
* **Parameters**:
    * **value** (string) - Required - The package extension identifier.
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportPackageExtension(".js");
```

#### `__reportPluginName(value: string)`
* **Description**: Reports the name of a plugin that was used.
* **Method**: `__reportPluginName`
* **Parameters**:
    * **value** (string) - Required - The name of the plugin.
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportPluginName("typescript");
```

#### `__reportProject(cwd: PortablePath)`
* **Description**: Reports information about the current project, identified by its current working directory.
* **Method**: `__reportProject`
* **Parameters**:
    * **cwd** (PortablePath) - Required - The portable path to the current working directory.
* **Returns**: `void`
* **Example**: 
```javascript
const currentPath = "/path/to/project";
telemetryManager.__reportProject(currentPath);
```

#### `__reportVersion(value: string)`
* **Description**: Reports a version string, likely related to the project or a specific component.
* **Method**: `__reportVersion`
* **Parameters**:
    * **value** (string) - Required - The version string to report.
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportVersion("1.2.3");
```

#### `__reportWorkspaceCount(count: number)`
* **Description**: Reports the number of workspaces within a project.
* **Method**: `__reportWorkspaceCount`
* **Parameters**:
    * **count** (number) - Required - The number of workspaces.
* **Returns**: `void`
* **Example**: 
```javascript
telemetryManager.__reportWorkspaceCount(5);
```

#### `__selectTip(allTips: (null | Tip)[])`
* **Description**: Selects a tip from a list of available tips.
* **Method**: `__selectTip`
* **Parameters**:
    * **allTips** (Array<null | Tip>) - Required - An array containing possible tips or null values.
* **Returns**: `null | Tip` - The selected tip or null if none is selected.
* **Example**: 
```javascript
const tips = [null, { id: 1, text: "Tip text" }];
const selected = telemetryManager.__selectTip(tips);
console.log(selected);
```
```