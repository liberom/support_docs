### Clone and Setup HCP Terraform Project

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/cloud-state-api

Clones the official HCP Terraform getting started repository and runs a setup script. This is the first step to applying an example configuration.

```bash
git clone https://github.com/hashicorp/tfc-getting-started.git
cd tfc-getting-started
scripts/setup.sh
```

--------------------------------

### Create Terraform Example Directory

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

Creates a new directory structure for Terraform examples and navigates into it. This is a preparatory step for creating Terraform configuration files that will reference the locally installed provider.

```bash
mkdir -p examples/functions/rfc3339_parse && cd "$_"
```

--------------------------------

### Terraform Widget Resource Initialization (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.5.x/deprecations

Provides the necessary setup for the example widget resource, including its type definition, metadata, and constructor function. It ensures the resource is correctly registered with the Terraform plugin framework.

```go
package provider

import (
    "context"

    "github.com/hashicorp/terraform-plugin-framework/resource"
    "github.com/hashicorp/terraform-plugin-framework/resource/schema"
    "github.com/hashicorp/terraform-plugin-framework/types"
)

var _ resource.Resource = (*exampleWidgetResource)(nil)

type exampleWidgetResource struct{}

func NewWidgetResource() resource.Resource {
    return &exampleWidgetResource{}
}

func (e *exampleWidgetResource) Metadata(_ context.Context, req resource.MetadataRequest, resp *resource.MetadataResponse) {
    resp.TypeName = req.ProviderTypeName + "_widget"
}
```

--------------------------------

### Boundary Server Start Log Output (JSON)

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Adev

Example of log output when a Boundary server starts, formatted as JSON. This includes event data, source, and timestamps, useful for observability.

```json
{
  "id": "GypYTtKfJI",
  "source": "https://hashicorp.com/boundary/localmachine/controller+worker",
  "specversion": "1.0",
  "type": "system",
  "data": {
    "version": "v0.1",
    "op": "github.com/hashicorp/boundary/internal/observability/event.(*HclogLoggerAdapter).writeEvent",
    "data": {
      "@original-log-level": "none",
      "@original-log-name": "aws",
      "msg": "configuring client automatic mTLS"
    }
  },
  "datacontentype": "text/plain",
  "time": "2022-09-06T14:14:37.939433-06:00"
}
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/cli/console

This command clones the example repository for the Terraform console tutorial. It downloads the necessary configuration files to your local machine, allowing you to follow along with the guide. Ensure you have Git installed to use this command.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-console
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/cli/init

Clones the 'learn-terraform-init' repository from GitHub. This repository contains example Terraform configuration files used in the tutorial. It requires Git to be installed and configured on your local machine.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-init
```

--------------------------------

### Example Auth Method Environment Variables (CLI)

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Adev_variants=boundary-deploy%3Ahcp

Provides an example of setting the Client ID, Client Secret, and Issuer URL environment variables with specific values for testing or demonstration purposes.

```bash
export CLIENT_ID="zaxJLTZh3n14WqSQ7qQ9onuIVRDaZdzz"; \
export CLIENT_SECRET="t35c9NNw1aZ8haEKFJbJF0lauMOSp5UNPovUJXo8Ea2sPZAR1DszEowX-6-lg-Xr"; \
export ISSUER_URL="dev-1sdl8c0z.us.auth0.com"
```

```bash
export CLIENT_ID="zaxJLTZh3n14WqSQ7qQ9onuIVRDaZdzz"; \
export CLIENT_SECRET="t35c9NNw1aZ8haEKFJbJF0lauMOSp5UNPovUJXo8Ea2sPZAR1DszEowX-6-lg-Xr"; \
export ISSUER_URL="dev-1sdl8c0z.us.auth0.com"
```

--------------------------------

### Example Output of Configuration Upload

Source: https://developer.hashicorp.com/terraform/cloud-docs/stacks/create

This is an example of the output received after successfully uploading stack configuration files. It provides the Stack ID, Configuration ID, Sequence Number, and a URL to view the run details.

```text
Uploading stack configuration...

Configuration for Stack (id: 'st-MLQLSJVrdtGazA4aU') was uploaded
Configuration ID: stc-6fSRO81hOzTPKMM
Sequence Number: 1

See run at: <URL>
```

--------------------------------

### Terraform Enterprise Docker Compose Volumes Definition

Source: https://developer.hashicorp.com/terraform/enterprise/v202404-1/flexible-deployments/install/docker/install

Defines named volumes used by Terraform Enterprise in a Docker Compose setup. This example specifies a volume for caching.

```yaml
volumes:
  terraform-enterprise-cache:
```

--------------------------------

### Start Terraform Provider Server (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/provider-servers

This Go program implements the `main` function to start a Terraform provider server. It utilizes the `providerserver` package and requires the `context` and `log` packages. The `ServeOpts` configure the provider's address and protocol version.

```go
package main

import (
    "context"
    "flag"
    "log"

    "github.com/example-namespace/terraform-provider-example/internal/provider"
    "github.com/hashicorp/terraform-plugin-framework/providerserver"
)

var (
    // Example version string that can be overwritten by a release process
    version string = "dev"
)

func main() {
    opts := providerserver.ServeOpts{
        // TODO: Update this string with the published name of your provider.
        Address: "registry.terraform.io/example-namespace/example",
    }

    err := providerserver.Serve(context.Background(), provider.New(version), opts)

    if err != nil {
        log.Fatal(err.Error())
    }
}
```

--------------------------------

### Start Minio Docker Container

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/requirements/data-storage/minio-setup-guide

Starts a Minio Docker container in detached mode, mounting a volume for configuration persistence. This command is intended for testing and not production use.

```docker
docker run \
  -d \
  --name minio \
  -v /run/minio/config:/root/.minio \
  minio/minio:latest \
  -- \
  server /data
```

--------------------------------

### Implement Create Function for Example Widget (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/deprecations

Handles the creation of the 'example_widget' resource. It checks for the presence of either 'existing_attribute' or 'new_attribute' and adds the appropriate attribute to the provider API call. Returns an error if neither attribute is configured.

```go
func resourceExampleWidgetCreate(d *schema.ResourceData, meta interface{}) error {
    // ... other logic ...

    existingAttribute, existingAttributeOk := d.GetOk("existing_attribute")
    newAttribute, newAttributeOk := d.GetOk("new_attribute")
    if !existingAttributeOk && !newAttributeOk {
        return errors.New("one of existing_attribute or new_attribute must be configured")
    }
    if existingAttributeOk {
        // add existingAttribute to provider create API call
    } else {
        // add newAttribute to provider create API call
    }

    // ... other logic ...
    return resourceExampleWidgetRead(d, meta)
}
```

--------------------------------

### Group Guides Using Subcategories in Directory Structure

Source: https://developer.hashicorp.com/terraform/registry/providers/docs

This example demonstrates how to structure guide documentation to use subcategories. By placing guides within subdirectories under 'guides/' and using the 'subcategory' field in their frontmatter, related guides can be grouped into separate top-level sections in the navigation.

```directory
docs/
    index.md
    guides/
        authenticating-basic.md
        authenticating-oauth.md
        setup.md
    actions/
        stop_instance.md
    data-sources/
        instance.md
    ephemeral-resources/
        auth_token.md
    functions/
        parse_instance_id.md
    list-resources/
        instance.md
    resources/
        instance.md
```

--------------------------------

### Register Resources in Framework Provider

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/resources

This Go code demonstrates how to register resources within a Framework provider. It returns a slice of functions, each creating an instance of a resource type, such as `exampleResource`. This replaces the `ResourcesMap` used in SDKv2.

```go
func (p *exampleProvider) Resources(_ context.Context) []func() resource.Resource {
    return []func() resource.Resource{
        func() resource.Resource {
            return &exampleResource{}
        },
        /* ... */
    }
}

```

--------------------------------

### Navigate to Terraform Example Directory

Source: https://developer.hashicorp.com/terraform/tutorials/use-case/vsphere-provider/vmware-environment%3Avcsim_variants=vmware-environment%3Avcsim

After cloning the example repository, this command navigates you into the `learn-terraform-vsphere` directory. This directory contains all the Packer and Terraform files needed for the tutorial.

```bash
cd learn-terraform-vsphere
```

--------------------------------

### Get Minio Secret Key

Source: https://developer.hashicorp.com/terraform/enterprise/v202501-1/replicated/requirements/data-storage/minio-setup-guide

Extracts the secret key from the Minio configuration file using 'jq'. This key is required for authenticating with the Minio instance.

```shell
jq -r .credential.secretKey /var/run/minio/config/config.json
```

--------------------------------

### Navigate to Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/cli/plan

Changes the current directory to the cloned 'learn-terraform-plan' repository. This is a necessary step before reviewing the configuration files.

```bash
cd learn-terraform-plan
```

--------------------------------

### Get Minio Access Key

Source: https://developer.hashicorp.com/terraform/enterprise/v202501-1/replicated/requirements/data-storage/minio-setup-guide

Extracts the access key from the Minio configuration file using 'jq'. This key is required for authenticating with the Minio instance.

```shell
jq -r .credential.accessKey /var/run/minio/config/config.json
```

--------------------------------

### Cloning Example Repository with Git

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/helm-provider

Shows the git clone command used to download the example repository for the tutorial. This repository contains configurations for deploying applications using Helm on Kubernetes.

```shell
$ git clone https://github.com/hashicorp-education/learn-terraform-helm
$ cd learn-terraform-helm
```

--------------------------------

### Wait for Minio Configuration File

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/requirements/data-storage/minio-setup-guide

Polls the filesystem until the Minio configuration file is created. This is used to ensure Minio has started correctly before proceeding with other operations.

```bash
while [ ! -e /var/run/minio/config/config.json ]; do
  sleep 3
done
```

--------------------------------

### Example Policy Using module() and module_paths

Source: https://developer.hashicorp.com/terraform/enterprise/v202503-1/policy-enforcement/import-reference/tfplan

This example demonstrates how to iterate through all modules using `module_paths` and the `module()` function to find resources of a specific type that have pending changes. It utilizes the `tfplan` import for accessing plan data.

```hcl
import "tfplan"

main = rule { tfplan.module(["foo"]).resources.null_resource.foo[0].applied.triggers.foo is "bar" }
```

```hcl
import "tfplan"

main = rule { tfplan.module(["foo"]).resources.null_resource.foo[0].applied.triggers.foo is "bar" }
```

```hcl
import "tfplan"

main = rule { tfplan.module_paths contains ["foo"] }
```

```hcl
import "tfplan"

main = rule { tfplan.module_paths contains ["foo"] }
```

--------------------------------

### Enable Terraform Enterprise Systemd Service

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/flexible-deployments/install/docker/install

Command to enable and start the Terraform Enterprise systemd service. This ensures the service runs automatically on system startup.

```bash
systemctl enable --now terraform-enterprise
```

--------------------------------

### Initialize Terraform Cloud Backend (Migration Example)

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/remote-backends

This output shows the process of initializing Terraform Cloud and migrating the state from a local backend. It prompts the user to confirm whether to copy the existing state to the new Terraform Cloud workspace. This is a crucial step when moving from local state management to a remote, collaborative backend.

```bash
Initializing Terraform Cloud...
Migrating from backend "local" to Terraform Cloud.
Do you wish to proceed?
              As part of migrating to Terraform Cloud, Terraform can optionally copy your
              current workspace state to the configured Terraform Cloud workspace.

              Answer "yes" to copy the latest state snapshot to the configured
              Terraform Cloud workspace.

              Answer "no" to ignore the existing state and just activate the configured
              Terraform Cloud workspace with its existing state, if any.

              Should Terraform migrate your existing state?

              Enter a value:
yes
Initializing provider plugins...
            - Reusing previous version of hashicorp/random from the dependency lock file
- Using previously-installed hashicorp/random v3.4.3
Terraform Cloud has been successfully initialized!

```

--------------------------------

### Systemd Pod Service Definition for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/v202312-1/flexible-deployments/install/podman/install

This is an example of an autogenerated systemd service file for a Terraform Enterprise pod. It defines unit properties, service configurations including start and stop commands, and installation targets.

```systemd
# autogenerated by Podman 4.6.1

[Unit]
Description=Podman pod-terraform-enterprise.service
Documentation=man:podman-generate-systemd(1)
Wants=network-online.target
After=network-online.target
RequiresMountsFor=/run/containers/storage
Wants=container-terraform-enterprise-terraform-enterprise.service
Before=container-terraform-enterprise-terraform-enterprise.service

[Service]
Environment=PODMAN_SYSTEMD_UNIT=%n
Restart=on-failure
TimeoutStopSec=70
ExecStart=/usr/bin/podman start 3085f37511a9-infra
ExecStop=/usr/bin/podman stop  \
          -t 10 3085f37511a9-infra
ExecStopPost=/usr/bin/podman stop  \
          -t 10 3085f37511a9-infra
PIDFile=/run/containers/storage/overlay-containers/e3bd0deae7ecfa4ebab25b0a876faaf23806ac1f81385ba621c1d22d426e45d0/userdata/conmon.pid
Type=forking

[Install]
WantedBy=default.target
```

--------------------------------

### Setup Go and Run Tests in GitHub Actions

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.26.x/testing/acceptance-tests

This snippet demonstrates setting up the Go environment to version 1.19 and then executing Go tests with verbose output and coverage reporting using the `go test` command.

```yaml
- uses: actions/checkout@v3
- uses: actions/setup-go@v3
    with:
      go-version: '1.19'
- run: go test -v -cover ./...
```

--------------------------------

### Clone Example Repository using Git

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/versions

This command clones the example GitHub repository for the Terraform versions tutorial. It requires the git CLI to be installed locally. The repository contains a complete Terraform configuration for deploying an example web application on AWS.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-versions
```

--------------------------------

### Get Minio Access and Secret Keys

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-1/requirements/data-storage/minio-setup-guide

Retrieves the access key and secret key from the Minio configuration file using jq. These credentials are required for authenticating with the Minio instance.

```shell
jq -r .credential.accessKey /var/run/minio/config/config.json
jq -r .credential.secretKey /var/run/minio/config/config.json
```

--------------------------------

### Main Application Entrypoint in Go

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/stacks

Sets up the Terraform CDK application, instantiates the VPCStack, and then the BackendStack, passing the VPC ID from the VPCStack to the BackendStack. Finally, it synthesizes the Terraform configuration.

```go
import (
    "github.com/aws/constructs-go/constructs/v10"
    "github.com/aws/jsii-runtime-go"
    "github.com/hashicorp/terraform-cdk-go/cdktf"
    aws "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/aws/provider"
    "github.com/hashicorp/terraform-cdk/examples/go/documentation/myconstructs"
)

// ... (VPCStack and BackendStack definitions)

func main() {
    app := cdktf.NewApp(nil)

    origin := NewVPCStack(app, "origin-stack", nil)
    NewBackendStack(app, "target-stack", BackendStackConfig{
        Region:      *origin.Region,
        VPCId:       origin.VPC.Id,
        DockerImage: "org/my-image:latest",
    })

    app.Synth()
}
```

--------------------------------

### Packer Build Output Example

Source: https://developer.hashicorp.com/terraform/tutorials/virtual-machine/vsphere-provider/vmware-environment%3Avsphere

An example of the output from the 'packer build' command, indicating the start of the VM creation process on vSphere.

```bash
vsphere-iso.this: output will be in this color.

==> vsphere-iso.this: Creating VM...

```

--------------------------------

### Custom Agent Dockerfile for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This Dockerfile demonstrates how to build a custom agent image for Terraform Enterprise. It starts from a base `hashicorp/tfc-agent` image, installs sudo, and configures it to allow the `tfc-agent` user to run apt-get commands. This enables adding custom tools to the agent environment.

```dockerfile
FROM hashicorp/tfc-agent:latest

# Switch the to root user in order to perform privileged actions such as
# installing software.
USER root

# Install sudo. The container runs as a non-root user, but people may rely on
# the ability to apt-get install things.
RUN apt-get -y install sudo

# Permit tfc-agent to use sudo apt-get commands.
RUN echo 'tfc-agent ALL=NOPASSWD: /usr/bin/apt-get , /usr/bin/apt' >> /etc/sudoers.d/50-tfc-agent

# Switch back to the tfc-agent user as needed by Terraform agents.
USER tfc-agent

```

```dockerfile
FROM hashicorp/tfc-agent:latest

# Switch the to root user in order to perform privileged actions such as
# installing software.
USER root

# Install sudo. The container runs as a non-root user, but people may rely on
# the ability to apt-get install things.
RUN apt-get -y install sudo

# Permit tfc-agent to use sudo apt-get commands.
RUN echo 'tfc-agent ALL=NOPASSWD: /usr/bin/apt-get , /usr/bin/apt' >> /etc/sudoers.d/50-tfc-agent

# Switch back to the tfc-agent user as needed by Terraform agents.
USER tfc-agent

```

--------------------------------

### Get GOBIN Path (Mac/Linux)

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This command retrieves the GOBIN path, which is where Go installs your binaries. This path is necessary for configuring local provider installations in Terraform.

```shell
$ go env GOBIN
/Users/<Username>/go/bin
```

--------------------------------

### Navigate to Order Examples Directory

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-resource-delete

Changes the current directory to the 'examples/order' directory, which contains a sample Terraform configuration for the HashiCups provider. This is a prerequisite for performing destroy operations.

```bash
cd examples/order
```

--------------------------------

### Systemd Service for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/flexible-deployments/install/docker/install

This systemd service file configures `systemd` to manage the Terraform Enterprise Docker Compose service. It ensures the service starts on boot and can be stopped gracefully.

```systemd
[Unit]
Description=Terraform Enterprise Service
Requires=docker.service
After=docker.service network.target

[Service]
Type=oneshot
RemainAfterExit=yes
WorkingDirectory=/etc/terraform-enterprise
ExecStart=/usr/local/bin/docker compose up -d
ExecStop=/usr/local/bin/docker compose down
TimeoutStartSec=0

[Install]
WantedBy=multi-user.target
```

--------------------------------

### Navigate to Example Repository Directory

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/dynamic-credentials-vault

After cloning the repository, this command changes the current directory to the root of the cloned example repository, allowing you to access its contents.

```bash
cd learn-terraform-vault-backed-dynamic-credentials
```

--------------------------------

### Get Minio Instance IP Address

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-1/requirements/data-storage/minio-setup-guide

Uses Docker inspect to retrieve the IP address of the running Minio container. This IP is needed to configure external services to connect to Minio.

```shell
docker inspect minio | jq -r .[0].NetworkSettings.IPAddress
```

--------------------------------

### Customize Terraform Agent Docker Image (Dockerfile)

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/v1.10.x/agents

This Dockerfile example shows how to create a customized Terraform agent Docker image. It starts from the official `hashicorp/tfc-agent:latest` image and then switches to the root user to install `sudo` using `apt-get`. This is useful for workflows that require elevated privileges within the container.

```dockerfile
FROM hashicorp/tfc-agent:latest

USER root

# Install sudo. The container runs as a non-root user, but people may rely on
# the ability to apt-get install things.
RUN apt-get -y install sudo

```

--------------------------------

### Configure Provider Example (Terraform)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This Terraform configuration block defines the 'exampletime' provider. It's a minimal example used to demonstrate provider configuration and is often placed in `examples/provider/provider.tf` for documentation generation.

```hcl
provider "exampletime" { }

```

--------------------------------

### Example CA Certificate Bundle (PEM Encoded)

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This snippet shows the format for a Certificate Authority (CA) bundle, which includes root and intermediate certificates. Certificates must be PEM encoded text. This is crucial for Terraform Enterprise to trust certificates from private CAs.

```text
-----BEGIN CERTIFICATE-----
MIIFtTCCA52gAwIBAgIIYY3HhjsBggUwDQYJKoZIhvcNAQEFBQAwRDEWMBQGA1UE
AwwNQUNFRElDT00gUm9vdDEMMAoGA1UECwwDUEtJMQ8wDQYDVQQKDAZFRElDT00x
CzAJBgNVBAYTAkVTMB4XDTA4MDQxODE2MjQyMloXDTI4MDQxMzE2MjQyMlowRDEW
MBQGA1UEAwwNQUNFRElDT00gUm9vdDEMMAoGA1UECwwDUEtJMQ8wDQYDVQQKDAZF
....
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIB5zCCAY6gAwIBAgIUNJADaMM+URJrPMdoIeeAs9/CEt4wCgYIKoZIzj0EAwIw
UjELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAkNBMRYwFAYDVQQHEw1TYW4gRnJhbmNp
    c2NvMR4wHAYDVQQDExVoYXNoaWNvcnAuZW5naW5lZXJpbmcwHhcNMTgwMjI4MDYx
....
-----END CERTIFICATE-----
```

```text
-----BEGIN CERTIFICATE-----
MIIFtTCCA52gAwIBAgIIYY3HhjsBggUwDQYJKoZIhvcNAQEFBQAwRDEWMBQGA1UE
AwwNQUNFRElDT00gUm9vdDEMMAoGA1UECwwDUEtJMQ8wDQYDVQQKDAZFRElDT00x
CzAJBgNVBAYTAkVTMB4XDTA4MDQxODE2MjQyMloXDTI4MDQxMzE2MjQyMlowRDEW
MBQGA1UEAwwNQUNFRElDT00gUm9vdDEMMAoGA1UECwwDUEtJMQ8wDQYDVQQKDAZF
....
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIB5zCCAY6gAwIBAgIUNJADaMM+URJrPMdoIeeAs9/CEt4wCgYIKoZIzj0EAwIw
UjELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAkNBMRYwFAYDVQQHEw1TYW4gRnJhbmNp
    c2NvMR4wHAYDVQQDExVoYXNoaWNvcnAuZW5naW5lZXJpbmcwHhcNMTgwMjI4MDYx
....
-----END CERTIFICATE-----
```

--------------------------------

### Example Log Inspection for Licensing Service

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/flexible-deployments/troubleshooting

This example demonstrates inspecting the logs for the `tfe:licensing` service. It shows both informational messages about initialization and an error message indicating a database connection failure.

```bash
$ cat /var/log/terraform-enterprise/licensing.log
{"@level":"info","@message":"initializing database","@module":"tfe-licensing","@timestamp":"2023-05-10T20:46:26.379084Z"}
{"@level":"error","@message":"error opening database connection","@module":"tfe-licensing","@timestamp":"2023-05-10T20:46:26.399064Z","error":"failed to connect to `host=/var/run/postgresql user=terraform-enterprise database=`: server error (FATAL: role \"terraform-enterprise\" does not exist (SQLSTATE 28000))"}
```

--------------------------------

### Copy Credentials File

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/kubernetes-operator

Copies the example credentials file to a new file named 'credentials'. This is a common step to prepare configuration files.

```bash
$ cp credentials.example credentials
```

--------------------------------

### Install jq and Terraform Installer

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/admin/infrastructure/automated-recovery

This script installs the 'jq' utility and the Terraform installer. 'jq' is used for parsing JSON output, and the installer sets up the necessary Terraform environment. It uses apt-get for package management and curl to download the installer.

```bash
apt-get update
apt-get install -y jq
curl https://install.terraform.io/ptfe/stable | bash -s fast-timeouts
```

--------------------------------

### Prepare Terraform Enterprise Installer - Airgapped Mode

Source: https://developer.hashicorp.com/terraform/enterprise/v202411-1/install/interactive/installer

Steps to prepare for an airgapped installation of Terraform Enterprise, which does not require internet access during installation. This involves pre-installing Docker and downloading necessary files.

```bash
wget --content-disposition "<url>"
```

```bash
tar xzf replicated.tar.gz
```

--------------------------------

### Terraform Example Changelog Structure

Source: https://developer.hashicorp.com/terraform/plugin/best-practices/versioning

Provides a complete example of a Terraform changelog, demonstrating the correct application of version headers, categories, entry formats, and ordering rules. This serves as a practical guide for contributors.

```markdown
## 1.0.0 (Unreleased)

BREAKING CHANGES:

* Resource `network_port` has been removed [GH-1]

FEATURES:

* **New Resource:** `cluster` [GH-43]

IMPROVEMENTS:

* resource/load_balancer: Add `ATTRIBUTE` argument (support X new functionality) [GH-12]
* resource/subnet: Now better [GH-22, GH-32]

## 0.2.0 (Month Day, Year)

FEATURES:

...

```

--------------------------------

### Run Terraform Enterprise Installer - Airgapped Mode

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

Steps for performing an airgapped installation of Terraform Enterprise, suitable for environments without internet access. This involves downloading an `.airgap` file and the installer bootstrapper, then executing the installation script.

```bash
wget --content-disposition "<url>"
```

```bash
tar xzf replicated.tar.gz
sudo ./install.sh airgap
```

--------------------------------

### Define Example Terraform Resource Configuration (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/best-practices/testing

This Go function generates a Terraform configuration string for the 'example_widget' resource. It takes a name as input and returns a formatted string suitable for use in Terraform tests. Dependencies include the standard Go 'fmt' package.

```go
func testAccExampleResource(name string) string {
    return fmt.Sprintf(
        "resource \"example_widget\" \"foo\" {\n  active = true\n  name = \"%s\"\n}", name)
}

```

--------------------------------

### Navigate to Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/azure/azure-virtual-machine-scale-sets

Navigates the user into the cloned Terraform example repository directory. This is a prerequisite step before reviewing or applying the Terraform configuration.

```bash
$ cd learn-terraform-azure-scale-sets

```

```bash
$ cd learn-terraform-azure-scale-sets

```

--------------------------------

### Install Terraform Modules

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-use

This snippet shows the commands 'terraform init' or 'terraform get' used to install modules. It illustrates the resulting directory structure after modules are installed, including local module symlinks.

```bash
.terraform/modules/
├── ec2_instances
├── modules.json
└── vpc


```

--------------------------------

### Configure Remote Backend with CloudBackend - C#

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/remote-backends

This C# code example demonstrates the setup of a Terraform stack and the configuration of a remote backend using CloudBackend. It facilitates the migration of state from local storage to a remote location like Terraform Cloud.

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using System.Linq;
using Constructs;
using HashiCorp.Cdktf;

namespace Examples
{
    class LocalBackendStack : TerraformStack
    {
        public LocalBackendStack(Construct scope, string name) : base(scope, name)
        {
            new TerraformOutput(this, "dns-server", new TerraformOutputConfig
            {
                Value = "local"
            });
        }
    }
}

App app = new App();
LocalBackendStack stack = new LocalBackendStack(app, "local-to-cloud-backend");
new CloudBackend(stack, new CloudBackendConfig {
    Hostname = "app.terraform.io",
    Organization = "company",
    Workspaces = new NamedCloudWorkspace("my-app-prod")
});

app.Synth();

```

--------------------------------

### Navigate to Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/cli/plan_utm_offer=ARTICLE_PAGE

Changes the current directory to the cloned 'learn-terraform-plan' repository. This is a necessary step before reviewing the configuration or running Terraform commands.

```bash
# Navigate to the cloned repository
$ cd learn-terraform-plan

```

--------------------------------

### GET /github-app/installations

Source: https://developer.hashicorp.com/terraform/enterprise/v202404-1/api-docs/github-app-installations

Lists all GitHub App installations that the current user has access to within GitHub. You can filter the results by organization name or installation ID.

```APIDOC
## GET /github-app/installations

### Description
Lists GitHub App installations available to the current User. Queries only return GitHub App Installations that the current user has access to within GitHub.

### Method
GET

### Endpoint
/github-app/installations

### Parameters
#### Query Parameters
- **filter[name]** (string) - Optional - If present, returns a list of available GitHub App installations that match the GitHub organization or login.
- **filter[installation_id]** (integer) - Optional - If present, returns a list of available GitHub App installations that match the installation id within GitHub. (Not HCP Terraform)

### Request Example
```bash
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installations
```

### Response
#### Success Response (200)
- **data** (array) - An array of GitHub App installation objects.
  - **id** (string) - The unique identifier for the GitHub App installation.
  - **type** (string) - The resource type, always 'github-app-installations'.
  - **attributes** (object) - Contains the details of the installation.
    - **name** (string) - The name of the GitHub organization or user.
    - **installation-id** (integer) - The GitHub installation ID.
    - **icon-url** (string) - The URL of the GitHub App icon.
    - **installation-type** (string) - The type of installation (e.g., 'User', 'Organization').
    - **installation-url** (string) - The URL to manage the installation in GitHub.

#### Response Example
```json
{
    "data": [
        {
            "id": "ghain-BYrbNeGQ8nAzKouu",
            "type": "github-app-installations",
            "attributes": {
                "name": "octouser",
                "installation-id": 54810170,
                "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
                "installation-type": "User",
                "installation-url": "https://github.com/settings/installations/54810170"
            }
        }
    ]
}
```
```

--------------------------------

### Terraform Enterprise Traffic Hairpinning Configuration

Source: https://developer.hashicorp.com/terraform/enterprise/v202407-1/flexible-deployments/install/docker/install

Example Docker Compose configuration snippet demonstrating how to simulate traffic hairpinning in Terraform Enterprise Flexible Deployment Options. This is achieved by setting the TFE_RUN_PIPELINE_DOCKER_EXTRA_HOSTS environment variable to map the TFE hostname to the instance's IP address.

```yaml
name: terraform-enterprise
services:
  tfe:
    image: images.releases.hashicorp.com/hashicorp/terraform-enterprise:<vYYYYMM-#>
    environment:
      TFE_HOSTNAME: "terraform.example.com"
      TFE_RUN_PIPELINE_DOCKER_EXTRA_HOSTS: "terraform.example.com:<IP.ADDRESS.OF.INSTANCE>"
```

--------------------------------

### Implement Simplified Create Function (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/deprecations

Handles the creation of the 'example_widget' resource with the simplified schema. It retrieves the required 'new_attribute' and adds it to the provider API call. This function assumes 'new_attribute' is always present due to schema definition.

```go
func resourceExampleWidgetCreate(d *schema.ResourceData, meta interface{}) error {
    // ... other logic ...

    newAttribute := d.Get("new_attribute").(string)
    // add attribute to provider create API call

    // ... other logic ...
    return resourceExampleWidgetRead(d, meta)
}
```

--------------------------------

### Clone Example Repository - Git

Source: https://developer.hashicorp.com/terraform/tutorials/0-13/dependencies

Clones the example repository for the Terraform dependencies tutorial. This repository contains the necessary configuration files to follow along with the guide.

```shell
git clone https://github.com/hashicorp-education/learn-terraform-dependencies

```

--------------------------------

### GET /github-app/installation/:gh_app_installation_id

Source: https://developer.hashicorp.com/terraform/enterprise/v202404-1/api-docs/github-app-installations

Retrieves details for a specific GitHub App installation using its ID.

```APIDOC
## GET /github-app/installation/:gh_app_installation_id

### Description
Retrieves details for a specific GitHub App installation.

### Method
GET

### Endpoint
/github-app/installation/:gh_app_installation_id

### Parameters
#### Path Parameters
- **gh_app_installation_id** (string) - Required - The HCP Terraform ID of the GitHub App installation.

### Request Example
```bash
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installation/ghain-R4xmKTaxnhLFioUq
```

### Response
#### Success Response (200)
- **data** (object) - The GitHub App installation object.
  - **id** (string) - The unique identifier for the GitHub App installation.
  - **type** (string) - The resource type, always 'github-app-installations'.
  - **attributes** (object) - Contains the details of the installation.
    - **name** (string) - The name of the GitHub organization or user.
    - **installation-id** (integer) - The GitHub installation ID.
    - **icon-url** (string) - The URL of the GitHub App icon.
    - **installation-type** (string) - The type of installation (e.g., 'User', 'Organization').
    - **installation-url** (string) - The URL to manage the installation in GitHub.

#### Response Example
```json
{
    "data": {
        "id": "ghain-R4xmKTaxnhLFioUq",
        "type": "github-app-installations",
        "attributes": {
            "name": "octouser",
            "installation-id": 54810170,
            "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
            "installation-type": "User",
            "installation-url": "https://github.com/settings/installations/54810170"
        }
    }
}
```
```

--------------------------------

### Implement Multiple Data Sources using Service Grouping (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.10.x/providers

This example shows how to manage a large number of data sources by grouping them within different services. The provider's `DataSources` method aggregates data sources from various service packages (e.g., `servicex`, `servicey`) using Go's variadic slice expansion (`...`). This approach enhances code organization and maintainability for providers with many data sources.

```go
package provider

import (
	"context"
	"github.com/hashicorp/terraform-plugin-framework/datasource"
	"your_module/internal/servicex"
	"your_module/internal/servicey"
)

type Provider interface {
	DataSources(ctx context.Context) []func() datasource.DataSource
}

// ExampleCloudProvider is a placeholder for a concrete provider implementation.
type ExampleCloudProvider struct {}

// With the provider.Provider implementation
func (p *ExampleCloudProvider) DataSources(_ context.Context) []func() datasource.DataSource {
	return []func() datasource.DataSource{
		servicex.DataSources...,
		servicey.DataSources...
	}
}

// With the servicex implementation
package servicex

import (
	"github.com/hashicorp/terraform-plugin-framework/datasource"
)

var DataSources = []func() datasource.DataSource {
	NewThingDataSource,
	NewWidgetDataSource,
}

func NewThingDataSource() datasource.DataSource {
	return &ThingDataSource{}
}

type ThingDataSource struct {}

func NewWidgetDataSource() datasource.DataSource {
	return &WidgetDataSource{}
}

type WidgetDataSource struct {}

```

--------------------------------

### Navigate to Example Directory (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/bulk-migrate-hcp

Changes the current directory to the 'example' directory. This is a common shell command used to navigate the file system.

```shell
$ cd ../example
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/cli/plan

Clones the 'learn-terraform-plan' repository from GitHub to your local machine. This repository contains example Terraform configurations for the tutorial.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-plan
```

--------------------------------

### Airgapped Installer Configuration (JSON)

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

Example JSON configuration for an automated airgapped installation of Terraform Enterprise. This extends the online configuration by adding a path to the airgap package bundle.

```json
{
  "DaemonAuthenticationType": "password",
  "DaemonAuthenticationPassword": "your-password-here",
  "TlsBootstrapType": "server-path",
  "TlsBootstrapHostname": "server.company.com",
  "TlsBootstrapCert": "/etc/server.crt",
  "TlsBootstrapKey": "/etc/server.key",
  "BypassPreflightChecks": true,
  "ImportSettingsFrom": "/path/to/settings.json",
  "LicenseFileLocation": "/path/to/license.rli",
  "LicenseBootstrapAirgapPackagePath": "/path/to/bundle.airgap"
}
```

--------------------------------

### Apply Terraform Configuration and View Outputs

Source: https://developer.hashicorp.com/terraform/tutorials/cli/outputs

This example demonstrates applying a Terraform configuration and shows the expected output, including newly defined variables like 'lb_url', 'vpc_id', and 'web_server_count'. It prompts the user to confirm the changes.

```bash
$ terraform apply
random_string.lb_id: Refreshing state... [id=5YI]
module.vpc.aws_vpc.this[0]: Refreshing state... [id=vpc-004c2d1ba7394b3d6]

## ...

Plan: 0 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + lb_url           = "http://lb-5YI-project-alpha-dev-2144336064.us-east-1.elb.amazonaws.com/"
  + vpc_id           = "vpc-004c2d1ba7394b3d6"
  + web_server_count = 4

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes


Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

lb_url = "http://lb-5YI-project-alpha-dev-2144336064.us-east-1.elb.amazonaws.com/"
vpc_id = "vpc-004c2d1ba7394b3d6"
web_server_count = 4
```

--------------------------------

### Clone Example Configuration Repository

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/kubernetes-crd-faas

Clones the GitHub repository containing the example Terraform configuration for managing Kubernetes custom resources. This is the first step to get the necessary files for the tutorial.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-k8s-crd-openfaas
```

--------------------------------

### Run Terraform Enterprise Installer - Airgapped Mode

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/interactive/installer

Installs Terraform Enterprise using a local installer bootstrapper file in an airgapped environment. This method is for instances without internet access. It requires the installer to be extracted and run with `sudo`. Docker must be pre-installed or specified.

```bash
tar xzf replicated.tar.gz
sudo ./install.sh airgap docker-version=20.10.17
```

```bash
tar xzf replicated.tar.gz
sudo ./install.sh airgap
```

--------------------------------

### Navigate to Order Examples Directory (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This command changes the current directory to the `examples/order` directory. This location contains Terraform configurations for testing the order resource's lifecycle, including deletion.

```bash
$ cd examples/order

```

--------------------------------

### Install Kind using Chocolatey (Windows)

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/kubernetes-provider/kubernetes%3Akind_variants=kubernetes%3Akind

Installs the 'kind' tool on Windows using the Chocolatey package manager. This is a prerequisite for creating local Kubernetes clusters for the tutorial.

```shell
$ choco install kind

```

--------------------------------

### Configure HTTP Proxy during Terraform Enterprise Installation

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This command sets the HTTP proxy for the Terraform Enterprise installer. It's used when the installation requires outbound HTTP/HTTPS connections through a proxy server. The proxy address is provided as a URL.

```bash
./install.sh http-proxy=http://internal.mycompany.com:8080
```

--------------------------------

### Start Terraform Protocol Version 6 Provider Server (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v0.10.x/provider-servers

This Go program implements the startup logic for a Terraform provider server using protocol version 6. It requires the 'context', 'flag', 'log', and specific 'terraform-plugin-framework' packages. The main function initializes provider server options and calls the 'providerserver.Serve' function.

```go
package main

import (
    "context"
    "flag"
    "log"

    "github.com/example-namespace/terraform-provider-example/internal/provider"
    "github.com/hashicorp/terraform-plugin-framework/providerserver"
)

var (
    // Example version string that can be overwritten by a release process
    version string = "dev"
)

func main() {
    opts := providerserver.ServeOpts{
        // TODO: Update this string with the published name of your provider.
        Address: "registry.terraform.io/example-namespace/example",
    }

    err := providerserver.Serve(context.Background(), provider.New(version), opts)

    if err != nil {
        log.Fatal(err.Error())
    }
}

```

--------------------------------

### Clone Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/automation/validation-enforcement

Clones the example Terraform repository for the tutorial. This command downloads the necessary configuration files to your local machine.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-validation-enforcement

```

--------------------------------

### Clone Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/packer

Clones the example repository for the tutorial. This repository contains the necessary configuration files for both Packer and Terraform.

```bash
git clone -b packer https://github.com/hashicorp-education/learn-terraform-provisioning

```

--------------------------------

### Register Resource in SDKv2 Provider

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/resources

This code snippet shows how to register a resource named 'example_resource' within an SDKv2 provider by mapping it to the `exampleResource()` function. This is a common pattern in SDKv2 for defining available resources.

```go
func New() (*schema.Provider, error) {
    return &schema.Provider {
        ResourcesMap: map[string]*schema.Resource {
            "example_resource": exampleResource(),
            /* ... */

```

--------------------------------

### Install Terraform Enterprise with Proxy

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/interactive/installer

This command installs Terraform Enterprise while specifying a Docker version and an HTTP proxy for outbound connections. Ensure the Docker version is compatible with your Terraform Enterprise version.

```bash
./install.sh docker-version=20.10.17 http-proxy=http://internal.mycompany.com:8080
```

--------------------------------

### Get GOBIN Path (Mac/Windows)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-provider

This command retrieves the GOBIN path, which is where Go installs your binaries. This path is necessary for configuring local provider installations in Terraform. The output may vary based on your Go environment variable configuration.

```bash
$ go env GOBIN
/Users/<Username>/go/bin
```

```bash
$ go env GOBIN
/Users/<Username>/go/bin
```

--------------------------------

### Enable and Start Terraform Enterprise (Docker)

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated-migration

This command enables the Terraform Enterprise service to start on boot and immediately starts the service. This is used after migrating to the Docker Compose-based installation.

```bash
$ systemctl enable --now terraform-enterprise

```

--------------------------------

### Navigate to Terraform Examples Directory

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This command changes the current directory to the 'examples/order' directory, which contains a sample Terraform configuration for testing the provider.

```shell
$ cd examples/order
```

--------------------------------

### Build and Install Terraform Provider Binary

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This command compiles your provider code and installs the binary into your Go bin directory. This makes the provider available for Terraform to use.

```shell
$ go install
```

--------------------------------

### Clone Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-eks-deferred

Clones the example repository for the tutorial. Replace 'USER' with your GitHub username. This sets up the necessary files for the HCP Terraform Stack.

```bash
git clone https://github.com/USER/learn-terraform-stacks-eks-deferred

```

--------------------------------

### Main Application Entry Point in Go (CDKTF)

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/stacks

The main function demonstrates the usage of `NewSourceStack`, `NewDependencyStack`, and `NewNestedDependencyStack` to set up a CDKTF application with multiple stacks and their dependencies. It initializes the app, creates source stacks, a dependency stack, a nested dependency stack, and synthesizes the configuration.

```go
func main() {
    app := cdktf.NewApp(nil)

    stackA := NewSourceStack(app, "stack-a")
    stackB := NewSourceStack(app, "stack-b")

    stackC := NewDependencyStack(app, "stack-c", []*SourceStack{&stackA, &stackB})

    NewNestedDependencyStack(app, "stack-d", *stackC.AllResources)

    app.Synth()
}
```

--------------------------------

### Terraform Provision Start Message Example (JSON)

Source: https://developer.hashicorp.com/terraform/internals/v1.1.x/machine-readable-ui

This JSON message indicates the beginning of a provisioning process for a specific Terraform resource. It includes information about the resource and the type of provisioner being used, such as 'local-exec'.

```json
{
  "@level": "info",
  "@message": "null_resource.none[0]: Provisioning with 'local-exec'வுகளை...",
  "@module": "terraform.ui",
  "@timestamp": "2021-03-26T16:38:43.997431-04:00",
  "hook": {
    "resource": {
      "addr": "null_resource.none[0]",
      "module": "",
      "resource": "null_resource.none[0]",
      "implied_provider": "null",
      "resource_type": "null_resource",
      "resource_name": "none",
      "resource_key": 0
    },
    "provisioner": "local-exec"
  },
  "type": "provision_start"
}
```

--------------------------------

### Online Installer Configuration (JSON)

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

Example JSON configuration for an automated online installation of Terraform Enterprise. This requires specifying authentication details, TLS settings, and paths to application settings and license files.

```json
{
  "DaemonAuthenticationType": "password",
  "DaemonAuthenticationPassword": "your-password-here",
  "TlsBootstrapType": "server-path",
  "TlsBootstrapHostname": "server.company.com",
  "TlsBootstrapCert": "/etc/server.crt",
  "TlsBootstrapKey": "/etc/server.key",
  "BypassPreflightChecks": true,
  "ImportSettingsFrom": "/path/to/settings.json",
  "LicenseFileLocation": "/path/to/license.rli"
}
```

--------------------------------

### Terraform Initialization Process

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

This snippet details the output of the `terraform init` command, including backend initialization, provider plugin discovery and installation (specifically hashicorp/boundary v1.0.5), and the creation of a lock file to ensure consistent provider selections.

```bash
Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/boundary versions matching "1.0.5"...
- Installing hashicorp/boundary v1.0.5...
- Installed hashicorp/boundary v1.0.5 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

... 
... truncated output ...
... 

```

--------------------------------

### Run Terraform Enterprise Installer - Online Mode

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/interactive/installer

Executes the Terraform Enterprise installer script directly from the internet. This method is suitable for instances with internet access. It requires `curl` and `sudo` to run. The `docker-version` can be specified.

```bash
curl https://install.terraform.io/ptfe/stable | sudo bash docker-version=20.10.17
```

```bash
curl https://install.terraform.io/ptfe/stable > install.sh docker-version=20.10.17
sudo bash install.sh
```

```bash
sudo bash install.sh no-docker
```

--------------------------------

### Navigate to Examples Directory (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This command changes the current directory to the `examples/coffees` directory. This is where you'll find sample Terraform configuration files to test the data source functionality.

```bash
$ cd examples/coffees

```

--------------------------------

### Clone Terraform Example Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/cli/resource-targeting

Clones the example Terraform configuration repository from GitHub. This is the first step to setting up the infrastructure.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-resource-targeting
```

--------------------------------

### Clone Example Repository with Git

Source: https://developer.hashicorp.com/terraform/tutorials/applications/multicloud-kubernetes

This command clones the example repository containing the necessary Terraform configurations for the multi-cloud Kubernetes deployment. Ensure you have Git installed.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-multicloud-kubernetes
```

--------------------------------

### Navigate to Tutorial Directory

Source: https://developer.hashicorp.com/terraform/tutorials/networking/consul-terraform-sync

After cloning the repository, change into the directory that contains the complete configuration files for this tutorial. This directory holds all Terraform configurations and provisioning scripts.

```bash
cd learn-consul-cts-intro/self-managed
```

--------------------------------

### Download Installer Script Locally - Online Mode

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/install/interactive/installer

Downloads the Terraform Enterprise installer script to the local machine for inspection before execution. This allows users to review the script's contents prior to running it with administrative privileges. It's a safer approach for understanding the installation process.

```bash
curl https://install.terraform.io/ptfe/stable > install.sh
```

--------------------------------

### Download Terraform Enterprise Installer - Online Mode

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/interactive/installer

Downloads the Terraform Enterprise installer script locally for inspection before execution. This allows reviewing the script's content. Requires `curl` and `sudo` for execution. The `docker-version` can be specified.

```bash
curl https://install.terraform.io/ptfe/stable > install.sh docker-version=20.10.17
sudo bash install.sh
```

--------------------------------

### Initialize Terraform Project

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/helm-provider

Initializes the Terraform working directory. This command downloads necessary provider plugins, initializes backend configuration, and prepares the project for use. It's a crucial first step before running 'terraform plan' or 'terraform apply'.

```bash
$ terraform init
Initializing modules...
Downloading registry.terraform.io/terraform-aws-modules/eks/aws 19.5.1 for eks...
- eks in .terraform/modules/eks
- eks.eks_managed_node_group in .terraform/modules/eks/modules/eks-managed-node-group
- eks.eks_managed_node_group.user_data in .terraform/modules/eks/modules/_user_data
- eks.fargate_profile in .terraform/modules/eks/modules/fargate-profile
Downloading registry.terraform.io/terraform-aws-modules/kms/aws 1.1.0 for eks.kms...
- eks.kms in .terraform/modules/eks.kms
- eks.self_managed_node_group in .terraform/modules/eks/modules/self-managed-node-group
- eks.self_managed_node_group.user_data in .terraform/modules/eks/modules/_user_data
Downloading registry.terraform.io/terraform-aws-modules/vpc/aws 3.19.0 for vpc...
- vpc in .terraform/modules/vpc

Initializing the backend...

Initializing provider plugins...
##...
Terraform has been successfully initialized!
##...
```

--------------------------------

### Clone Example Terraform Configuration Repository

Source: https://developer.hashicorp.com/terraform/tutorials/policy/sentinel-policy

This command clones the example code repository which contains a Sentinel policy and mock import data for testing. Ensure you have Git installed and configured.

```bash
git clone https://github.com/hashicorp-education/learn-sentinel-write-policy

```

--------------------------------

### Navigate to Terraform Example Directory

Source: https://developer.hashicorp.com/terraform/tutorials/0-13/count_utm_offer=ARTICLE_PAGE

Changes the current directory to the cloned Terraform example repository. This is a necessary step before applying Terraform configurations.

```bash
cd learn-terraform-count

```

--------------------------------

### Main Application Entry Point in Go

Source: https://developer.hashicorp.com/terraform/cdktf/v0.17.x/concepts/stacks

Initializes the Terraform CDK app, creates an origin VPC stack, and then a target backend stack using outputs from the origin stack. Finally, it synthesizes the Terraform configuration. Dependencies include the previously defined VPCStack and BackendStack functions.

```go
import (
    "github.com/aws/constructs-go/constructs/v10"
    "github.com/aws/jsii-runtime-go"
    "github.com/hashicorp/terraform-cdk-go/cdktf"
    aws "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/aws/provider"
    "github.com/hashicorp/terraform-cdk/examples/go/documentation/myconstructs"
)

// ... (VPCStack and NewVPCStack definitions)

// ... (BackendStackConfig and NewBackendStack definitions)

func main() {
    app := cdktf.NewApp(nil)

    origin := NewVPCStack(app, "origin-stack", nil)
    NewBackendStack(app, "target-stack", BackendStackConfig{
        Region:      *origin.Region,
        VPCId:       origin.VPC.Id,
        DockerImage: "org/my-image:latest",
    })

    app.Synth()
}
```

--------------------------------

### Start and Enable Docker Compose Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/v202505-1/deploy/replicated-migration

Command to start the Terraform Enterprise service managed by Docker Compose and enable it to start on system boot. This command initiates the new Docker-based installation.

```bash
$ systemctl enable --now terraform-enterprise

```

```bash
$ systemctl enable --now terraform-enterprise

```

--------------------------------

### Run Terraform Enterprise Installer - Online Mode

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

Instructions for installing Terraform Enterprise in online mode, which requires internet access. The installer can be executed directly or inspected locally before running. Red Hat Enterprise Linux users may need to specify 'no-docker' if Docker is pre-installed.

```bash
curl https://install.terraform.io/ptfe/stable | sudo bash
```

```bash
curl https://install.terraform.io/ptfe/stable > install.sh
sudo bash install.sh
```

```bash
curl https://install.terraform.io/ptfe/stable > install.sh
sudo bash install.sh no-docker
```

--------------------------------

### Initialize Packer and Install Plugins

Source: https://developer.hashicorp.com/terraform/tutorials/provision/multicloud

This command initializes the Packer template in the current directory, automatically downloading and installing the necessary plugins (e.g., for AWS and Azure) as defined in the template's 'required_plugins' block. These plugins extend Packer's functionality for interacting with cloud providers.

```bash
$ packer init .
Installed plugin github.com/hashicorp/azure v1.0.6 in "…"
Installed plugin github.com/hashicorp/amazon v1.0.9 in "…"
```

--------------------------------

### Terraform Initialization Output

Source: https://developer.hashicorp.com/terraform/cdktf/v0.20.x/concepts/resources

This output shows the initialization process for Terraform, including backend setup and provider plugin installation. It confirms the successful initialization of the Terraform working directory, preparing it for commands like `terraform plan` and `terraform apply`.

```terraform
ts-import  Initializing the backend...
ts-import  Initializing provider plugins...
ts-import  - Reusing previous version of hashicorp/aws from the dependency lock file
ts-import  - Using previously-installed hashicorp/aws v5.5.0
```

--------------------------------

### Serve Terraform Provider with `providerserver.Serve`

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

The `main` function serves your provider so that Terraform can communicate with it over RPC. This example uses a specially formatted provider address for local testing and development. It takes a background context, a new provider instance, and options as input, and logs any fatal errors.

```go
err := providerserver.Serve(context.Background(), provider.New(version), opts)

    if err != nil {
        log.Fatal(err.Error())
    }
}
```

--------------------------------

### Directory Structure for Podman Installation

Source: https://developer.hashicorp.com/terraform/enterprise/v202402-2/flexible-deployments/install/podman/install

This example shows the expected directory structure for storing TLS certificates and the Kubernetes pod specification file when installing Terraform Enterprise on Podman. The `certs` directory should contain `cert.pem`, `key.pem`, and `bundle.pem`.

```shell
certs
├── cert.pem
├── key.pem
└── bundle.pem
```

--------------------------------

### Destroy-Time Provisioner Example (Terraform)

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/resources/provisioners

This example demonstrates a destroy-time provisioner using the 'local-exec' provisioner in Terraform. It specifies `when = destroy` to ensure the command runs during resource destruction.

```terraform
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    when    = destroy
    command = "echo 'Destroy-time provisioner'"
  }
}

```

--------------------------------

### Apply Terraform Configuration and Verify Output

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/data-sources/terraform-workflow%3Acommunity

This section demonstrates the command to apply Terraform configurations and shows example output, including the creation of resources and the final output values like `lb_url` and `web_instance_count`. It also includes a `curl` command to test the deployed application.

```Bash
$ terraform apply
##...

Plan: 10 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + lb_url             = (known after apply)
  + web_instance_count = 4

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

##...

Apply complete! Resources: 10 added, 0 changed, 0 destroyed.

Outputs:

lb_url = "http://lb-DOf-tutorial-example-1971328425.us-west-2.elb.amazonaws.com/"
web_instance_count = 4


```

```Bash
$ curl $(terraform output -raw lb_url)
<html><body><div>Hello, world!</div></body></html>

```

--------------------------------

### Install Terraform Enterprise with Proxy and Exclusions

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/interactive/installer

This command installs Terraform Enterprise with a specific Docker version, an HTTP proxy, and a list of hostnames that should bypass the proxy. This is useful for services like S3 or internal VCS that require direct access.

```bash
./install.sh docker-version=20.10.17 additional-no-proxy=s3.amazonaws.com,internal-vcs.mycompany.com,example.com
```

--------------------------------

### Apply Terraform Configuration and Verify Output

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/data-sources/terraform-workflow%3Acommunity_variants=terraform-workflow%3Acommunity

This section shows the command-line execution of `terraform apply` to provision resources and the subsequent output, including the load balancer URL and web instance count. It also demonstrates how to use `terraform output` to retrieve values.

```Bash
$ terraform apply
##...

Plan: 10 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + lb_url             = (known after apply)
  + web_instance_count = 4

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

##...

Apply complete! Resources: 10 added, 0 changed, 0 destroyed.

Outputs:

lb_url = "http://lb-DOf-tutorial-example-1971328425.us-west-2.elb.amazonaws.com/"
web_instance_count = 4

```

```Bash
$ curl $(terraform output -raw lb_url)
<html><body><div>Hello, world!</div></body></html>

```

--------------------------------

### Download Airgap File with Wget

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/install/interactive/installer

Demonstrates how to download the `.airgap` file for an airgapped Terraform Enterprise installation using `wget`. The `--content-disposition` flag is crucial to ensure the downloaded file retains its correct extension, which is necessary for the installation process.

```bash
wget --content-disposition "<url>"
```

--------------------------------

### Initialize and Apply Production Environment

Source: https://developer.hashicorp.com/terraform/tutorials/modules/organize-configuration

Navigates to the production directory, initializes Terraform, and applies the configuration. This deploys the infrastructure for the production environment, ensuring it's separate from development.

```bash
$ cd ../prod
$ terraform init
$ terraform apply
```

--------------------------------

### Monitor Terraform Enterprise Installation Status

Source: https://developer.hashicorp.com/terraform/enterprise/v202209-1/install/automated/active-active

Use the replicatedctl app status command to monitor the installation progress of Terraform Enterprise. This command provides details about the application's state, desired state, and transition status. Installation is complete when 'isTransitioning' is false and 'State' is 'started'.

```shell
replicatedctl app status

```

```json
[
    {
        "AppID": "218b78fa2bd6f0044c6a1010a51d5852",
        "Sequence": 504,
        "PatchSequence": 0,
        "State": "starting",
        "DesiredState": "started",
        "IsCancellable": false,
        "IsTransitioning": true,
        "LastModifiedAt": "2021-01-07T21:15:11.650385151Z"
    }
]

```

--------------------------------

### Navigate to Provider Verification Directory

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-provider-configure

Change the current directory to the provider installation verification example. This is a common first step in many Terraform examples to isolate testing.

```bash
cd examples/provider-install-verification
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/module-object-attributes

This command clones the example repository containing Terraform configuration for an AWS S3 bucket. Ensure you have Git installed to execute this command.

```bash
#!/bin/bash
git clone https://github.com/hashicorp-education/learn-terraform-module-object-attributes

```

--------------------------------

### Create Workspace (with Key/Value Tags)

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/api-docs/workspaces

This example demonstrates creating a workspace with key/value tags.

```APIDOC
## POST /api/v2/workspaces

### Description
Creates a new HCP Terraform workspace with specified key/value tags.

### Method
POST

### Endpoint
/api/v2/workspaces

### Parameters
#### Request Body
- **data** (object) - Required - The workspace object.
  - **attributes** (object) - Required - Workspace attributes.
    - **name** (string) - Required - The name of the workspace.
  - **type** (string) - Required - Must be "workspaces".
  - **relationships** (object) - Optional - Relationships to other resources.
    - **tag-bindings** (object) - Optional - Tag bindings for the workspace.
      - **data** (array) - Required - An array of tag binding objects.
        - **type** (string) - Required - Must be "tag-bindings".
        - **attributes** (object) - Required - Tag attributes.
          - **key** (string) - Required - The tag key.
          - **value** (string) - Required - The tag value.

### Request Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-1"
    },
    "type": "workspaces",
    "relationships": {
      "tag-bindings": {
          "data": [{
            "type": "tag-bindings",
            "attributes": { "key": "env", "value": "test"}
          }]
      }
    }
  }
}
```

### Response
#### Success Response (201 Created)
- **data** (object) - The created workspace object.
  - **attributes** (object) - Workspace attributes.
    - **name** (string) - The name of the workspace.
  - **type** (string) - The type of the resource, "workspaces".
  - **relationships** (object) - Relationships to other resources.
    - **tag-bindings** (object) - Tag bindings for the workspace.
      - **data** (array) - An array of tag binding objects.
        - **type** (string) - The type of the resource, "tag-bindings".
        - **attributes** (object) - Tag attributes.
          - **key** (string) - The tag key.
          - **value** (string) - The tag value.

#### Response Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-1"
    },
    "type": "workspaces",
    "relationships": {
      "tag-bindings": {
          "data": [{
            "type": "tag-bindings",
            "attributes": { "key": "env", "value": "test"}
          }]
      }
    }
  }
}
```
```

--------------------------------

### Terraform substr Function Examples

Source: https://developer.hashicorp.com/terraform/language/v1.12.x/functions/substr

Demonstrates the basic usage of the `substr` function to extract substrings. The examples show how to specify the starting position and the number of characters to include.

```Terraform
substr("hello world", 1, 4)
# Output: ello
```

```Terraform
substr("hello world", 6, 10)
# Output: world
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/cli/state-import

Clones the example Terraform repository from GitHub. This is the first step to setting up the project.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-import
```

--------------------------------

### Start and Enable Docker Compose Terraform Enterprise Service

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated-migration

This command enables the Terraform Enterprise service to start automatically on system boot and starts it immediately. This is part of the migration process to switch from Replicated to a Docker Compose-managed installation.

```shell
$ systemctl enable --now terraform-enterprise
```

--------------------------------

### Minimal Terraform Module Structure Example

Source: https://developer.hashicorp.com/terraform/language/v1.12.x/modules/develop/structure

This example demonstrates the minimal recommended file and directory structure for a Terraform module. It includes the essential files for a functional module, serving as a starting point for module development.

```tree
tree minimal-module/
.
├── README.md
├── main.tf
├── variables.tf
├── outputs.tf


```

```tree
tree minimal-module/
.
├── README.md
├── main.tf
├── variables.tf
├── outputs.tf


```

--------------------------------

### Run Terraform Enterprise Installer - Online Mode (Bash)

Source: https://developer.hashicorp.com/terraform/enterprise/v202209-2/install/interactive/installer

Executes the Terraform Enterprise installer script directly from the internet using curl and bash. This method is suitable for instances with internet access. It allows for direct execution or local inspection before running. Requires Docker to be installed separately on RedHat Enterprise Linux.

```bash
curl https://install.terraform.io/ptfe/stable | sudo bash docker-version=20.10.17
```

```bash
curl https://install.terraform.io/ptfe/stable > install.sh docker-version=20.10.17
sudo bash install.sh
```

```bash
curl https://install.terraform.io/ptfe/stable > install.sh docker-version=20.10.17
sudo bash install.sh no-docker
```

--------------------------------

### Apply Terraform Configuration and View Outputs

Source: https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-outputs

This example shows the process of applying a Terraform configuration and the subsequent output display. It includes the refresh and plan phases, confirmation prompt, and the final output of the 'ip' variable after a successful apply. This demonstrates how Terraform presents defined outputs upon completion of resource provisioning.

```bash
$ terraform apply
google_compute_network.vpc_network: Refreshing state... [id=projects/testing-project/global/networks/terraform-network]
google_compute_instance.vm_instance: Refreshing state... [id=projects/testing-project/zones/us-central1-c/instances/terraform-instance]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:

Terraform will perform the following actions:

Plan: 0 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + ip = "10.128.0.3"

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes


Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

ip = "10.128.0.3"
```

--------------------------------

### Retrieve State Version with Related Resources

Source: https://developer.hashicorp.com/terraform/enterprise/v202311-1/api-docs/state-versions

This example demonstrates fetching a state version and including related resources such as the creator ('created_by') and the run that generated it ('run'). This provides more context about the state version in a single request.

```bash
curl \
  --header "Authorization: Bearer $TF_API_TOKEN" \
  "https://app.terraform.io/api/v2/state-versions/sv-g4rqST72reoHMM5a?include=created_by,run"
```

--------------------------------

### Install Local Terraform Module

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-create

Installs local Terraform modules using the 'terraform get' command. This command downloads and prepares modules for use in your configuration. It's often run as part of 'terraform init'.

```bash
$ terraform get
```

--------------------------------

### Clone Terraform Example Configuration Repository

Source: https://developer.hashicorp.com/terraform/tutorials/aws/lambda-api-gateway

This command clones the GitHub repository containing the example Terraform configuration for deploying AWS Lambda and API Gateway. Ensure you have Git installed to use this command.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-lambda-api-gateway
```

--------------------------------

### New Terraform Provider Directory Structure Example

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/upgrade-guides/0-13

Illustrates the new hierarchical directory structure for manually installed Terraform providers in version 0.13. This structure is required for Terraform to recognize local provider installations.

```plaintext
registry.terraform.io/hashicorp/google/2.0.0/linux_amd64/terraform-provider-google_v2.0.0
```

--------------------------------

### Running Boundary Compose Services

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

This snippet shows the command used to start Boundary services defined in a compose file and the subsequent output indicating the creation of various containerized services like postgres, mysql, redis, and controller.

```bash
$ ./run all
~/learn-boundary-target-aware-workers/compose ~/learn-boundary-target-aware-workers
Creating boundary_postgres_1 ... done
Creating boundary_mysql_1    ... done
Creating boundary_db_1       ... done
Creating boundary_redis_1    ... done
Creating boundary_db-init_1  ... done
Creating boundary_controller_1 ... done
Creating boundary_worker1_1    ... done
Creating boundary_worker2_1    ... done
~/Projects/hashicorp/tutorial-repos/learn-boundary-target-aware-workers-test
~/Projects/hashicorp/tutorial-repos/learn-boundary-target-aware-workers-test/terraform ~/Projects/hashicorp/   tutorial-repos/learn-boundary-target-aware-workers-test

```

--------------------------------

### Start Terraform Enterprise (Replicated) for Rollback

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated-migration

This command starts the Terraform Enterprise application managed by Replicated. This is the final step in rolling back to the Replicated installation.

```bash
$ replicatedctl app start

```

--------------------------------

### Implement Simplified Terraform Resource Example Widget Create Function (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/best-practices/deprecations

Implements the Create function for a simplified 'example_widget' resource. It retrieves the required 'new_attribute' and adds it to the provider create API call.

```go
func resourceExampleWidgetCreate(d *schema.ResourceData, meta any) error {
    // ... other logic ...

    newAttribute := d.Get("new_attribute").(string)
    // add attribute to provider create API call

    // ... other logic ...
    return resourceExampleWidgetRead(d, meta)
}
```

--------------------------------

### Multiple Provisioners Example (Terraform)

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/resources/provisioners

This example shows how to define multiple provisioners within a single resource block in Terraform. The provisioners are executed sequentially in the order they appear in the configuration.

```terraform
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    command = "echo first"
  }

  provisioner "local-exec" {
    command = "echo second"
  }
}

```

--------------------------------

### Install Software and CA Certificates on Ubuntu for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This Dockerfile snippet installs essential software packages and custom CA certificates for Terraform Enterprise on an Ubuntu base image. It uses `apt-get` for package management and `update-ca-certificates` to integrate the provided certificates.

```dockerfile
FROM ubuntu:bionic

# Install required software for Terraform Enterprise.
RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y --no-install-recommends awscli ca-certificates curl daemontools git-core iproute2 netcat-openbsd openssh-client psmisc redis-tools ssh sudo unzip wget

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/local/share/ca-certificates/
ADD example-intermediate-ca.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

```

```dockerfile
FROM ubuntu:bionic

# Install required software for Terraform Enterprise.
RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y --no-install-recommends awscli ca-certificates curl daemontools git-core iproute2 netcat-openbsd openssh-client psmisc redis-tools ssh sudo unzip wget

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/local/share/ca-certificates/
ADD example-intermediate-ca.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

```

--------------------------------

### Initialize Project from Template (CLI)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.11.x/create-and-deploy/project-setup

Scaffolds a new CDKTF project using a specified template. This command automatically creates the necessary file structure for defining infrastructure. Available templates include typescript, python, c#, java, and go (experimental).

```bash
cdktf init --template="templateName"
```

```bash
cdktf init --template="templateName"
```

--------------------------------

### Instantiate KubernetesWebAppDeployment Construct in Python

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/constructs

This Python snippet shows how to import and use the `KubernetesWebAppDeployment` construct. It sets up the Kubernetes provider using a kubeconfig file and defines the deployment's image, replica count, application details, and environment.

```python
from constructs import Construct
from cdktf import App, TerraformStack
from constructs.kubernetes_web_app_deployment import KubernetesWebAppDeployment
from providers.kubernetes.provider import KubernetesProvider
import os

class MyKubernetesStack(TerraformStack):
    def __init__(self, scope: Construct, name: str):
        super().__init__(scope, name)
        KubernetesProvider(self, "kind",
            config_path=os.path.join(os.path.dirname(__file__), '..', 'kubeconfig.yaml')
        )

        KubernetesWebAppDeployment(self, "deployment",
            image="nginx:latest",
            replicas=2,
            app="myapp",
            component="frontend",
            environment="dev"
        )


app = App()
MyKubernetesStack(app, "demo")
app.synth()

```

--------------------------------

### Initialize Terraform Cloud and Migrate State (CLI)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.16.x/concepts/remote-backends

Demonstrates the command-line process for initializing Terraform Cloud and migrating existing state. It prompts the user to confirm state migration and shows the output of provider plugin initialization.

```bash
cdktf diff <stack name> --migrate-state

Initializing Terraform Cloud...
Migrating from backend "local" to Terraform Cloud.
Do you wish to proceed?
              As part of migrating to Terraform Cloud, Terraform can optionally copy your
              current workspace state to the configured Terraform Cloud workspace.

              Answer "yes" to copy the latest state snapshot to the configured
              Terraform Cloud workspace.

              Answer "no" to ignore the existing state and just activate the configured
              Terraform Cloud workspace with its existing state, if any.

              Should Terraform migrate your existing state?

              Enter a value:
yes
Initializing provider plugins...
            - Reusing previous version of hashicorp/random from the dependency lock file
- Using previously-installed hashicorp/random v3.4.3
Terraform Cloud has been successfully initialized!
```

--------------------------------

### Clone Example Repository using Git

Source: https://developer.hashicorp.com/terraform/tutorials/applications/cloudflare-static-website_variants=cdn%3Acloudflare

This snippet demonstrates how to clone a remote Git repository to your local machine. It uses the `git clone` command followed by the repository's URL. Ensure Git is installed and accessible in your environment.

```shell
git clone https://github.com/hashicorp-education/learn-terraform-cloudflare-static-website
```

--------------------------------

### Terraform Module and Configuration Structure Example

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/syntax/style

This example demonstrates a recommended repository structure for Terraform, separating reusable modules (e.g., function, queue, vpc) from the main infrastructure configuration. Each module has its own directory with main.tf, outputs.tf, and variables.tf files.

```terraform
.\n├── modules\n│   ├── function\n│   │   ├── main.tf      # contains aws_iam_role, aws_lambda_function\n│   │   ├── outputs.tf\n│   │   └── variables.tf\n│   ├── queue\n│   │   ├── main.tf      # contains aws_sqs_queue\n│   │   ├── outputs.tf\n│   │   └── variables.tf\n│   └── vpc\n│       ├── main.tf      # contains aws_vpc, aws_subnet\n│       ├── outputs.tf\n│       └── variables.tf\n├── main.tf\n├── outputs.tf\n└── variables.tf\n
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/it-saas/servicenow-sgc

Clones the example configuration repository for the ServiceNow Service Graph Connector tutorial. This repository contains the necessary Terraform configuration files.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-snow-sgc

```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/helm-provider

This command initializes the Terraform working directory. It downloads the necessary provider plugins (e.g., `helm`, `kubernetes`, `aws`) and sets up the backend configuration. This step is required before applying any Terraform changes.

```bash
$ terraform init
Initializing the backend...

Initializing provider plugins...
- terraform.io/builtin/terraform is built in to Terraform
- Reusing previous version of hashicorp/kubernetes from the dependency lock file
- Reusing previous version of hashicorp/aws from the dependency lock file
- Reusing previous version of hashicorp/helm from the dependency lock file
- Using previously-installed hashicorp/aws v4.52.0
- Using previously-installed hashicorp/helm v2.8.0
- Using previously-installed hashicorp/kubernetes v2.17.0

Terraform has been successfully initialized!

##...
```

--------------------------------

### Clone Example Terraform Configuration Repository

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-use/terraform-workflow%3Acommunity_variants=terraform-workflow%3Alab

This command clones the example repository containing Terraform configuration that uses modules to create an AWS environment. Ensure you have Git installed and configured.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-modules-use
```

--------------------------------

### Clone Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/cli/plan_utm_offer=ARTICLE_PAGE

Clones the 'learn-terraform-plan' repository from GitHub using the git command. This repository contains example Terraform configurations for creating an EC2 instance.

```bash
# Clone the example repository
$ git clone https://github.com/hashicorp-education/learn-terraform-plan

```

--------------------------------

### Configure Example Widget Resource for Testing

Source: https://developer.hashicorp.com/terraform/plugin/testing/testing-patterns

Generates a Terraform configuration string for the 'example_widget' resource. This function takes a name as input and returns a string suitable for use in acceptance tests.

```go
func testAccExampleResource(name string) string {
    return fmt.Sprintf(
        `
resource "example_widget" "foo" {
  active = true
  name = "%s"
}`, name)
}

```

--------------------------------

### Install and Configure Habitat Services with Terraform

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/resources/provisioners/habitat

This example demonstrates how to use the Habitat provisioner within a Terraform resource to install and configure Redis services. It specifies connection details, service type, license acceptance, and custom TOML configuration for the Redis service.

```terraform
resource "aws_instance" "redis" {
  count = 3

  provisioner "habitat" {
    peers = [aws_instance.redis[0].private_ip]
    use_sudo = true
    service_type = "systemd"
    accept_license = true

    service {
      name = "core/redis"
      topology = "leader"
      user_toml = file("conf/redis.toml")
    }
  }
}

```

--------------------------------

### Reconfigure Replicated Proxy Settings

Source: https://developer.hashicorp.com/terraform/enterprise/v202209-2/install/interactive/installer

This snippet shows how to update the proxy settings for Replicated services after installation. It involves editing configuration files and adding proxy environment variables to REPLICATED_OPTS or REPLICATED_OPERATOR_OPTS.

```bash
# Example for replicated file
REPLICATED_OPTS="-e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>"

# Example for replicated-operator file
REPLICATED_OPERATOR_OPTS="-e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>"
```

--------------------------------

### SFTP Configuration and Setup

Source: https://developer.hashicorp.com/terraform/enterprise/v202409-3/replicated/administration/infrastructure/automated-recovery

This script sets up the SFTP configuration for snapshot storage and retrieval. It defines variables for the SSH key, SFTP server host, and user. The 'access' variable is constructed using these variables to specify the SFTP store.

```bash
key_file=path_to_your_ssh_key
key="$(base64 -w0 \"$key_file\")"
host=sftp_server_hostname_or_ip
user=user_to_sftp_on_the_remote_server

access="--store sftp --sftp-host $host --sftp-user $user --sftp-key $key"
```

--------------------------------

### Run Terraform Provider Unit Tests (Go)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This command executes the unit tests for the exampletime Terraform provider using Go's testing framework. The `TF_ACC=1` environment variable is set to enable acceptance tests, and `-count=1 -v` flags are used for a single run with verbose output. The output shows the status of each test case, including `TestRFC3339Parse_UTC`, `TestRFC3339Parse_offset`, and `TestRFC3339Parse_invalid`, confirming that all tests passed.

```bash
TF_ACC=1 go test -count=1 -v
```

--------------------------------

### Inspect Terraform Enterprise Pods

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/openshift

Verify that the Terraform Enterprise pods have started successfully by listing the pods in the specified OpenShift project. If pods fail to start, consult Kubernetes troubleshooting guides.

```bash
$ oc get pods -n <TFE_PROJECT>

```

--------------------------------

### Terraform substr Function Example: Basic Extraction

Source: https://developer.hashicorp.com/terraform/language/functions/substr

This example demonstrates the basic usage of the `substr` function to extract a substring starting from the second character (index 1) with a length of 4 characters.

```terraform
substr("hello world", 1, 4)
```

--------------------------------

### Instantiate KubernetesWebAppDeployment Construct in Java

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/constructs

This Java code demonstrates importing and using the `KubernetesWebAppDeployment` construct. It configures the Kubernetes provider with a kubeconfig path and specifies the image, replica count, application name, component, and environment for the web application deployment.

```java
import java.nio.file.Paths;
import imports.kubernetes.provider.KubernetesProvider;
import imports.kubernetes.provider.KubernetesProviderConfig;
import com.mycompany.app.myconstructs.KubernetesWebAppDeployment;
import com.mycompany.app.myconstructs.KubernetesWebAppDeploymentConfig;
import software.constructs.Construct;
import com.hashicorp.cdktf.TerraformStack;
import com.hashicorp.cdktf.App;

public class MainUseConstructs extends TerraformStack {

    public MainUseConstructs(Construct scope, String name){
        super(scope, name);

        new KubernetesProvider(this, "kind", KubernetesProviderConfig.builder()
                .configPath(Paths.get(System.getProperty("user.dir"), "..", "kubeconfig.yaml").toString())
                .build()
        );

        new KubernetesWebAppDeployment(this, "deployment",  KubernetesWebAppDeploymentConfig.builder()
                .image("nginx:latest")
                .replicas(2)
                .app("myapp")
                .components("frontend")
                .environments("dev")
                .build()
        );
    }

    public static void main(String[] args) {
        final App app = new App();
        new MainUseConstructs(app, "demo");
        app.synth();
    }
}

```

--------------------------------

### Install Kind using Homebrew (macOS)

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/kubernetes-provider/kubernetes%3Akind_variants=kubernetes%3Akind

Installs the 'kind' tool on macOS using the Homebrew package manager. This is a prerequisite for creating local Kubernetes clusters for the tutorial.

```shell
$ brew install kind

```

--------------------------------

### Configure Proxy Exclusions (NO_PROXY) during Terraform Enterprise Installation

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This command configures proxy exclusions for the Terraform Enterprise installer, specifying hostnames that should bypass the proxy. This is useful for services like S3 or internal VCS that need direct access. The exclusions are provided as a comma-separated list.

```bash
./install.sh additional-no-proxy=s3.amazonaws.com,internal-vcs.mycompany.com,example.com
```

--------------------------------

### Install Terraform MCP Server using Go (Shell)

Source: https://developer.hashicorp.com/terraform/mcp-server/deploy

These shell commands demonstrate how to install the Terraform MCP server using the Go programming language. The first command installs the latest stable release, while the second installs the development version from the main branch.

```shell
$ go install github.com/hashicorp/terraform-mcp-server/cmd/terraform-mcp-server@latest

```

```shell
$ go install github.com/hashicorp/terraform-mcp-server/cmd/terraform-mcp-server@main

```

--------------------------------

### Terraform Apply Start Message Example (JSON)

Source: https://developer.hashicorp.com/terraform/internals/v1.1.x/machine-readable-ui

This JSON snippet represents a 'apply_start' message from Terraform. It indicates the beginning of an operation on a specific resource, detailing the action (e.g., 'create') and resource identifiers. This message is crucial for tracking the lifecycle of resource modifications.

```json
{
  "@level": "info",
  "@message": "random_pet.animal: Creating...",
  "@module": "terraform.ui",
  "@timestamp": "2021-05-25T13:32:41.825308-04:00",
  "hook": {
    "resource": {
      "addr": "random_pet.animal",
      "module": "",
      "resource": "random_pet.animal",
      "implied_provider": "random",
      "resource_type": "random_pet",
      "resource_name": "animal",
      "resource_key": null
    },
    "action": "create"
  },
  "type": "apply_start"
}
```

--------------------------------

### Verify tf-migrate installation

Source: https://developer.hashicorp.com/terraform/migrate/install

This snippet demonstrates how to verify the successful installation of tf-migrate. It uses the `-help` flag to display the tool's usage information and available commands.

```bash
$ tf-migrate -help
Welcome to the HCP Terraform Migrator for Community Edition.

Usage: tf-migrate [global options] <subcommand> [args]

The available commands for execution are listed below.
The primary workflow commands are given first,
followed by global options.

Commands:
##...
```

--------------------------------

### Install Local Terraform Provider with Go

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-provider

Compiles and installs the Terraform provider binary into your GOBIN path, making it available for local development. This command should be run from the root directory of your provider's Go module.

```bash
go install .
```

--------------------------------

### Manual Provider Installation Path for Terraform

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/run/install-software

This example illustrates the directory structure required for manually installing a custom provider binary on a Terraform worker. The path must match the source specified in the `required_providers` block, including the host, namespace, plugin name, version, and architecture.

```bash
terraform.d/plugins/<SOURCE HOST>/<SOURCE NAMESPACE>/<PLUGIN NAME>/<VERSION>/linux_amd64/terraform-provider-<PLUGIN NAME>
```

--------------------------------

### Terraform Initialization and Plan

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

Shows the output of Terraform initialization and plan commands. This includes provider installation, backend initialization, and a summary of planned infrastructure changes.

```bash
Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/boundary versions matching "1.0.5"...
- Installing hashicorp/boundary v1.0.5...
- Installed hashicorp/boundary v1.0.5 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

...
... truncated output ...
...

Plan: 24 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + username = {
      + user1 = {
          + auth_method_id = (known after apply)
          + description    = "User account for user1"
          + id             = (known after apply)
          + login_name     = "user1"
          + name           = "user1"
          + password       = "password"
          + type           = "password"
        }
    }
boundary_scope.global: Creating...
boundary_scope.global: Creation complete after 0s [id=global]
boundary_scope.org: Creating...
boundary_role.global_anon_listing: Creating...
boundary_scope.org: Creation complete after 0s [id=o_zYT1ci74Xp]
boundary_auth_method.password: Creating...
boundary_scope.project: Creating...
boundary_role.org_anon_listing: Creating...
boundary_scope.project: Creation complete after 1s [id=p_uMmQ2Nmyzr]
boundary_host_catalog.databases: Creating...
boundary_auth_method.password: Creation complete after 1s [id=ampw_rZ6z1yjsNQ]
boundary_account.user["user1"]: Creating...
boundary_host_catalog.databases: Creation complete after 0s [id=hcst_Iws4PPJ0Cd]
boundary_host.redis: Creating...
boundary_host.localhost: Creating...
boundary_host.postgres: Creating...
boundary_host.mysql: Creating...
boundary_account.user["user1"]: Creation complete after 1s [id=acctpw_z3wsUqIxl0]
boundary_user.user["user1"]: Creating...
boundary_role.global_anon_listing: Creation complete after 2s [id=r_jf0aBQrlq9]
boundary_host.redis: Creation complete after 1s [id=hst_AfZWO0NmRH]
boundary_host_set.redis: Creating...

```

--------------------------------

### Initialize App and Synthesize Stacks (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/variables-and-outputs

This Go function initializes the Terraform CDK application and instantiates both the producer and consumer stacks. It then calls 'app.Synth()' to synthesize the Terraform configuration. This requires the 'cdktf' library.

```go
import (
    "github.com/hashicorp/terraform-cdk-go/cdktf"
)

func main() {
    app := cdktf.NewApp(nil)

    NewProducerStack(app, "cdktf-producer")
    NewConsumerStack(app, "cdktf-consumer")

    app.Synth()
}
```

--------------------------------

### Local Module Source Example (Terraform)

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/modules/sources

This example demonstrates how to reference a local module using a relative path. Local paths are used for factoring out code within the same repository and are not 'installed' like remote modules.

```terraform
module "consul" {
  source = "./consul"
}

```

--------------------------------

### Configure Replicated Proxy Settings (Bash)

Source: https://developer.hashicorp.com/terraform/enterprise/v202308-1/install/interactive/installer

This snippet shows how to update the proxy settings for Replicated services after Terraform Enterprise has been installed. It involves editing configuration files and adding proxy environment variables.

```bash
# Example for replicated service
# Locate the Replicated configuration files on the instance under either /etc/sysconfig/ or /etc/default: replicated and replicated-operator.
# Open the files for editing. On the line that includes REPLICATED_OPTS for replicated or REPLICATED_OPERATOR_OPTS for replicated-operator,
# add -e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts> to the existing command options.
# Example:
# REPLICATED_OPTS="-e HTTP_PROXY=http://internal.mycompany.com:8080 -e NO_PROXY=127.0.0.1,172.17.0.1,$(hostname -i),$(hostname)"
```

--------------------------------

### Terraform Module Structure Example

Source: https://developer.hashicorp.com/terraform/language/style

This example demonstrates a common directory structure for Terraform modules, including main.tf, outputs.tf, and variables.tf for each module. It shows how to organize modules for functions, queues, and VPCs.

```terraform
.\n├── modules\n│   ├── function\n│   │   ├── main.tf      # contains aws_iam_role, aws_lambda_function\n│   │   ├── outputs.tf\n│   │   └── variables.tf\n│   ├── queue\n│   │   ├── main.tf      # contains aws_sqs_queue\n│   │   ├── outputs.tf\n│   │   └── variables.tf\n│   └── vpc\n│       ├── main.tf      # contains aws_vpc, aws_subnet\n│       ├── outputs.tf\n│       └── variables.tf\n├── main.tf\n├── outputs.tf\n└── variables.tf

```

--------------------------------

### Update CA Certificates - Ubuntu

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-3/install/interactive/installer

Updates the CA certificates bundle on Ubuntu-based Docker images. This ensures that newly added CA certificates are recognized by the system. It requires the `ca-certificates` package to be installed.

```dockerfile
RUN update-ca-certificates
```

--------------------------------

### Deployment Output Example

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/variables-and-outputs

This output is displayed when `cdktf deploy` is executed. It shows the resources created, including the 'random_pet.pet', and the value of the 'random-pet' output, which is a randomly generated string.

```text
Deploying Stack: cdktf-demo
Resources
 ✔ RANDOM_PET     pet     random_pet.pet

Summary: 1 created, 0 updated, 0 destroyed.

Output: random-pet = choice-haddock

```

--------------------------------

### Navigate to Terraform Example Repository Directory

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/locals

Change the current directory to the cloned Terraform example repository. This step is necessary to access and modify the Terraform configuration files for the tutorial.

```bash
cd learn-terraform-locals
```

--------------------------------

### Install Custom Provider Binary (Terraform < 0.13)

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/workspaces/run/install-software

For Terraform versions prior to 0.13, custom or community providers must be installed manually. This involves placing the compiled provider binary in the `terraform.d/plugins/linux_amd64/` directory within your workspace's configuration. Ensure the plugin file has read and execute permissions.

```shell
## Add the provider binary to the VCS repo (or manually-uploaded configuration version) for any workspace that uses it.
# Place the compiled `linux_amd64` version of the plugin at `terraform.d/plugins/linux_amd64/<PLUGIN NAME>`
# (as a relative path from the root of the working directory).
# The plugin name should follow the naming scheme and the plugin file must have read and execute permissions.
```

--------------------------------

### Provision Start Log

Source: https://developer.hashicorp.com/terraform/internals/v1.1.x/machine-readable-ui

This log message indicates that a provisioner has started executing for a resource.

```APIDOC
## Provision Start Log

### Description
This log message indicates that a provisioner has started executing for a resource.

### Method
N/A (Log Event)

### Endpoint
N/A (Log Event)

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
  "@level": "info",
  "@message": "null_resource.none[0]: Provisioning with 'local-exec'...",
  "@module": "terraform.ui",
  "@timestamp": "2021-03-26T16:38:43.997431-04:00",
  "hook": {
    "resource": {
      "addr": "null_resource.none[0]",
      "module": "",
      "resource": "null_resource.none[0]",
      "implied_provider": "null",
      "resource_type": "null_resource",
      "resource_name": "none",
      "resource_key": 0
    },
    "provisioner": "local-exec"
  },
  "type": "provision_start"
}
```

### Response
#### Success Response (200)
None (This is a log message, not an API response)

#### Response Example
None
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/configure-providers/three-cloud-providers%3Aaws_variants=three-cloud-providers%3Aaws

Clones the example repository containing Terraform configurations for the tutorial. This repository is essential for following the provided examples and setting up your environment.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-providers

```

--------------------------------

### Example Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This is an example of how to configure the HashiCups provider in a Terraform configuration file (`main.tf`). It specifies the username, password, and host for the provider.

```hcl
provider "hashicups" {
  username = "education"
  password = "test123"
  host     = "http://localhost:19090"
}

```

--------------------------------

### Create Terraform Provider Instance Helper (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/providers

This Go function, 'New', simplifies the creation of a provider server implementation. It returns a function that instantiates and returns an 'ExampleCloudProvider' with a specified version.

```Go
func New(version string) func() provider.Provider {
    return func() provider.Provider {
        return &ExampleCloudProvider{
            Version: version,
        }
    }
}

```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/eks

Clones the example repository containing Terraform configuration for provisioning an EKS cluster. This is the initial step to obtain the necessary configuration files.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-provision-eks-cluster
```

--------------------------------

### Generate Provider Classes with cdktf get

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/providers

This command-line example shows the execution of `cdktf get` to download and generate the necessary TypeScript classes for Terraform providers. This step is crucial for using providers within the CDK project.

```bash
cdktf get
⠋ downloading and generating providers...

```

--------------------------------

### GET /api/v2/admin/organizations

Source: https://developer.hashicorp.com/terraform/enterprise/v202502-1/api-docs/admin/organizations

Lists all organizations in the Terraform Enterprise installation. Supports filtering, searching, and pagination.

```APIDOC
## GET /api/v2/admin/organizations

### Description
This endpoint lists all organizations in the Terraform Enterprise installation. It supports filtering by module and provider sharing configurations, searching by name or email, and pagination.

### Method
GET

### Endpoint
/api/v2/admin/organizations

### Query Parameters
#### Query Parameters
- **q** (string) - Optional - A search query string. Organizations are searchable by name and notification email. This query takes precedence over the attribute specific searches `q[email]` or `q[name]`.
- **q[email]** (string) - Optional - A search query string. This query searches organizations by notification email. If used with `q[name]`, it returns organizations that match both queries.
- **q[name]** (string) - Optional - A search query string. This query searches organizations by name. If used with `q[email]`, it returns organizations that match both queries.
- **filter[module_producer]** (boolean) - Optional - Allows filtering organizations based on their module sharing configuration. Accepts a boolean true/false value. A `true` value returns organizations that are configured to share their modules, and a `false` value returns organizations that are not configured to share their modules.
- **filter[provider_producer]** (boolean) - Optional - Allows filtering organizations based on their provider sharing configuration. Accepts a boolean true/false value. A `true` value returns organizations that are configured to share their providers, and a `false` value returns organizations that are not configured to share their providers.
- **page[number]** (integer) - Optional - If omitted, the endpoint will return the first page.
- **page[size]** (integer) - Optional - If omitted, the endpoint will return 20 organizations per page.
- **include** (string) - Optional - Allows requesting related resources. Available resource types: `owners`.

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  "https://tfe.example.com/api/v2/admin/organizations?q[name]=example&include=owners"
```

### Response
#### Success Response (200)
- **data** (array) - A JSON API document with `type: "organizations"`.
- **links** (object) - Links related to the response, including pagination.
- **included** (array) - Included related resources if requested (e.g., `owners`).

#### Response Example
```json
{
  "data": [
    {
      "type": "organizations",
      "id": "1",
      "attributes": {
        "name": "Example Org",
        "notification-email": "example@example.com",
        "created-at": "2023-01-01T12:00:00Z",
        "updated-at": "2023-01-01T12:00:00Z"
      },
      "links": {
        "self": "/api/v2/admin/organizations/1"
      }
    }
  ],
  "links": {
    "self": "/api/v2/admin/organizations?page[number]=1&page[size]=20"
  }
}
```

#### Error Response (404)
- **errors** (array) - A JSON API error object indicating the client is not an administrator.
```

--------------------------------

### Implement Create and Read Functions for HashiCups Order Resource (Go)

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

Outlines the implementation of `Create` and `Read` functions for the HashiCups order resource. The `Create` function handles API calls to provision a resource and persist its state, while `Read` fetches existing resource data from the API.

```go
// Create function implementation placeholder
func (r *OrderResource) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
    // Implementation to create the resource via API
    // ...
    // Persist resource data to Terraform state
    // ...
}

// Read function implementation placeholder
func (r *OrderResource) Read(ctx context.Context, req resource.ReadRequest, resp *resource.ReadResponse) {
    // Implementation to read the resource data from API
    // ...
    // Load resource data into Terraform state
    // ...
}
```

--------------------------------

### Initialize Terraform Workspace with New Module (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/configure-providers/three-cloud-providers%3Aaws_variants=three-cloud-providers%3Agcp

This command initializes the Terraform workspace, installing necessary provider plugins and downloading the specified module. It's crucial to run after adding or changing provider configurations or modules to ensure Terraform recognizes the new setup. The output confirms the successful installation of the AWS provider and the 's3-bucket' module.

```bash
$ terraform init
Initializing the backend...
Initializing modules...
Downloading registry.terraform.io/terraform-aws-modules/s3-bucket/aws 5.2.0 for website_east...
- website_east in .terraform/modules/website_east
Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/aws v6.6.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

--------------------------------

### GET /api/v2/admin/runs

Source: https://developer.hashicorp.com/terraform/enterprise/v202410-1/api-docs/admin/runs

Lists all runs in the Terraform Enterprise installation. This endpoint is restricted to administrators.

```APIDOC
## GET /api/v2/admin/runs

### Description
Lists all runs in the Terraform Enterprise installation. This endpoint is restricted to administrators.

### Method
GET

### Endpoint
/api/v2/admin/runs

### Query Parameters
#### Query Parameters
- **q** (string) - Optional. A search query string. Runs are searchable by ID, workspace name, organization name or email, and VCS repository identifier.
- **filter[status]** (string) - Optional. A comma-separated list of Run statuses to restrict results to. Possible values include: "pending", "plan_queued", "planning", "planned", "confirmed", "apply_queued", "applying", "applied", "discarded", "errored", "canceled", "cost_estimating", "cost_estimated", "policy_checking", "policy_override", "policy_soft_failed", "policy_checked", and "planned_and_finished".
- **filter[from]** (string) - Optional. Must be formatted in RFC 3339 and UTC.
- **filter[to]** (string) - Optional. Must be formatted in RFC 3339 and UTC.
- **page[number]** (integer) - Optional. If omitted, the endpoint will return the first page.
- **page[size]** (integer) - Optional. If omitted, the endpoint will return 20 runs per page.

*Note: A VCS repository identifier is a reference to a VCS repository in the format `:org/:repo`, where `:org` and `:repo` refer to the organization (or project) and repository in your VCS provider.*

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  "https://app.terraform.io/api/v2/admin/runs"
```

### Response
#### Success Response (200)
- **data** (array) - A JSON API document with type "runs".

#### Response Example
```json
{
  "data": [
    {
      "type": "runs",
      "id": "run-id-1",
      "attributes": {
        "status": "applied"
      }
    },
    {
      "type": "runs",
      "id": "run-id-2",
      "attributes": {
        "status": "errored"
      }
    }
  ]
}
```

#### Error Response (404)
- **errors** (array) - A JSON API error object indicating the client is not an administrator.

#### Error Response Example
```json
{
  "errors": [
    {
      "status": "404",
      "title": "Client is not an administrator."
    }
  ]
}
```
```

--------------------------------

### Implement Update Function for Example Widget (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/deprecations

Handles updating the 'example_widget' resource. Similar to create, it validates the presence of 'existing_attribute' or 'new_attribute' and applies the changes to the provider API. It then calls the read function to refresh the resource state.

```go
func resourceExampleWidgetUpdate(d *schema.ResourceData, meta interface{}) error {
    // ... other logic ...

    existingAttribute, existingAttributeOk := d.GetOk("existing_attribute")
    newAttribute, newAttributeOk := d.GetOk("new_attribute")
    if !existingAttributeOk && !newAttributeOk {
        return errors.New("one of existing_attribute or new_attribute must be configured")
    }
    if existingAttributeOk {
        // add existingAttribute to provider update API call
    } else {
        // add newAttribute to provider update API call
    }

    // ... other logic ...
    return resourceExampleWidgetRead(d, meta)
}
```

--------------------------------

### Installing Additional Tools with local-exec Provisioner

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/run/run-environment

Example of using the `local-exec` provisioner within a Terraform resource to install additional tools on the worker VM. This requires careful handling as worker VMs are ephemeral and changes are not persisted.

```Terraform
resource "null_resource" "install_tools" {
  provisioner "local-exec" {
    command = "sudo apt-get update && sudo apt-get install -y some-tool"
  }
}
```

--------------------------------

### Implement List Method for ExampleCloud Thing Resource (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/resources/list

This Go code snippet demonstrates the implementation of the `List` method for the `examplecloud_thing` resource. It shows how to retrieve configuration data, make external API calls (simulated), and convert SDKv2 resource data into framework types for streaming results. Dependencies include the Terraform Plugin Framework and SDKv2.

```go
// Some list.ListResource interface methods are omitted for brevity.

import (
    "context"

    "github.com/hashicorp/terraform-plugin-framework/list"
    "github.com/hashicorp/terraform-plugin-sdk/v2/terraform"
)

type ThingListResource struct{}

func (r *ThingListResource) Metadata(ctx context.Context, req resource.MetadataRequest, resp *resource.MetadataResponse) {
    resp.TypeName = "examplecloud_thing"
}

func (r *ThingListResource) RawV5Schemas(ctx context.Context, req list.RawV5SchemaRequest, resp *list.RawV5SchemaResponse) {
    // Where `resourceThing` returns an SDKv2 `schema.Resource` instance
    thingResource := resourceThing()

    resp.ProtoV5Schema = thingResource.ProtoSchema(ctx)()
    resp.ProtoV5IdentitySchema = thingResource.ProtoIdentitySchema(ctx)()
}

func (r *ThingListResource) List(ctx context.Context, req list.ListRequest, stream *list.ListResultsStream) {
    var data ThingListResourceModel

    // Read list config data into the model
    diags := request.Config.Get(ctx, &data)
    if diags.HasError() {
        stream.Results = list.ListResultsStreamDiagnostics(diags)
        return
    }

    // Typically lists will make external calls here using data from the config
    // as input. For brevity, we assume the `things` slice below was returned by an
    // API call here

    // Define the function that will push results into the stream
    stream.Results = func(push func(list.ListResult) bool) {
        for _, thing := range things {
            // Initialize a new result object for each thing
            result := req.NewListResult(ctx)

            // Set the user-friendly name of this thing
            result.DisplayName = thing.Name

            // Create an instance of the SDKv2 resource
            thingResource := resourceThing()

            // Create a new ResourceData object to hold the state of this thing
            rd := thingResource.Data(&terraform.InstanceState{})

            // Set the ID of the resource for the ResourceData object
            rd.SetId("a_unique_id_related_to_the_thing")

            // Get the existing identity data from ResourceData and set relevant identity attributes
            identity, err := rd.Identity()
            if err != nil {
                result.Diagnostics.AddError(
                    "Retrieving identity data",
                    "An error was encountered when retrieving the identity data: "+err.Error(),
                )
            }

            identity.Set("an_identity_attribute", thing.IdentityAttribute)

            // Set the attributes of interest into the resource state
            rd.Set("name", thing.Name)
            rd.Set("attribute_one", thing.AttributeOne)
            rd.Set("attribute_two", thing.AttributeTwo)

            // Convert and set the identity and resource state into the result
            tfTypeIdentity, err := rd.TfTypeIdentityState()
            if err != nil {
                result.Diagnostics.AddError(
                    "Converting identity data",
                    "An error was encountered when converting the identity data: "+err.Error(),
                )
            }

            if err := result.Identity.Set(ctx, *tfTypeIdentity); err != nil {
                result.Diagnostics.AddError(
                    "Setting identity data",
                    "An error was encountered when setting the identity data: "+err.Error(),
                )
            }

            // Convert and set the resource state into the result
            tfTypeResource, err := rd.TfTypeResourceState()
            if err != nil {
                result.Diagnostics.AddError(
                    "Converting resource state",
                    "An error was encountered when converting the resource state: "+err.Error(),
                )
            }

            if err := result.Resource.Set(ctx, *tfTypeResource); err != nil {
                result.Diagnostics.AddError(
                    "Setting resource state",
                    "An error was encountered when setting the resource state: "+err.Error(),
                )
            }

            // Send the result to the stream.
            if !push(result) {
                return
            }
        }
    }
}

```

--------------------------------

### Initialize Terraform with New Provider Configurations

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/configure-providers/three-cloud-providers%3Aazure_variants=three-cloud-providers%3Aaws

This output shows the result of running `terraform init` after adding new provider configurations or modules. It details the initialization process, including backend setup, module installation, and provider plugin discovery. The output confirms that existing providers are reused and new ones (like Azure API and ModTm) are installed, updating the lock file.

```bash
$ terraform init
Initializing the backend...
Initializing modules...
Initializing provider plugins...
- Reusing previous version of hashicorp/azurerm from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Finding azure/azapi versions matching ">= 1.14.0, < 3.0.0"...
- Finding azure/modtm versions matching "~> 0.3"...
- Using previously-installed hashicorp/azurerm v4.37.0
- Using previously-installed hashicorp/random v3.7.2
- Installing azure/azapi v2.5.0...
- Installed azure/azapi v2.5.0 (signed by a HashiCorp partner, key ID 6F0B91BDE98478CF)
- Installing azure/modtm v0.3.5...
- Installed azure/modtm v0.3.5 (signed by a HashiCorp partner, key ID 6F0B91BDE98478CF)
Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://developer.hashicorp.com/terraform/cli/plugins/signing
Terraform has made some changes to the provider dependency selections recorded
in the .terraform.lock.hcl file. Review those changes and commit them to your
version control system if they represent changes you intended to make.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Install jq and Terraform, Restore Snapshot via SFTP

Source: https://developer.hashicorp.com/terraform/enterprise/v202503-1/admin/infrastructure/automated-recovery

This script installs jq, installs Terraform, retrieves a list of snapshots from an SFTP server, identifies the latest snapshot, and restores it. It uses SFTP for storage and waits for the application to boot after restoration. The script requires an SSH key and SFTP server details.

```bash
```bash
#!/bin/bash

set -e -u -o pipefail

key_file=path_to_your_ssh_key
key="$(base64 -w0 \"$key_file\")"
host=sftp_server_hostname_or_ip
user=user_to_sftp_on_the_remote_server

access="--store sftp --sftp-host $host --sftp-user $user --sftp-key $key"

# jq is used by this script, so install it. For other Linux distros, either preinstall jq
# and remove these lines, or change to the mechanism your distro uses to install jq.

apt-get update
apt-get install -y jq

# Run the installer.

curl https://install.terraform.io/ptfe/stable | bash -s fast-timeouts

# Wait for replicated to start before proceeding
until replicatedctl system status --template '{{and (eq .Replicated \"ready\") (eq .Retraced \"ready\")}}' | grep -q true; do
  sleep 1
  echo "Replicated is not yet ready."
done
echo "Replicated is ready."

# This retrieves a list of all the snapshots currently available.
replicatedctl snapshot ls $access -o json > /tmp/snapshots.json

# Pull just the snapshot id out of the list of snapshots
id=$(jq -r 'sort_by(.finished) | .[-1].id // \"\"' /tmp/snapshots.json)

# If there are no snapshots available, exit out
if test \"$id\" = \"\"; then
  echo "No snapshots found"
  exit 1
fi

echo "Restoring snapshot: $id"

# Restore the detected snapshot. This ignores preflight checks to be sure the application
# is booted.
replicatedctl snapshot restore $access --dismiss-preflight-checks \"$id\"

# Wait until the application reports itself as running. This step can be removed if
# something upstream is prepared to wait for the application to finish booting.
until curl -f -s --connect-timeout 1 http://localhost/_health_check; do
  sleep 1
done

echo
echo "Application booted!"
```
```

--------------------------------

### Initialize Terraform pg Backend with Partial Configuration

Source: https://developer.hashicorp.com/terraform/language/v1.2.x/backend/pg

This example demonstrates initializing the 'pg' backend using a partial configuration, deferring the connection string to the `terraform init` command. This is recommended for sensitive credentials.

```terraform
terraform {
  backend "pg" {}
}

terraform init -backend-config="conn_str=postgres://user:pass@db.example.com/terraform_backend"
```

--------------------------------

### Install Azure CLI on Windows with PowerShell

Source: https://developer.hashicorp.com/terraform/tutorials/azure-get-started/azure-build

Installs the Azure CLI on Windows using PowerShell by downloading and executing the MSI installer. This is a prerequisite for authenticating with Azure.

```powershell
$Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi

```

--------------------------------

### Initialize Kubernetes Provider and Deploy Web App (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.12.x/concepts/constructs

Initializes a Kubernetes provider for CDKTF using a specified config path and deploys a web application with configurable image, replicas, and metadata. This snippet demonstrates basic CDKTF resource provisioning in Go.

```go
package main

import (
	"github.com"
	"github.com/aws/constructs-go/constructs/v10"
	"github.com/hashicorp/cdktf-provider-kubernetes-go/kubernetes/v2"
	"github.com/hashicorp/cdktf-provider-null-go/null/v2"
	"github.com/hashicorp/terraform-cdk-go/cdktf"
	"path"
)

type ExampleCdktfDocumentationStackProps struct {
	cdktf.TerraformStackProps
}

func NewExampleCdktfDocumentationStack(scope constructs.Construct, id string, props *ExampleCdktfDocumentationStackProps) cdktf.TerraformResourceConstructor {
	cdktf.NewTerraformStack(scope, &id, props)

	// Initialize Kubernetes Provider
	kubernetes.NewKubernetesProvider(stack, jsii.String("kind"), &kubernetes.KubernetesProviderConfig{
		ConfigPath: jsii.String(path.Join(cwd, "kubeconfig.yaml")),
	})

	// Deploy a Kubernetes Web App
	myconstructs.NewKubernetesWebAppDeployment(stack, "deployment", map[string]interface{}{
		"image":       jsii.String("nginx:latest"),
		"replicas":    jsii.Number(2),
		"app":         jsii.String("myapp"),
		"component":   jsii.String("frontend"),
		"environment": jsii.String("dev"),
	})

	return stack
}

func main() {
	app := cdktf.NewApp(nil)

	NewExampleCdktfDocumentationStack(app, "demo", &ExampleCdktfDocumentationStackProps{
		StackName: jsii.String("demo-stack"),
	})

	app.Synth()
}

```

--------------------------------

### Get Go Binary Path (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-functions

Retrieves the GOBIN path, which is where Go installs binaries. This path is needed to configure local provider installations in Terraform. The command may vary based on Go environment variable configuration.

```shell
go env GOBIN
```

--------------------------------

### Implement Data Source Methods with Framework

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/data-sources

This example shows the implementation of core methods for a data source (`exampleDataSource`) using the Terraform Framework. It includes defining metadata, schema, and the read function.

```go
func (d *exampleDataSource) Metadata(ctx context.Context, req datasource.MetadataRequest, resp *datasource.MetadataResponse) {
    resp.TypeName = "example_datasource"
}

func (d *exampleDataSource) Schema(ctx context.Context, req datasource.SchemaRequest, resp *datasource.SchemaResponse) {
    resp.Schema = schema.Schema{
        Attributes: map[string]schema.Attribute{
            "example_attribute": schema.StringAttribute{
                Required:    true,
            },
            /* ... */

func (d *exampleDataSource) Read(ctx context.Context, req datasource.ReadRequest, resp *datasource.ReadResponse) {
    /* ... */
}

```

--------------------------------

### Manage Terraform Modules Installation

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-use/terraform-workflow%3Acommunity_variants=terraform-workflow%3Alab

Installs or updates modules used in a Terraform configuration. Running 'terraform init' or 'terraform get' is necessary when using a new module for the first time. Modules are stored in the .terraform/modules directory.

```bash
.terraform/modules/
├── ec2_instances
├── modules.json
└── vpc
```

--------------------------------

### Get Nested List Block Path (Terraform Schema)

Source: https://developer.hashicorp.com/terraform/plugin/framework/handling-data/paths

Shows how to get the path to a nested list block within a parent list item using `AtName()`. This example targets the 'nested_list_block' within the first item of 'root_list_block'.

```go
path.Root("root_list_block").AtListIndex(0).AtName("nested_list_block")

```

--------------------------------

### Deploy Kubernetes Web App (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.15.x/concepts/constructs

Deploys a Kubernetes web application using the `KubernetesWebAppDeployment` construct in Go. It initializes the Kubernetes provider and configures the deployment with an Nginx image, 2 replicas, and specifies app, component, and environment. This code is within a `TerraformStack` and is synthesized by the application.

```go
kubernetes.NewKubernetesProvider(stack, jsii.String("kind"), &kubernetes.KubernetesProviderConfig{
        ConfigPath: jsii.String(path.Join(cwd, "kubeconfig.yaml")),
    })
    myconstructs.NewKubernetesWebAppDeployment(stack, "deployment", map[string]interface{}{
        "image":       jsii.String("nginx:latest"),
        "replicas":    jsii.Number(2),
        "app":         jsii.String("myapp"),
        "component":   jsii.String("frontend"),
        "environment": jsii.String("dev"),
    })

    return stack
}

func main() {
    app := cdktf.NewApp(nil)

    NewConstructsStack(app, "constructs")

    app.Synth()
}
```

--------------------------------

### Terraform Provisioner Configuration Example

Source: https://developer.hashicorp.com/terraform/cdktf/v0.14.x/concepts/resources

This snippet demonstrates the basic structure for configuring provisioners within Terraform, including the 'provisioners' key and the 'connection' key for setting up remote access. It also shows how to use the 'TerraformSelf' class to reference parent resources.

```hcl
resource "aws_instance" "example" {
  # ... other configurations ...

  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx"
    ]

    connection {
      type     = "ssh"
      user     = "ubuntu"
      private_key = file("~/.ssh/id_rsa")
      host     = TerraformSelf.getString("public_ip")
    }
  }
}
```

--------------------------------

### Start Vault Development Server

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/terraform-secrets-engine

Starts a local Vault development server with a specified root token. This server runs with an in-memory database and is not suitable for production environments. Ensure Vault is installed and initialized before running this command.

```bash
$ vault server -dev -dev-root-token-id root

```

--------------------------------

### HCP Terraform Configuration Example

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/integrations/service-now/service-catalog-terraform

Example of the information required for configuring the ServiceNow integration with HCP Terraform. This includes organization name, API token, hostname, VCS details, and variables.

```text
Terraform Enterprise Organization Name: `ServiceNowExampleOrg`

Team API Token: `q2uPExampleELkQ.atlasv1.A7jGHmvufExampleTeamAPITokenimVYxwunJk0xD8ObVol054`

Terraform Enterprise Hostname: `terraform.corp.example`

OAuth Token ID (GitHub org: example-corp): `ot-DhjEXAMPLELVtFA`
  - Repository ID (Developer Environment): `example-corp/developer-repo`
    - Environment variables:
      - `AWS_ACCESS_KEY_ID=AKIAEXAMPLEKEY`
      - `AWS_SECRET_ACCESS_KEY=ZB0ExampleSecretAccessKeyGjUiJh`
      - `AWS_DEFAULT_REGION=us-west-2`
    - Terraform variables:
      - `instance_type=t2.medium`
  - Repository ID (Testing Environment): `example-corp/testing-repo`
    - Environment variables:
      - `AWS_ACCESS_KEY_ID=AKIAEXAMPLEKEY`
      - `AWS_SECRET_ACCESS_KEY=ZB0ExampleSecretAccessKeyGjUiJh`
      - `AWS_DEFAULT_REGION=us-west-2`
    - Terraform variables:
      - `instance_type=t2.large`
```

--------------------------------

### Clone GitHub Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/0-13/for-each

Clones the specified Terraform example GitHub repository to your local machine. This command requires Git to be installed and configured.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-for-each
```

--------------------------------

### Provisioner Configuration Parameters

Source: https://developer.hashicorp.com/terraform/language/v1.12.x/block/resource

This section details the parameters available for configuring provisioners, including target platform, HTTPS settings, authentication, certificate handling, bastion host settings, and proxy configurations.

```APIDOC
## Provisioner Configuration Parameters

### Description
This section details the parameters available for configuring provisioners, including target platform, HTTPS settings, authentication, certificate handling, bastion host settings, and proxy configurations.

### Method
N/A (Configuration Block)

### Endpoint
N/A (Configuration Block)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **target_platform** (string) - Required - Specifies the target platform (`windows` or `unix`), affecting the default `script_path`.
- **https** (boolean) - Optional - Set to `true` to connect using HTTPS instead of HTTP. Defaults to `false` for `winrm`.
- **insecure** (boolean) - Optional - Set to `true` to skip validating the HTTPS certificate chain. Defaults to `false` for `winrm`.
- **use_ntlm** (boolean) - Optional - Set to `true` to use NTLM authentication instead of basic authentication. Defaults to `false` for `winrm`.
- **cacert** (string) - Optional - Specifies the CA certificate to validate against. Defaults to `none` for `winrm`.
- **bastion_host** (string) - Optional - Specifies the address of the bastion host. Defaults to `none` for `ssh`.
- **bastion_host_key** (string) - Optional - Specifies the public key from the remote host or the signing CA to verify the host connection. Defaults to `none` for `ssh`.
- **bastion_port** (string) - Optional - Specifies the port number to use for the bastion host connection. Defaults to the value of the `port` field for `ssh`.
- **bastion_user** (string) - Optional - Specifies the user name for connecting to the bastion host. Defaults to the value of the `user` field for `ssh`.
- **bastion_password** (string) - Optional - Specifies the user password for connecting to the bastion host. Defaults to the value of the `password` field for `ssh`.
- **bastion_private_key** (string) - Optional - Specifies the contents of an SSH key file to use for the bastion host. Use a `file` function to load keys from file. Defaults to the value of the `private_key` field for `ssh`.
- **bastion_certificate** (string) - Optional - Specifies the contents of a signed CA certificate. You must also configure the `bastion_private_key` argument when providing the certificate for the bastion host. Use a `file` function to load certificates from file. Defaults to the value of the `certificate` field for `ssh`.
- **proxy_scheme** (string) - Optional - Specifies the connection protocol (`http`, `https`, `socks5`). Defaults to `none` for `ssh`.
- **proxy_host** (string) - Optional - Specifies the address of the proxy host. Defaults to `none` for `ssh`.
- **proxy_port** (number) - Optional - Specifies the port number to use for the proxy host connection. Defaults to `none` for `ssh`.
- **proxy_user_name** (string) - Optional - Specifies the user name for connecting to the proxy host. Defaults to `none` for `ssh`.
- **proxy_user_password** (string) - Optional - Specifies the user password for connecting to the proxy host. Defaults to `none` for `ssh`.

### Request Example
```json
{
  "target_platform": "unix",
  "https": false,
  "insecure": false,
  "use_ntlm": false,
  "cacert": null,
  "bastion_host": "bastion.example.com",
  "bastion_port": 2222,
  "proxy_scheme": "socks5",
  "proxy_host": "proxy.example.com",
  "proxy_port": 1080
}
```

### Response
#### Success Response (200)
This is a configuration block, no direct response.

#### Response Example
N/A
```

--------------------------------

### Clone Example Configuration with Git

Source: https://developer.hashicorp.com/terraform/tutorials/cli/cloud-migrate

Clones the example Terraform configuration from a GitHub repository. This configuration uses the `random` provider to generate a random pet name. No external dependencies are required beyond Git.

```bash
$ git clone https://github.com/hashicorp-education/learn-state-migration

```

--------------------------------

### Terraform Resource Structure and Initialization (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.10.x/deprecations

Defines the main structure for the example widget resource and provides a constructor function. It includes the necessary interface implementation for Terraform resources and imports from the plugin framework.

```go
package provider

import (
    "context"

    "github.com/hashicorp/terraform-plugin-framework/resource"
    "github.com/hashicorp/terraform-plugin-framework/resource/schema"
    "github.com/hashicorp/terraform-plugin-framework/types"
)

var _ resource.Resource = (*exampleWidgetResource)(nil)

type exampleWidgetResource struct{}

func NewWidgetResource() resource.Resource {
    return &exampleWidgetResource{}
}
```

--------------------------------

### GET /teams/:team_id/notification-configurations

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/notification-configurations

Retrieves a list of all notification configurations associated with a specific team. This endpoint is useful for auditing or managing existing notification setups.

```APIDOC
## GET /teams/:team_id/notification-configurations

### Description
Retrieves a list of all notification configurations associated with a specific team. This endpoint is useful for auditing or managing existing notification setups.

### Method
GET

### Endpoint
/api/v2/teams/:team_id/notification-configurations

### Parameters
#### Path Parameters
- **team_id** (string) - Required - The ID of the team to list configurations from.

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  https://app.terraform.io/api/v2/teams/team-6p5jTwJQXwqZBncC/notification-configurations
```

### Response
#### Success Response (200 OK)
- **data** (array) - A list of notification configuration objects.
  - Each object contains `id`, `type`, `attributes`, `relationships`, and `links` similar to the POST response.

#### Response Example
```json
{
  "data": [
    {
      "id": "nc-AeUQ2zfKZzW9TiGZ",
      "type": "notification-configurations",
      "attributes": {
        "enabled": true,
        "name": "Webhook server test",
        "url": "https://httpstat.us/200",
        "destination-type": "generic",
        "token": null,
        "triggers": [
          "change_request:created"
        ],
        "delivery-responses": [],
        "created-at": "2024-01-08T21:32:14.125Z",
        "updated-at": "2024-01-08T21:34:37.274Z"
      },
      "relationships": {
        "subscribable": {
          "data": {
            "id": "team-6p5jTwJQXwqZBncC",
            "type": "teams"
          }
        }
      },
      "links": {
        "self": "/api/v2/notification-configurations/nc-AeUQ2zfKZzW9TiGZ"
      }
    }
  ]
}
```
```

--------------------------------

### Create Workspace (with VCS Repository)

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/api-docs/workspaces

This example shows how to create a workspace linked to a VCS repository.

```APIDOC
## POST /api/v2/workspaces

### Description
Creates a new HCP Terraform workspace configured with a Version Control System (VCS) repository.

### Method
POST

### Endpoint
/api/v2/workspaces

### Parameters
#### Request Body
- **data** (object) - Required - The workspace object.
  - **attributes** (object) - Required - Workspace attributes.
    - **name** (string) - Required - The name of the workspace.
    - **terraform_version** (string) - Optional - The Terraform version to use.
    - **working-directory** (string) - Optional - The working directory within the VCS repository.
    - **vcs-repo** (object) - Optional - VCS repository configuration.
      - **identifier** (string) - Required - The VCS repository identifier (e.g., "owner/repo").
      - **oauth-token-id** (string) - Required - The ID of the OAuth token for VCS authentication.
      - **branch** (string) - Optional - The specific branch to use. If empty, the default branch is used.
      - **tags-regex** (string) - Optional - A regular expression to filter Git tags for triggering runs.
  - **type** (string) - Required - Must be "workspaces".

### Request Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-2",
      "terraform_version": "0.11.1",
      "working-directory": "",
      "vcs-repo": {
        "identifier": "example/terraform-test-proj",
        "oauth-token-id": "ot-hmAyP66qk2AMVdbJ",
        "branch": "",
        "tags-regex": null
      }
    },
    "type": "workspaces"
  }
}
```

### Response
#### Success Response (201 Created)
- **data** (object) - The created workspace object.
  - **attributes** (object) - Workspace attributes.
    - **name** (string) - The name of the workspace.
    - **terraform_version** (string) - The Terraform version used.
    - **working-directory** (string) - The working directory.
    - **vcs-repo** (object) - VCS repository configuration.
      - **identifier** (string) - The VCS repository identifier.
      - **oauth-token-id** (string) - The ID of the OAuth token.
      - **branch** (string) - The branch used.
      - **tags-regex** (string) - The regex for filtering Git tags.
  - **type** (string) - The type of the resource, "workspaces".

#### Response Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-2",
      "terraform_version": "0.11.1",
      "working-directory": "",
      "vcs-repo": {
        "identifier": "example/terraform-test-proj",
        "oauth-token-id": "ot-hmAyP66qk2AMVdbJ",
        "branch": "",
        "tags-regex": null
      }
    },
    "type": "workspaces"
  }
}
```
```

--------------------------------

### Terraform Enterprise Support Bundle Upload Structure Example

Source: https://developer.hashicorp.com/terraform/enterprise/deploy/reference/cli

This example illustrates the directory structure for uploaded support bundles, particularly for External Services, Active/Active, and Kubernetes installations. Bundles are organized by timestamp and then by node.

```text
support-bundles
└── 2020-11-10T02:03:05Z
    ├── 10.0.0.5
    │   └── 10.0.0.5-support-bundle-timestamp.tar.gz
    └── 10.0.0.6
        └── 10.0.0.6-support-bundle-timestamp.tar.gz
```

--------------------------------

### Terraform Protocol Version 6 Acceptance Test Example (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.2.x/migrating/mux

This Go code snippet demonstrates an acceptance test for verifying the muxing setup with Terraform Protocol Version 6. It utilizes `terraform-plugin-go` and `terraform-plugin-mux` to test the integration of different provider versions. The test case configures the `ProtoV6ProviderFactories` to include both a terraform-plugin-framework provider and an upgraded terraform-plugin-sdk provider.

```go
import (
    "context"
    "testing"

    "github.com/hashicorp/terraform-plugin-go/tfprotov6"
    "github.com/hashicorp/terraform-plugin-mux/tf5to6server"
    "github.com/hashicorp/terraform-plugin-mux/tf6muxserver"
    "github.com/hashicorp/terraform-plugin-testing/helper/resource"
)

func TestMuxServer(t *testing.T) {
    resource.Test(t, resource.TestCase{
        ProtoV6ProviderFactories: map[string]func() (tfprotov5.ProviderServer, error) {
            "examplecloud": func() (tfprotov6.ProviderServer, error) {
                ctx := context.Background()

                upgradedSdkServer, err := tf5to6server.UpgradeServer(
                    ctx,
                    Provider().GRPCProvider, // Example terraform-plugin-sdk provider
                )

                if err != nil {
                    return nil, err
                }

                providers := []func() tfprotov6.ProviderServer{
                    providerserver.NewProtocol6(New()), // Example terraform-plugin-framework provider
                    func() tfprotov6.ProviderServer {
                        return upgradedSdkServer,
                    },
                }

                muxServer, err := tf6muxserver.NewMuxServer(ctx, providers...)

                if err != nil {
                    return nil, err
                }

                return muxServer.ProviderServer(), nil
            },
        },
        Steps: []resource.TestStep{
            {
                Config: "... configuration including simplest data source or managed resource",
            },
        },
    })
}

```

--------------------------------

### GitHub App Installation APIs

Source: https://developer.hashicorp.com/terraform/enterprise/v202401-2/api-docs/changelog

Introduces new GitHub App Installation APIs and updates existing APIs to accept `vcs-repo.github-app-installation-id` for connecting to GitHub App Installations.

```APIDOC
## GitHub App Installation APIs

### Description
APIs for managing GitHub App Installations and integrating them with Terraform Cloud resources like workspaces, registry modules, and policy sets.

### Method
POST, GET, PUT, DELETE (depending on the specific endpoint)

### Endpoint
/github-app-installations, /workspaces, /registry/modules, /policy-sets

### Parameters
#### Request Body (for relevant endpoints)
- **vcs-repo.github-app-installation-id** (string) - Optional - The ID of the GitHub App Installation to associate with the resource.

### Request Example (Connect Workspace to GitHub App Installation)
```json
{
  "name": "my-workspace",
  "vcs-repo": {
    "identifier": "myorg/myrepo",
    "github-app-installation-id": "gh-app-install-123"
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Resource successfully connected to GitHub App Installation."
}
```
```

--------------------------------

### Example Error: Airgap Package Version Mismatch

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/replicated/administration/license/update-tfe-license

This error signifies that the airgap installation package version does not align with the currently installed version of Terraform Enterprise. This can lead to various operational issues and requires updating to a compatible airgap file.

```log
installed app release (325b33bf0ad539c994644423128cad5e:502) does not match the airgap package
```

--------------------------------

### Install Custom Provider Binary in Terraform < 0.13

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/run/install-software

For Terraform versions prior to 0.13, custom or community providers must be installed manually. This involves placing the compiled provider binary in the `terraform.d/plugins/linux_amd64/` directory relative to the working directory root. Ensure the plugin has read and execute permissions. Alternatively, providers can be added as Git submodules and symlinked.

```shell
mkdir -p terraform.d/plugins/linux_amd64/
# Assume <PLUGIN NAME> is the correct name for your provider
cp /path/to/your/provider terraform.d/plugins/linux_amd64/<PLUGIN NAME>
chmod +x terraform.d/plugins/linux_amd64/<PLUGIN NAME>
```

--------------------------------

### Instantiate Kubernetes Web App Deployment Construct in Python

Source: https://developer.hashicorp.com/terraform/cdktf/v0.12.x/concepts/constructs

This Python code shows how to use the `KubernetesWebAppDeployment` construct. It sets up the Kubernetes provider and then creates an instance of the construct, specifying the image, replica count, and application details. It requires `constructs`, `cdktf`, and the Kubernetes provider.

```python
from constructs import Construct
import cdktf
import os
import imports.kubernetes as kubernetes
from my_constructs import KubernetesWebAppDeployment


class MyStack(cdktf.TerraformStack):
    def __init__(self, scope: Construct, name: str):
        super().__init__(scope, name)
        kubernetes.KubernetesProvider(self, "kind",
                                      config_path=os.path.join(os.path.dirname(
                                          __file__), '..', 'kubeconfig.yaml')
                                      )

        KubernetesWebAppDeployment(self, "deployment",
                                   image="nginx:latest",
                                   replicas=2,
                                   app="myapp",
                                   component="frontend",
                                   environment="dev"
                                   )


app = cdktf.App()
MyStack(app, "demo")

app.synth()

```

--------------------------------

### Navigate to Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/functions

Changes the current directory to the cloned 'learn-terraform-functions' repository. This step is necessary to access and use the example configuration files.

```bash
$ cd learn-terraform-functions

```

--------------------------------

### SFTP Configuration and Script Setup

Source: https://developer.hashicorp.com/terraform/enterprise/v202409-1/admin/infrastructure/automated-recovery

This script sets up the necessary variables for SFTP access, including the key file, host, and user. It also sets up error handling and other configurations for the script.

```bash
#!/bin/bash

set -e -u -o pipefail

key_file=path_to_your_ssh_key
key="$(base64 -w0 \"$key_file\")"
host=sftp_server_hostname_or_ip
user=user_to_sftp_on_the_remote_server

access="--store sftp --sftp-host $host --sftp-user $user --sftp-key $key"
```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/custom-conditions

This command initializes a Terraform working directory. It downloads provider plugins, initializes the backend, and prepares the configuration for use. This is typically the first step before running other Terraform commands like `plan` or `apply`.

```bash
$ terraform init
Initializing modules...
- app in modules/example-app-deployment
Downloading registry.terraform.io/terraform-aws-modules/security-group/aws 4.9.0 for app.app_security_group...
- app.app_security_group in .terraform/modules/app.app_security_group/modules/web
- app.app_security_group.sg in .terraform/modules/app.app_security_group
Downloading registry.terraform.io/terraform-aws-modules/elb/aws 3.0.1 for app.elb_http...
- app.elb_http in .terraform/modules/app.elb_http
- app.elb_http.elb in .terraform/modules/app.elb_http/modules/elb
- app.elb_http.elb_attachment in .terraform/modules/app.elb_http/modules/elb_attachment
Downloading registry.terraform.io/terraform-aws-modules/security-group/aws 4.9.0 for app.lb_security_group...
- app.lb_security_group in .terraform/modules/app.lb_security_group/modules/web
- app.lb_security_group.sg in .terraform/modules/app.lb_security_group
Downloading registry.terraform.io/terraform-aws-modules/vpc/aws 3.14.0 for vpc...
- vpc in .terraform/modules/vpc

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/aws v4.10.0...
- Installed hashicorp/aws v4.10.0 (signed by HashiCorp)
- Installing hashicorp/random v3.1.3...
- Installed hashicorp/random v3.1.3 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform, 
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### SDKv2 Managed Resource Definition (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework-benefits

An example of a managed resource definition using SDKv2's declarative struct approach. This example is missing 'Read' and 'Delete' definitions, which would only be caught at runtime, requiring additional testing.

```go
// Example managed resource definition.
&schema.Resource{
  Schema: map[string]*schema.Schema{ /* ... */ },
  CreateContext: func(ctx context.Context, d *schema.ResourceData, meta any) diag.Diagnostics { /* ... */ },
  // Missing Read and Delete
}

```

--------------------------------

### Clone AFT Module Configuration Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/aws/aws-control-tower-aft

Clones the example repository containing the AFT module configuration from GitHub. This is the first step in setting up the project.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-aws-control-tower-aft 

```

--------------------------------

### Example Warning: Airgap License Mismatch

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/replicated/administration/license/update-tfe-license

This is an example of a warning message that might appear in the 'docker logs replicated' output. It indicates that the license file detected in the airgap installation directory does not match the license currently active within the Replicated system.

```log
WARN 2021-02-22T01:40:00+00:00 tasks/app_tasksteps.go:113 Airgap license on disk does not match installed license
```

--------------------------------

### Apply Terraform Configuration and Verify Output

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/data-sources/terraform-workflow%3Ahcp_variants=terraform-workflow%3Acommunity

This snippet shows the command-line output of applying a Terraform configuration, including the plan, confirmation prompt, and successful apply. It also demonstrates how to retrieve an output value (load balancer URL) using `terraform output -raw` and then use it with `curl` to verify the application response.

```bash
$ terraform apply
##...

Plan: 10 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + lb_url             = (known after apply)
  + web_instance_count = 4

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

##...

Apply complete! Resources: 10 added, 0 changed, 0 destroyed.

Outputs:

lb_url = "http://lb-DOf-tutorial-example-1971328425.us-west-2.elb.amazonaws.com/"
web_instance_count = 4

$ curl $(terraform output -raw lb_url)
<html><body><div>Hello, world!</div></body></html>
```

--------------------------------

### Terraform Provider Lock Command Example

Source: https://developer.hashicorp.com/terraform/language/v1.11.x/files/dependency-lock

This command allows users to pre-populate checksum hashes for a specified set of platforms when installing Terraform providers. This is useful for avoiding ongoing additions of new 'h1:' hashes when working with configurations on new target platforms or when installing providers from mirrors.

```shell
terraform providers lock \
  -platform=linux_arm64 \
  -platform=linux_amd64 \
  -platform=darwin_amd64 \
  -platform=windows_amd64
```

```shell
terraform providers lock \
  -platform=linux_arm64 \
  -platform=linux_amd64 \
  -platform=darwin_amd64 \
  -platform=windows_amd64
```

--------------------------------

### Implement Terraform Provider Interface in Go

Source: https://developer.hashicorp.com/terraform/plugin/framework/v0.10.x/providers

This Go code demonstrates how to implement the `tfsdk.Provider` interface for a Terraform provider. It includes the definition of an `exampleProvider` struct and its required methods: `GetSchema`, `Configure`, `GetDataSources`, and `GetResources`. This implementation is crucial for defining the provider's schema and handling its configuration, data sources, and resources.

```go
// Ensure the implementation satisfies the tfsdk.Provider interface.
var _ tfsdk.Provider = &exampleProvider{}

// exampleProvider implements the tfsdk.Provider interface. This implementation
// will be passed to data sources and resources as the tfsdk.Provider parameter
// in each NewDataSource and NewResource method call respectively.
type exampleProvider struct{
    // Typically fields including API clients or configuration necessary for
    // resource and data source operations. For example:
    Client exampleApiClient

    // version is an example field that can be set with an actual provider
    // version on release, "dev" when the provider is built and ran locally,
    // and "test" when running acceptance testing.
    Version string
}

// GetSchema satisfies the tfsdk.Provider interface for exampleProvider.
func (p *exampleProvider) GetSchema(ctx context.Context) (tfsdk.Schema, diag.Diagnostics) {
    return tfsdk.Schema{
        Attributes: map[string]tfsdk.Attribute{
            // Provider specific implementation.
        },
    }, nil
}

// Configure satisfies the tfsdk.Provider interface for exampleProvider.
func (p *exampleProvider) Configure(ctx context.Context, req tfsdk.ConfigureProviderRequest, resp *tfsdk.ConfigureProviderResponse) {
    // Provider specific implementation.
}

// GetDataSources satisfies the tfsdk.Provider interface for exampleProvider.
func (p *exampleProvider) GetDataSources(ctx context.Context) (map[string]tfsdk.DataSourceType, diag.Diagnostics) {
    return map[string]tfsdk.DataSourceType{
        // Provider specific implementation
    }, nil
}

// GetResources satisfies the tfsdk.Provider interface for exampleProvider.
func (p *exampleProvider) GetResources(ctx context.Context) (map[string]tfsdk.ResourceType, diag.Diagnostics) {
    return map[string]tfsdk.ResourceType{
        // Provider specific implementation
    }, nil
}

```

--------------------------------

### Install Software and CA Certificates on Red Hat Enterprise Linux 7 for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This Dockerfile snippet configures a Red Hat Enterprise Linux 7 minimal image for Terraform Enterprise. It installs required packages using `microdnf`, downloads and makes the `envdir` tool executable, and integrates custom CA certificates using `update-ca-trust`.

```dockerfile
FROM registry.access.redhat.com/ubi7/ubi-minimal:latest

# Update installed packages and clear cache.
RUN microdnf --assumeyes update && \
    rm --recursive --force /var/cache/yum

# Install required software for Terraform Enterprise.
RUN microdnf --assumeyes install curl git iproute nmap-ncat openssh openssl psmisc sudo unzip wget && \
    microdnf clean all && \
    curl --location --output /usr/local/bin/envdir https://github.com/jezdez/envdir/releases/download/0.7/envdir-0.7.pyz && \
    chmod +x /usr/local/bin/envdir

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/share/pki/ca-trust-source/anchors
ADD example-intermediate-ca.crt /usr/share/pki/ca-trust-source/anchors
RUN update-ca-trust

```

```dockerfile
FROM registry.access.redhat.com/ubi7/ubi-minimal:latest

# Update installed packages and clear cache.
RUN microdnf --assumeyes update && \
    rm --recursive --force /var/cache/yum

# Install required software for Terraform Enterprise.
RUN microdnf --assumeyes install curl git iproute nmap-ncat openssh openssl psmisc sudo unzip wget && \
    microdnf clean all && \
    curl --location --output /usr/local/bin/envdir https://github.com/jezdez/envdir/releases/download/0.7/envdir-0.7.pyz && \
    chmod +x /usr/local/bin/envdir

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/share/pki/ca-trust-source/anchors
ADD example-intermediate-ca.crt /usr/share/pki/ca-trust-source/anchors
RUN update-ca-trust

```

--------------------------------

### Example: Auth0 OIDC Auth Method Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Ahcp

This is a complete Terraform configuration example for setting up an OIDC auth method for Auth0 within HashiCorp Boundary. It includes the provider configuration and the `boundary_auth_method_oidc` resource with example values for Auth0. Remember to update the 'updateme' comments with your specific details.

```terraform
terraform {
  required_providers {
    boundary = {
      source  = "hashicorp/boundary"
      version = "1.0.12"
    }
  }
}

provider "boundary" {
  addr                            = "BOUNDARY_ADDR" # updateme
  auth_method_id                  = "ampw_1234567890"    # updateme
  password_auth_method_login_name = "myuser"             # updateme
  password_auth_method_password   = "passpass"           # updateme
}

resource "boundary_auth_method_oidc" "provider" {
  name               = "Auth0"
  description        = "OIDC auth method for Auth0"
  scope_id           = "o_1234567890"                    # updateme
  issuer             = "https://dev-1vdl8c0q.us.auth0.com/"   # updateme
  client_id          = "YOUR_AUTH0_CLIENT_ID"             # updateme
  client_secret      = "YOUR_AUTH0_CLIENT_SECRET"         # updateme
  signing_algorithms = ["RS256"]
  api_url_prefix     = "https://e58fe114-7624-431c-994d-b6670e90b03J.boundary.hashicorp.cloud"
}

resource "boundary_account_oidc" "user" {
  name           = "my-auth0-user"
  description    = "OIDC account for my Auth0 user"
  auth_method_id = boundary_auth_method_oidc.provider.id
  issuer         = "https://dev-1vdl8c0q.us.auth0.com/"
  subject        = "YOUR_AUTH0_USER_ID" # updateme
}
```

--------------------------------

### CDKTF Configuration File Example

Source: https://developer.hashicorp.com/terraform/cdktf/v0.10.x/cli-reference/commands

An example of a `cdktf.json` configuration file. This file specifies the application's language ('typescript'), the entry point for the app ('node main.js'), and a list of Terraform providers to be used ('aws@~> 2.0'). This configuration is used by the `cdktf get` command.

```json
{
  "language": "typescript",
  "app": "node main.js",
  "terraformProviders": ["aws@~> 2.0"]
}
```

--------------------------------

### Deploy Kubernetes Web App (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.16.x/concepts/constructs

Deploys a web application to Kubernetes using the `KubernetesWebAppDeployment` construct in Go. It configures the image, replicas, app name, component, and environment. This requires the `cdktf-cli` and relevant providers.

```go
kubernetes.NewKubernetesProvider(stack, jsii.String("kind"), &kubernetes.KubernetesProviderConfig{
    ConfigPath: jsii.String(path.Join(cwd, "kubeconfig.yaml")),
})
myconstructs.NewKubernetesWebAppDeployment(stack, "deployment", map[string]interface{}{
    "image":       jsii.String("nginx:latest"),
    "replicas":    jsii.Number(2),
    "app":         jsii.String("myapp"),
    "component":   jsii.String("frontend"),
    "environment": jsii.String("dev"),
})

return stack
}

func main() {
app := cdktf.NewApp(nil)

NewConstructsStack(app, "constructs")

app.Synth()
}
```

--------------------------------

### GitHub App Installation APIs

Source: https://developer.hashicorp.com/terraform/enterprise/v202307-1/api-docs/changelog

New APIs have been introduced for managing GitHub App Installations.

```APIDOC
## POST /api/github-app-installations

### Description
Create a new GitHub App installation.

### Method
POST

### Endpoint
/api/github-app-installations

### Request Body
[Request body details for creating a GitHub App installation]
```

--------------------------------

### Instantiate Kubernetes Web App Deployment Construct in Java

Source: https://developer.hashicorp.com/terraform/cdktf/v0.16.x/concepts/constructs

This Java code demonstrates the usage of the KubernetesWebAppDeployment construct. It initializes the Kubernetes provider and deploys a web application, configuring parameters such as image, replica count, application name, component, and environment.

```java
import java.nio.file.Paths;
import imports.kubernetes.provider.KubernetesProvider;
import imports.kubernetes.provider.KubernetesProviderConfig;
import com.mycompany.app.myconstructs.KubernetesWebAppDeployment;
import com.mycompany.app.myconstructs.KubernetesWebAppDeploymentConfig;
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
import { App } from "cdktf";


public class MainUseConstructs extends TerraformStack {

    public MainUseConstructs(Construct scope, String name){
        super(scope, name);

        new KubernetesProvider(this, "kind", KubernetesProviderConfig.builder() 
                .configPath(Paths.get(System.getProperty("user.dir"), "..", "kubeconfig.yaml").toString())
                .build()
        );

        new KubernetesWebAppDeployment(this, "deployment",  KubernetesWebAppDeploymentConfig.builder() 
                .image("nginx:latest")
                .replicas(2)
                .app("myapp")
                .components("frontend")
                .environments("dev")
                .build()
        );
    }

    public static void main(String[] args) {
        final App app = new App();
        new MainUseConstructs(app, "demo");
        app.synth();
    }
}

```

--------------------------------

### GET /api/v2/admin/users

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/api-docs/admin/users

Lists all user accounts in the Terraform Enterprise installation. This endpoint is exclusive to Terraform Enterprise and can only be used by administrators.

```APIDOC
## GET /api/v2/admin/users

### Description
Lists all user accounts in the Terraform Enterprise installation. This endpoint is exclusive to Terraform Enterprise and can only be used by administrators.

### Method
GET

### Endpoint
/api/v2/admin/users

### Query Parameters
#### Query Parameters
- **q** (string) - Optional. A search query string. Users are searchable by username and email address.
- **filter[admin]** (string) - Optional. Can be "true" or "false" to show only administrators or non-administrators.
- **filter[suspended]** (string) - Optional. Can be "true" or "false" to show only suspended users or users who are not suspended.
- **page[number]** (integer) - Optional. If omitted, the endpoint will return the first page.
- **page[size]** (integer) - Optional. If omitted, the endpoint will return 20 users per page.

### Available Related Resources
This GET endpoint can optionally return related resources, if requested with the `include` query parameter. The following resource types are available:
- **organizations**: A list of organizations that each user is a member of.

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  "https://app.terraform.io/api/v2/admin/users"
```

### Response
#### Success Response (200)
- **data** (array) - An array of user objects.
  - **id** (string) - The unique identifier for the user.
  - **type** (string) - The resource type, always "users".
  - **attributes** (object) - Contains user attributes.
    - **username** (string) - The user's username.
    - **email** (string) - The user's email address.
    - **avatar-url** (string) - The URL for the user's avatar.
    - **is-admin** (boolean) - Indicates if the user is an administrator.
    - **is-suspended** (boolean) - Indicates if the user account is suspended.
    - **is-service-account** (boolean) - Indicates if the user is a service account.
  - **relationships** (object) - Contains relationships to other resources.
    - **organizations** (object) - A list of organizations the user is a member of.
      - **data** (array) - An array of organization objects.
        - **id** (string) - The organization ID.
        - **type** (string) - The resource type, always "organizations".
  - **links** (object) - Links related to the user resource.
    - **self** (string) - The URL for the user's self-link.
- **links** (object) - Links for pagination.
  - **self** (string) - The URL for the current page.
  - **first** (string) - The URL for the first page.
  - **prev** (string | null) - The URL for the previous page.
  - **next** (string | null) - The URL for the next page.
  - **last** (string) - The URL for the last page.
- **meta** (object) - Metadata about the response.
  - **pagination** (object) - Pagination details.
    - **current-page** (integer) - The current page number.
    - **prev-page** (integer | null) - The previous page number.
    - **next-page** (integer | null) - The next page number.
    - **total-pages** (integer) - The total number of pages.
    - **total-count** (integer) - The total number of users.
  - **status-counts** (object) - Counts of users by status.
    - **total** (integer) - Total number of users.
    - **suspended** (integer) - Number of suspended users.
    - **admin** (integer) - Number of administrator users.

#### Response Example
```json
{
  "data": [
    {
      "id": "user-ZL4MsEKnd6iTigTb",
      "type": "users",
      "attributes": {
        "username": "myuser",
        "email": "myuser@example.com",
        "avatar-url": "https://www.gravatar.com/avatar/3a23b75d5aa41029b88b73f47a0d90db?s=100&d=mm",
        "is-admin": true,
        "is-suspended": false,
        "is-service-account": false
      },
      "relationships": {
        "organizations": {
          "data": [
            {
              "id": "my-organization",
              "type": "organizations"
            }
          ]
        }
      },
      "links": {
        "self": "/api/v2/users/myuser"
      }
    }
  ],
  "links": {
    "self": "https://app.terraform.io/api/v2/admin/users?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://app.terraform.io/api/v2/admin/users?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": null,
    "last": "https://app.terraform.io/api/v2/admin/users?page%5Bnumber%5D=1&page%5Bsize%5D=20"
  },
  "meta": {
    "pagination": {
      "current-page": 1,
      "prev-page": null,
      "next-page": null,
      "total-pages": 1,
      "total-count": 1
    },
    "status-counts": {
      "total": 1,
      "suspended": 0,
      "admin": 1
    }
  }
}
```

#### Error Response (404)
- **error** (object) - JSON API error object indicating the client is not an administrator.
```

--------------------------------

### Clone GitHub Repository for Terraform Modules

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-create

Clones the specified GitHub repository to your local machine. This is the first step to get the example configuration for creating Terraform modules.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-modules-create

```

--------------------------------

### Launch Demo Web Application (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/provision/cloud-init

This command executes the GoLang web application demo within the SSH session on the provisioned instance. The application will print the instance's public IP address and continue running. Access the application by navigating to the instance's IP address on port 8080 in a web browser.

```shell
$ ~/go/bin/learn-go-webapp-demo
54.196.121.30

```

--------------------------------

### In-House Provider Binary Location (v0.13+)

Source: https://developer.hashicorp.com/terraform/enterprise/run/install-software

This example illustrates the directory structure required for manually installing an in-house provider binary for Terraform 0.13 and later. The compiled provider should be placed at a specific path relative to the configuration root, matching the source details.

```shell
terraform.d/plugins/<SOURCE HOST>/<SOURCE NAMESPACE>/<PLUGIN NAME>/<VERSION>/linux_amd64/
```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/provider-versioning

Initializes a Terraform working directory, downloading provider plugins and setting up the backend. This command is essential before running other Terraform commands like `plan` or `apply`. Rerun if modules or backend configuration change.

```bash
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/aws v4.5.0...
- Installed hashicorp/aws v4.5.0 (signed by HashiCorp)
- Installing hashicorp/random v3.1.0...
- Installed hashicorp/random v3.1.0 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Terraform Apply and Output Example

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/data-sources/terraform-workflow%3Ahcp

This snippet shows the command-line output of a `terraform apply` operation, including the plan, confirmation prompt, and the final apply complete message with generated outputs like `lb_url` and `web_instance_count`.

```bash
$ terraform apply
##...

Plan: 10 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + lb_url             = (known after apply)
  + web_instance_count = 4

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

##...

Apply complete! Resources: 10 added, 0 changed, 0 destroyed.

Outputs:

lb_url = "http://lb-DOf-tutorial-example-1971328425.us-west-2.elb.amazonaws.com/"
web_instance_count = 4
```

--------------------------------

### Start Terraform Agent with Environment Variables (Bash)

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/v1.10.x/agents

This snippet shows how to start the Terraform Cloud agent using bash. It requires setting the TFC_AGENT_TOKEN and optionally TFC_AGENT_NAME environment variables before executing the agent binary. Ensure the agent binaries are in the current directory or in your PATH.

```bash
export TFC_AGENT_TOKEN=your-token
export TFC_AGENT_NAME=your-agent-name
./tfc-agent
```

--------------------------------

### Terraform Apply Example

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/configure-providers/three-cloud-providers%3Aaws_variants=three-cloud-providers%3Aaws

Demonstrates the output of `terraform apply` when creating AWS S3 buckets. It shows the plan, user confirmation prompt, and resource creation status.

```bash
$ terraform apply
module.website_east.data.aws_region.current: Reading...
module.website_east.data.aws_caller_identity.current: Reading...
module.website_east.data.aws_partition.current: Reading...
module.website_east.data.aws_partition.current: Read complete after 0s [id=aws]

## ...

Terraform used the selected providers to generate the following execution plan. Resource
actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_s3_bucket.cloudfront_logs will be created
  + resource "aws_s3_bucket" "cloudfront_logs" {
      + acceleration_status         = (known after apply)
      + acl                         = (known after apply)
      + arn                         = (known after apply)

## ...

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_s3_bucket.cloudfront_logs: Creating...
aws_s3_bucket.cloudfront_logs: Creation complete after 3s [id=terraform-cloudfront-logs-20250729164952700100000001]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

```

--------------------------------

### Show a User - GET Request Example (Terraform Cloud API)

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-3/api-docs/users

This code snippet demonstrates how to make a GET request to the Terraform Cloud API to retrieve details for a specific user. It requires an authorization token and specifies the content type as application/vnd.api+json. The user ID is included in the URL.

```curl
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/users/user-MA4GL63FmYRpSFxa

```

--------------------------------

### Clone Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/functions

Clones the 'learn-terraform-functions' repository from GitHub, which contains example configurations for practicing Terraform functions. This is a prerequisite for the tutorial.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-functions

```

--------------------------------

### Initialize Terraform with New Provider Configurations

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/configure-providers/three-cloud-providers%3Agcp

This command output shows the result of running `terraform init` after adding new provider configurations or modules. It details the initialization process, including backend setup, module downloads, and provider plugin installation, confirming that Terraform is ready to manage the defined infrastructure.

```bash
$ terraform init
Initializing the backend...
Initializing modules...
Downloading registry.terraform.io/terraform-google-modules/cloud-storage/google 11.0.0 for gcs_bucket_east...
- gcs_bucket_east in .terraform/modules/gcs_bucket_east
Initializing provider plugins...
- Reusing previous version of hashicorp/google from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Using previously-installed hashicorp/google v6.46.0
- Using previously-installed hashicorp/random v3.7.2

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### CDKTF Get Command with Parallelism Limit

Source: https://developer.hashicorp.com/terraform/cdktf/cli-reference/commands

This example demonstrates how to use the `--parallelism` option with the `cdktf get` command to limit the number of provider or module bindings generated concurrently. This can be useful for managing resource usage or avoiding issues when generating a large number of bindings.

```bash
cdktf get --parallelism 1
```

--------------------------------

### Initialize Project with Local Backend (CLI)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.11.x/create-and-deploy/project-setup

Initializes a new CDKTF project and configures it to use a local backend for Terraform state storage. All Terraform operations will be performed on the local machine.

```bash
cdktf init --template="typescript" --local
```

```bash
cdktf init --template="typescript" --local
```

--------------------------------

### Clone Spotify Playlist Terraform Example (Git)

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/spotify-playlist

Clones the example Terraform configuration repository for creating a Spotify playlist. This repository contains the necessary Terraform files to search for songs and build a playlist.

```git
$ git clone https://github.com/hashicorp-education/learn-terraform-spotify
```

--------------------------------

### Organize Provider Documentation Directory Structure

Source: https://developer.hashicorp.com/terraform/registry/providers/docs

This example illustrates a typical directory structure for a Terraform provider's documentation. It includes the main index file, a 'guides' directory for user guides, and directories for different resource types like 'actions', 'data-sources', 'ephemeral-resources', 'functions', 'list-resources', and 'resources'.

```directory
docs/
    index.md
    guides/
        authenticating.md
    actions/
        stop_instance.md
    data-sources/
        instance.md
    ephemeral-resources/
        auth_token.md
    functions/
        parse_instance_id.md
    list-resources/
        instance.md
    resources/
        instance.md
```

--------------------------------

### Terraform Module Installation Directory Structure

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-use/terraform-workflow%3Alab

Illustrates the directory structure created by Terraform after initializing or getting modules. This includes the 'ec2_instances' and 'vpc' modules, along with a 'modules.json' file.

```file structure
.terraform/modules/
├── ec2_instances
├── modules.json
└── vpc

```

--------------------------------

### Initialize Terraform pg Backend

Source: https://developer.hashicorp.com/terraform/language/v1.4.x/backend/pg

These examples demonstrate how to initialize the Terraform pg backend. The first shows a direct initialization with a connection string, while the second illustrates using the `-backend-config` flag for providing the connection string, which is a more secure approach for sensitive data.

```bash
terraform init -backend-config="conn_str=postgres://user:pass@db.example.com/terraform_backend"
```

```bash
terraform init -backend-config="conn_str=postgres://localhost/terraform_backend?sslmode=disable"
```

--------------------------------

### Install jq and Terraform, Restore Snapshot via SFTP

Source: https://developer.hashicorp.com/terraform/enterprise/v202503-1/deploy/replicated/administration/infrastructure/automated-recovery

This script installs jq, installs Terraform, retrieves a list of snapshots from an SFTP server, identifies the latest snapshot, and restores it. It uses SFTP for storage and waits for the application to boot after restoration.  It requires an SSH key for SFTP access.

```bash
#!/bin/bash

set -e -u -o pipefail

key_file=path_to_your_ssh_key
key="$(base64 -w0 \"$key_file\")"
host=sftp_server_hostname_or_ip
user=user_to_sftp_on_the_remote_server

access="--store sftp --sftp-host $host --sftp-user $user --sftp-key $key"

# jq is used by this script, so install it. For other Linux distros, either preinstall jq
# and remove these lines, or change to the mechanism your distro uses to install jq.

apt-get update
apt-get install -y jq

# Run the installer.

curl https://install.terraform.io/ptfe/stable | bash -s fast-timeouts

# Wait for replicated to start before proceeding
until replicatedctl system status --template '{{and (eq .Replicated \"ready\") (eq .Retraced \"ready\"}}' | grep -q true; do
  sleep 1
  echo "Replicated is not yet ready."
done
echo "Replicated is ready."

# This retrieves a list of all the snapshots currently available.
replicatedctl snapshot ls $access -o json > /tmp/snapshots.json

# Pull just the snapshot id out of the list of snapshots
id=$(jq -r 'sort_by(.finished) | .[-1].id // \"\"' /tmp/snapshots.json)

# If there are no snapshots available, exit out
if test \"$id\" = \"\"; then
  echo "No snapshots found"
  exit 1
fi

echo "Restoring snapshot: $id"

# Restore the detected snapshot. This ignores preflight checks to be sure the application
# is booted.
replicatedctl snapshot restore $access --dismiss-preflight-checks \"$id\"

# Wait until the application reports itself as running. This step can be removed if
# something upstream is prepared to wait for the application to finish booting.
until curl -f -s --connect-timeout 1 http://localhost/_health_check; do
  sleep 1
done

echo
echo "Application booted!"

```

--------------------------------

### Install Terraform on Fedora using dnf

Source: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Installs Terraform on Fedora Linux. This process involves installing `dnf-plugins-core` to manage repositories, adding the official HashiCorp repository, and then installing Terraform using dnf. This is the recommended method for Fedora.

```bash
$ sudo dnf install -y dnf-plugins-core
$ sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/fedora/hashicorp.repo
$ sudo dnf -y install terraform
```

--------------------------------

### Export Airgap Package Path (CLI)

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/admin/infrastructure/upgrades

Exports the AirgapPackagePath parameter using the replicatedctl command-line tool. This path is where airgap packages should be placed for installation.

```bash
$ replicatedctl params export --template '{{.AirgapPackagePath}}'

```

--------------------------------

### Implement Terraform Resource Example Widget Create Function (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/best-practices/deprecations

Implements the Create function for the 'example_widget' Terraform resource. It handles the logic for adding either 'existing_attribute' or 'new_attribute' to the provider API call, ensuring at least one is configured.

```go
func resourceExampleWidgetCreate(d *schema.ResourceData, meta any) error {
    // ... other logic ...

    existingAttribute, existingAttributeOk := d.GetOk("existing_attribute")
    newAttribute, newAttributeOk := d.GetOk("new_attribute")
    if !existingAttributeOk && !newAttributeOk {
        return errors.New("one of existing_attribute or new_attribute must be configured")
    }
    if existingAttributeOk {
        // add existingAttribute to provider create API call
    } else {
        // add newAttribute to provider create API call
    }

    // ... other logic ...
    return resourceExampleWidgetRead(d, meta)
}
```

--------------------------------

### GET /api/v2/notification-configurations

Source: https://developer.hashicorp.com/terraform/enterprise/v202311-1/api-docs/notification-configurations

Retrieves a list of all notification configurations associated with the authenticated user's account. This endpoint allows fetching details about various notification setups, such as Slack or webhook integrations.

```APIDOC
## GET /api/v2/notification-configurations

### Description
Retrieves a list of all notification configurations. This endpoint allows fetching details about various notification setups, such as Slack or webhook integrations.

### Method
GET

### Endpoint
/api/v2/notification-configurations

### Parameters
#### Query Parameters
- **filter[workspace]** (string) - Optional - Filters notification configurations by a specific workspace ID.
- **page[size]** (integer) - Optional - Specifies the number of results per page.
- **page[number]** (integer) - Optional - Specifies the page number for pagination.

### Request Example
```
GET /api/v2/notification-configurations?filter[workspace]=ws-XdeUVMWShTesDMME
```

### Response
#### Success Response (200)
- **data** (array) - An array of notification configuration objects.
  - **id** (string) - The unique identifier for the notification configuration.
  - **type** (string) - The type of the resource, always "notification-configurations".
  - **attributes** (object) - Contains the details of the notification configuration.
    - **enabled** (boolean) - Indicates if the notification configuration is currently enabled.
    - **name** (string) - The name of the notification configuration.
    - **url** (string) - The URL or endpoint where notifications will be sent.
    - **destination-type** (string) - The type of destination (e.g., "slack", "generic").
    - **token** (string) - The authentication token for the destination (may be null).
    - **triggers** (array of strings) - A list of events that trigger notifications.
    - **delivery-responses** (array) - Details of past delivery attempts and responses.
    - **created-at** (string) - The timestamp when the configuration was created.
    - **updated-at** (string) - The timestamp when the configuration was last updated.
  - **relationships** (object) - Information about related resources.
    - **subscribable** (object) - Details about the subscribable resource (e.g., workspace).
      - **data** (object) - Contains the ID and type of the subscribable resource.
  - **links** (object) - Links related to the notification configuration.
    - **self** (string) - The URL of the specific notification configuration resource.

#### Response Example
```json
{
  "data": [
    {
      "id": "nc-W6VGEi8A7Cfoaf4K",
      "type": "notification-configurations",
      "attributes": {
        "enabled": false,
        "name": "Slack: #devops",
        "url": "https://hooks.slack.com/services/T00000000/BC012345/0PWCpQmYyD4bTTRYZ53q4w",
        "destination-type": "slack",
        "token": null,
        "triggers": [
          "run:errored",
          "run:needs_attention"
        ],
        "delivery-responses": [],
        "created-at": "2019-01-08T21:34:28.367Z",
        "updated-at": "2019-01-08T21:34:28.367Z"
      },
      "relationships": {
        "subscribable": {
          "data": {
            "id": "ws-XdeUVMWShTesDMME",
            "type": "workspaces"
          }
        }
      },
      "links": {
        "self": "/api/v2/notification-configurations/nc-W6VGEi8A7Cfoaf4K"
      }
    }
  ]
}
```
```

--------------------------------

### Navigate to Terraform Example Repository Directory

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/refresh

Changes the current directory to the cloned Terraform example repository. This step is necessary to access and modify the configuration files for the tutorial.

```bash
cd learn-terraform-refresh
```

--------------------------------

### API Resource Inclusion Example

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/admin

Shows how to use the `include` query parameter to fetch related resources along with a primary resource. The included resources are returned in an `included` section of the response. This is useful for reducing the number of API calls needed to retrieve related data.

```shell
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/teams/team-n8UQ6wfhyym25sMe?include=users

```

```shell
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/teams/team-n8UQ6wfhyym25sMe?include=users

```

--------------------------------

### Define Custom Role for Team Membership in AAD Manifest

Source: https://developer.hashicorp.com/terraform/enterprise/v202211-1/saml/idp-configuration/aad

This JSON example demonstrates how to define a custom role within the Azure Active Directory application manifest. This role, named 'Dev' in this example, maps users to a specific team in Terraform Enterprise. The 'id' must be a unique GUID.

```json
{
  "allowedMemberTypes": [
    "User"
  ],
  "displayName": "Dev",
  "id": "d1c2ade8-98f8-45fd-aa4a-6d06b947c66f",
  "isEnabled": true,
  "description": "Dev Team",
  "value": "Dev"
}
```

--------------------------------

### Get Map Keys - Terraform

Source: https://developer.hashicorp.com/terraform/language/configuration-0-11/interpolation

The `keys` function returns a lexically sorted list of all keys present in a given map. Example: `keys(var.my_map)`.

```Terraform
keys(var.my_map)
```

--------------------------------

### Test Provider with Protocol Version 5 (Framework)

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/testing

Illustrates writing a test for a provider using protocol version 5 with the Terraform Plugin Framework. This example uses `resource.UnitTest` and `ProtoV5ProviderFactories`.

```go
resource.UnitTest(t, resource.TestCase{
    ProtoV5ProviderFactories: protoV5ProviderFactories(),


```

```go
resource.UnitTest(t, resource.TestCase{
    ProtoV5ProviderFactories: protoV5ProviderFactories(),


```

--------------------------------

### Navigate to Terraform Example Directory

Source: https://developer.hashicorp.com/terraform/tutorials/cli/init

Changes the current directory to the 'learn-terraform-init' folder after cloning. This command is essential for running subsequent Terraform commands within the context of the cloned project.

```bash
$ cd learn-terraform-init
```

--------------------------------

### Navigate to rfc3339_parse Example Directory in Terraform

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This command navigates the user to the specific directory containing the rfc3339_parse function example within the Terraform project. It is a prerequisite for applying the configuration.

```bash
cd examples/functions/rfc3339_parse
```

--------------------------------

### Run Terraform Enterprise Pod

Source: https://developer.hashicorp.com/terraform/enterprise/v202406-1/flexible-deployments/install/podman/install

Starts a Terraform Enterprise pod using a pre-configured YAML file. Replace '<path_to_YAML_file>' with the actual path to your configuration file.

```shell
# podman play kube <path_to_YAML_file>
```

--------------------------------

### Establish MySQL Session with Boundary Connect

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

This snippet illustrates establishing a session to a MySQL target using 'boundary connect -exec'. It executes the 'SHOW DATABASES;' command via the proxy, showing proxy details and a warning about using passwords on the command line. The {{boundary.port}} is substituted with the active proxy port.

```bash
$ boundary connect -exec mysql -target-name mysql -target-scope-name databases -- -h 127.0.0.1 -P {{boundary.port}} --protocol=tcp -uroot -p"my-secret-pw" --execute="SHOW DATABASES;"

Proxy listening information:
  Address:             127.0.0.1
  Connection Limit:    -1
  Expiration:          Mon, 04 Oct 2021 17:57:15 MDT
  Port:                51958
  Protocol:            tcp
  Session ID:          s_DdWBdvTp6Z
mysql: [Warning] Using a password on the command line interface can be insecure.
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+

```

--------------------------------

### HCL Configuration for Random Provider

Source: https://developer.hashicorp.com/terraform/cdktf/v0.13.x/create-and-deploy/project-setup

An example of an HCL configuration defining the 'random' provider and a 'random_pet' resource. This configuration is used as input for conversion to a CDKTF project.

```hcl
# File: /tmp/demo/main.tf

terraform {
  required_providers {
    random = {
      source = "hashicorp/random"
      version = "3.1.0"
    }
  }
}

provider "random" {
}

resource "random_pet" "server" {
}

```

```hcl
# File: /tmp/demo/main.tf

terraform {
  required_providers {
    random = {
      source = "hashicorp/random"
      version = "3.1.0"
    }
  }
}

provider "random" {
}

resource "random_pet" "server" {
}

```

--------------------------------

### Initialize New Typescript CDKTF Project

Source: https://developer.hashicorp.com/terraform/cdktf/cli-reference/commands

Initializes a new CDKTF project using the 'typescript' template. This is a basic setup for starting a new project with TypeScript.

```bash
cdktf init --template="typescript"
```

--------------------------------

### Update Replicated Proxy Settings (Shell)

Source: https://developer.hashicorp.com/terraform/enterprise/v202212-1/install/interactive/installer

This snippet demonstrates how to update the proxy settings for Replicated services after installation by modifying configuration files. It involves adding HTTP_PROXY and NO_PROXY environment variables to the `REPLICATED_OPTS` or `REPLICATED_OPERATOR_OPTS` variables. Ensure to include necessary local and instance-specific addresses in the NO_PROXY list.

```shell
# Example for /etc/sysconfig/replicated or /etc/default/replicated
# Add to the line with REPLICATED_OPTS:
# -e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>

# Example for /etc/sysconfig/replicated-operator or /etc/default/replicated-operator
# Add to the line with REPLICATED_OPERATOR_OPTS:
# -e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>

# Note: The NO_PROXY list should include 127.0.0.1,<DOCKER0 INTERFACE IP>,<IP ADDRESS OF TFE INSTANCE>,<HOSTNAME OF TFE INSTANCE>
```

--------------------------------

### Terraform Framework Data Access Examples

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/benefits

Demonstrates how the Terraform Framework simplifies data access by providing distinct request and response types for each operation (Create, Read, Update, Delete). This approach clearly delineates available data (Config, Plan, State) for each stage, reducing ambiguity.

```go
func (r ThingResource) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
  req.Config // configuration data
  req.Plan // plan data
  // No req.State as it is always null
  // No resp.Config as configuration cannot be set by provider during creation
  // No resp.Plan as plan cannot be set by provider during creation
  resp.State // new state data to save
}

func (r ThingResource) Read(ctx context.Context, req resource.ReadRequest, resp *resource.CreateResponse) {
  // No req.Config as configuration cannot be read by provider during read
  // No req.Plan as there is no plan during read
  req.State // prior state data
  // No resp.Config as configuration cannot be set by provider during read
  // No resp.Plan as there is no plan during read
  resp.State // new state data to save
}

func (r ThingResource) Update(ctx context.Context, req resource.UpdateRequest, resp *resource.UpdateResponse) {
  req.Config // configuration data
  req.Plan // plan data
  req.State // prior state data
  // No resp.Config as configuration cannot be set by provider during update
  // No resp.Plan as plan cannot be set by provider during update
  resp.State // new state data to save
}

func (r ThingResource) Delete(ctx context.Context, req resource.DeleteRequest, resp *resource.DeleteResponse) {
  // No req.Config as configuration cannot be read by provider during delete
  // No req.Plan as it is always null
  req.State // prior state data
  // No resp.Config as configuration cannot be set by provider during delete
  // No resp.Plan as plan cannot be set by provider during delete
}

```

--------------------------------

### Service Discovery Document Example

Source: https://developer.hashicorp.com/terraform/internals/module-registry-protocol

An example of a service discovery document for a host implementing the module registry protocol. This JSON document maps the service identifier 'modules.v1' to its base URL.

```json
{
  "modules.v1": "/terraform/modules/v1/"
}
```

--------------------------------

### Clone Example Repository for No-Code Module Tutorial

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/no-code-provisioning

Clone the example repository for the no-code module tutorial and navigate to the directory. This step is crucial for setting up the local environment to work with the module.

```bash
git clone git@github.com:USER/terraform-aws-rds.git
cd terraform-aws-rds
```

--------------------------------

### Start HCP Terraform Agent with Environment Variables

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/v1.16.x/agents

This snippet shows how to start the HCP Terraform agent by setting the agent token and an optional agent name as environment variables. The agent then connects to the specified HCP Terraform agent pool. Ensure the `tfc-agent` binary is in your PATH or specify its full path.

```bash
export TFC_AGENT_TOKEN=your-token
export TFC_AGENT_NAME=your-agent-name
./tfc-agent
```

```bash
export TFC_AGENT_TOKEN=your-token
export TFC_AGENT_NAME=your-agent-name
./tfc-agent
```

--------------------------------

### Navigate to Repository Directory

Source: https://developer.hashicorp.com/terraform/internals/lifecycle

Changes the current directory to the cloned Terraform example repository. This step is necessary to execute Terraform commands within the project context. Requires a file system.

```bash
$ cd learn-terraform-lifecycle-management
```

--------------------------------

### Terraform substr Function Example: Basic Usage

Source: https://developer.hashicorp.com/terraform/language/v1.10.x/functions/substr

Demonstrates a simple use case of the 'substr' function, extracting a substring starting from a specific offset with a defined length.

```hcl
> substr("hello world", 1, 4)
ell
```

--------------------------------

### Clone Terraform Azure AD Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/azure/entra-id

Clones the example repository containing Terraform configurations for creating new users in an Entra ID tenant. After cloning, navigate into the cloned directory.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-azure-ad
$ cd learn-terraform-azure-ad
```

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-azure-ad
$ cd learn-terraform-azure-ad
```

--------------------------------

### Generate Updated Example Widget Resource Configuration (Go)

Source: https://developer.hashicorp.com/terraform/plugin/testing/v1.7.x/testing-patterns

This Go function generates a Terraform configuration string for an updated example_widget resource. It takes a name as input and returns a formatted string suitable for acceptance tests. This is often used as a superset of basic tests.

```go
package main

import "fmt"

// testAccExampleResourceUpdated returns an configuration for an Example Widget with the provided name
func testAccExampleResourceUpdated(name string) string {
    return fmt.Sprintf(
        `resource "example_widget" "foo" {
  active = false
  name = "%s" 
}`, name)
}
```

--------------------------------

### Terraform Input Variable Validation Example

Source: https://developer.hashicorp.com/terraform/language/checks

This example demonstrates how to use the `validation` block within a Terraform variable definition to enforce specific format requirements for input variables. It checks if the provided `image_id` string starts with 'ami-' and has a minimum length. If the condition fails, Terraform will display the custom error message and halt the operation.

```terraform
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}

```

--------------------------------

### Example Terraform Configuration Directory Structure

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-create

Illustrates the expected directory layout after creating the module directories. This structure is essential for Terraform to locate and use the module.

```text
.
├── LICENSE
├── README.md
├── main.tf
├── modules
│   └── aws-s3-static-website-bucket
├── outputs.tf
├── terraform.tfstate
├── terraform.tfstate.backup
└── variables.tf

```

--------------------------------

### GET /api/v1/nodes

Source: https://developer.hashicorp.com/terraform/enterprise/api-docs/nodes

Retrieves a list of all node IDs available in the Terraform Enterprise installation. These IDs can be used to target specific nodes in other API calls.

```APIDOC
## GET /api/v1/nodes

### Description
Retrieves a list of all node IDs available in the Terraform Enterprise installation. You can use these node IDs to target specific nodes for any endpoint that supports filtering of nodes.

### Method
GET

### Endpoint
/api/v1/nodes

### Parameters
#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --request GET \
  https://tfe.example.com:8443/api/v1/nodes
```

### Response
#### Success Response (200)
- **data** (array) - An array of node ID strings. The format of node IDs depends on the deployment environment (e.g., Container ID for Docker, Pod name for Kubernetes).
- **links** (object) - Contains a link to the self resource.
  - **self** (string) - The URL for the current resource.

#### Response Example
```json
{
  "data": [
    "node-id-1",
    "node-id-2",
    "node-id-3"
  ],
  "links": {
    "self": "/api/v1/nodes"
  }
}
```

### Error Handling
- **401** - JSON API error object: Authentication required.
- **500** - JSON API error object: Internal server error.
```

--------------------------------

### Create Nginx Deployment using CDKTF (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/resources

This Go code snippet demonstrates how to create an Nginx deployment using the CDKTF library. It defines a namespace and a deployment resource with metadata and specification, including container details. Dependencies include the `namespace` and `deployment` modules.

```go
package main

import (
	"github.com/aws/constructs-go/constructs/v10"
	"github.com/hashicorp/cdktf-provider-kubernetes-go/kubernetes/v2"
	"github.com/hashicorp/terraform-cdk-go/cdktf"
	"cdk.tf/examples/go/namespace"
	"cdk.tf/examples/go/deployment"
)

func main() {
	app := cdktf.NewApp(nil)

	stack := cdktf.NewTerraformStack(app, jsii.String("tf-cdk-example"))

	// Example: Creating a namespace
	exampleNamespace := namespace.NewNamespace(stack, jsii.String("tf-cdk-example"), &namespace.NamespaceConfig{
		Metadata: &namespace.NamespaceMetadata{
			Name: jsii.String("tf-cdk-example"),
		},
	})

	// Example: Creating an Nginx deployment
	deployment.NewDeployment(stack, jsii.String("nginx-deployment"), &deployment.DeploymentConfig{
		Metadata: &deployment.DeploymentMetadata{
			Name:      jsii.String("nginx"),
			Namespace: exampleNamespace.Metadata().Name(), // Reference the name property
			Labels: &map[string]*string{
					"app": jsii.String("my-app"),
				},
		},
		Spec: &deployment.DeploymentSpec{
			Template: &deployment.DeploymentSpecTemplate{
					Metadata: &deployment.DeploymentSpecTemplateMetadata{
						Labels: &map[string]*string{
							"app": jsii.String("my-app"),
						},
					},
					Spec: &deployment.DeploymentSpecTemplateSpec{
						Container: []deployment.DeploymentSpecTemplateSpecContainer{
							{
								Name:  jsii.String("nginx"),
								Image: jsii.String("nginx:1.7.9"),
							},
						},
					},
				},
			},
		},
	})

	cdktf.NewTerraformOutput(stack, jsii.String("output"), &cdktf.TerraformOutputConfig{
		Value: jsii.String("hello world"),
	})

	app.Synth()
}

```

--------------------------------

### Get Terraform Enterprise License Information

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/admin/infrastructure/admin-cli

This command displays the license information and the current workspace count for the Terraform Enterprise installation. It is a straightforward command with no configurable parameters.

```bash
tfe-admin license-info
```

--------------------------------

### Install jq and Terraform, Restore Snapshot via SFTP

Source: https://developer.hashicorp.com/terraform/enterprise/v202312-1/replicated/administration/infrastructure/automated-recovery

This bash script installs jq, installs Terraform, retrieves a list of snapshots from an SFTP server, and restores the latest snapshot. It uses `replicatedctl` to interact with the snapshots and waits for the application to boot after restoration. The script requires an SSH key for SFTP access.

```bash
```bash
#!/bin/bash

set -e -u -o pipefail

key_file=path_to_your_ssh_key
key="$(base64 -w0 \"$key_file\")"
host=sftp_server_hostname_or_ip
user=user_to_sftp_on_the_remote_server

access="--store sftp --sftp-host $host --sftp-user $user --sftp-key $key"

# jq is used by this script, so install it. For other Linux distros, either preinstall jq
# and remove these lines, or change to the mechanism your distro uses to install jq.

apt-get update
apt-get install -y jq

# Run the installer.

curl https://install.terraform.io/ptfe/stable | bash -s fast-timeouts

# Wait for replicated to start before proceeding
until replicatedctl system status --template '{{and (eq .Replicated \"ready\") (eq .Retraced \"ready\")}}' | grep -q true; do
  sleep 1
  echo "Replicated is not yet ready."
done
echo "Replicated is ready."

# This retrieves a list of all the snapshots currently available.
replicatedctl snapshot ls $access -o json > /tmp/snapshots.json

# Pull just the snapshot id out of the list of snapshots
id=$(jq -r 'sort_by(.finished) | .[-1].id // \"\"' /tmp/snapshots.json)

# If there are no snapshots available, exit out
if test \"$id\" = \"\"; then
  echo "No snapshots found"
  exit 1
fi

echo "Restoring snapshot: $id"

# Restore the detected snapshot. This ignores preflight checks to be sure the application
# is booted.
replicatedctl snapshot restore $access --dismiss-preflight-checks \"$id\"

# Wait until the application reports itself as running. This step can be removed if
# something upstream is prepared to wait for the application to finish booting.
until curl -f -s --connect-timeout 1 http://localhost/_health_check; do
  sleep 1
done

echo
echo "Application booted!"
```
```

```bash
```bash
#!/bin/bash

set -e -u -o pipefail

key_file=path_to_your_ssh_key
key="$(base64 -w0 \"$key_file\")"
host=sftp_server_hostname_or_ip
user=user_to_sftp_on_the_remote_server

access="--store sftp --sftp-host $host --sftp-user $user --sftp-key $key"

# jq is used by this script, so install it. For other Linux distros, either preinstall jq
# and remove these lines, or change to the mechanism your distro uses to install jq.

apt-get update
apt-get install -y jq

# Run the installer.

curl https://install.terraform.io/ptfe/stable | bash -s fast-timeouts

# Wait for replicated to start before proceeding
until replicatedctl system status --template '{{and (eq .Replicated \"ready\") (eq .Retraced \"ready\")}}' | grep -q true; do
  sleep 1
  echo "Replicated is not yet ready."
done
echo "Replicated is ready."

# This retrieves a list of all the snapshots currently available.
replicatedctl snapshot ls $access -o json > /tmp/snapshots.json

# Pull just the snapshot id out of the list of snapshots
id=$(jq -r 'sort_by(.finished) | .[-1].id // \"\"' /tmp/snapshots.json)

# If there are no snapshots available, exit out
if test \"$id\" = \"\"; then
  echo "No snapshots found"
  exit 1
fi

echo "Restoring snapshot: $id"

# Restore the detected snapshot. This ignores preflight checks to be sure the application
# is booted.
replicatedctl snapshot restore $access --dismiss-preflight-checks \"$id\"

# Wait until the application reports itself as running. This step can be removed if
# something upstream is prepared to wait for the application to finish booting.
until curl -f -s --connect-timeout 1 http://localhost/_health_check; do
  sleep 1
done

echo
echo "Application booted!"
```
```

--------------------------------

### Terraform fileset Function Examples

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/functions/fileset

Demonstrates various ways to use the `fileset` function with different patterns like `*`, `**`, and `{alternative1,...}`. These examples show how to list files in a directory, including nested ones with `**`.

```Terraform
> fileset(path.module, "files/*.txt")
[
  "files/hello.txt",
  "files/world.txt",
]

> fileset(path.module, "files/{hello,world}.txt")
[
  "files/hello.txt",
  "files/world.txt",
]

> fileset("${path.module}/files", "*")
[
  "hello.txt",
  "world.txt",
]

> fileset("${path.module}/files", "**")
[
  "hello.txt",
  "world.txt",
  "subdirectory/anotherfile.txt",
]
```

--------------------------------

### Install Terraform on Fedora

Source: https://developer.hashicorp.com/terraform/tutorials/oci-get-started/install-cli

Installs Terraform on Fedora Linux. This process requires installing dnf-plugins-core, adding the HashiCorp repository, and then installing Terraform.

```bash
$ sudo dnf install -y dnf-plugins-core
# Note: The command to add the repo and install terraform for Fedora is missing from the provided text.
```

--------------------------------

### Clone GCP Terraform Repository using Git

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-deploy

Clones the GCP Terraform example repository from GitHub. Requires a GitHub username and Git installed locally. This command fetches the repository content to your local machine.

```bash
$ git clone https://github.com/USER/learn-terraform-stacks-deploy-gcp
```

--------------------------------

### Initialize Terraform Configuration with New Providers

Source: https://developer.hashicorp.com/terraform/tutorials/aws/aws-cloud-control

This command `terraform init` is used to initialize the Terraform working directory. It downloads and installs the providers specified in the configuration, including the newly added `awscc` and `random` providers. This step is crucial after modifying the `terraform` block or adding new providers to ensure Terraform can access and use them.

```bash
$ terraform init
Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/awscc...
- Reusing previous version of hashicorp/random from the dependency lock file
- Reusing previous version of hashicorp/aws from the dependency lock file
- Installing hashicorp/random v3.1.0...
- Installed hashicorp/random v3.1.0 (signed by HashiCorp)
- Using previously-installed hashicorp/aws v3.59.0
```

--------------------------------

### Clone Azure Terraform Repository using Git

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-deploy

Clones the Azure Terraform example repository from GitHub. Requires a GitHub username and Git installed locally. This command fetches the repository content to your local machine.

```bash
$ git clone https://github.com/USER/learn-terraform-stacks-deploy-azure
```

--------------------------------

### Create Workspace (Basic)

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/api-docs/workspaces

This example shows the basic payload for creating a workspace without a VCS repository or tags.

```APIDOC
## POST /api/v2/workspaces

### Description
Creates a new HCP Terraform workspace.

### Method
POST

### Endpoint
/api/v2/workspaces

### Parameters
#### Request Body
- **data** (object) - Required - The workspace object.
  - **attributes** (object) - Required - Workspace attributes.
    - **name** (string) - Required - The name of the workspace.
  - **type** (string) - Required - Must be "workspaces".

### Request Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-1"
    },
    "type": "workspaces"
  }
}
```

### Response
#### Success Response (201 Created)
- **data** (object) - The created workspace object.
  - **attributes** (object) - Workspace attributes.
    - **name** (string) - The name of the workspace.
  - **type** (string) - The type of the resource, "workspaces".

#### Response Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-1"
    },
    "type": "workspaces"
  }
}
```
```

--------------------------------

### Clone AWS Terraform Repository using Git

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-deploy

Clones the AWS Terraform example repository from GitHub. Requires a GitHub username and Git installed locally. This command fetches the repository content to your local machine.

```bash
$ git clone https://github.com/USER/learn-terraform-stacks-deploy-aws
```

--------------------------------

### Implement Provider Type - Go

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This Go code defines the `ExampleTimeProvider` which implements the `provider.Provider` and `provider.ProviderWithFunctions` interfaces. It includes methods for metadata, schema, configuration, data sources, resources, and functions, serving as a template for custom Terraform providers.

```go
package provider

import (
    "context"

    "github.com/hashicorp/terraform-plugin-framework/datasource"
    "github.com/hashicorp/terraform-plugin-framework/function"
    "github.com/hashicorp/terraform-plugin-framework/provider"
    "github.com/hashicorp/terraform-plugin-framework/provider/schema"
    "github.com/hashicorp/terraform-plugin-framework/resource"
)

// Ensure the implementation satisfies the expected interfaces.
var (
    _ provider.Provider = &ExampleTimeProvider{}
    _ provider.ProviderWithFunctions = &ExampleTimeProvider{}
)

// New is a helper function to simplify provider server and testing implementation.
func New(version string) func() provider.Provider {
    return func() provider.Provider {
        return &ExampleTimeProvider{
            version: version,
        }
    }
}

// ExampleTimeProvider is the provider implementation.
type ExampleTimeProvider struct {
    // version is set to the provider version on release, "dev" when the
    // provider is built and ran locally, and "test" when running acceptance
    // testing.
    version string
}

// Metadata returns the provider type name.
func (p *ExampleTimeProvider) Metadata(_ context.Context, _ provider.MetadataRequest, resp *provider.MetadataResponse) {
    resp.TypeName = "exampletime"
    resp.Version = p.version
}

// Schema defines the provider-level schema for configuration data.
func (p *ExampleTimeProvider) Schema(_ context.Context, _ provider.SchemaRequest, resp *provider.SchemaResponse) {
    resp.Schema = schema.Schema{}
}

// Configure prepares an API client for data sources and resources.
func (p *ExampleTimeProvider) Configure(ctx context.Context, req provider.ConfigureRequest, resp *provider.ConfigureResponse) {
}

// DataSources defines the data sources implemented in the provider.
func (p *ExampleTimeProvider) DataSources(_ context.Context) []func() datasource.DataSource {
    return nil
}

// Resources defines the resources implemented in the provider.
func (p *ExampleTimeProvider) Resources(_ context.Context) []func() resource.Resource {
    return nil
}

// Functions defines the functions implemented in the provider.
func (p *ExampleTimeProvider) Functions(_ context.Context) []func() function.Function {
    return nil
}

```

--------------------------------

### Terraform Splat Expression Example

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/expressions

Demonstrates splat expressions (e.g., `var.list[*].id`) which extract simpler collections from more complex expressions, like getting a list of IDs from a list of resources.

```terraform
resource "aws_instance" "web" {
  count = 2
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

output "instance_ids" {
  value = aws_instance.web[*].id
}
```

--------------------------------

### Instantiate Kubernetes Web App Deployment Construct in Python

Source: https://developer.hashicorp.com/terraform/cdktf/v0.16.x/concepts/constructs

This Python code shows how to import and use the KubernetesWebAppDeployment construct. It sets up the Kubernetes provider and creates a web application deployment with specific configurations for image, replicas, application name, component, and environment.

```python
from constructs import Construct
from cdktf import App, TerraformStack
from constructs.kubernetes_web_app_deployment import KubernetesWebAppDeployment
from providers.kubernetes.provider import KubernetesProvider
import os


class MyKubernetesStack(TerraformStack):
    def __init__(self, scope: Construct, name: str):
        super().__init__(scope, name)
        KubernetesProvider(self, "kind",
            config_path=os.path.join(os.path.dirname(__file__), '..', 'kubeconfig.yaml')
        )

        KubernetesWebAppDeployment(self, "deployment",
            image="nginx:latest",
            replicas=2,
            app="myapp",
            component="frontend",
            environment="dev"
        )



app = App()
MyKubernetesStack(app, "demo")
app.synth()

```

--------------------------------

### Create Directory and File for Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Adev_variants=boundary-deploy%3Adev

These commands create a new directory named 'learn-boundary-oidc' and change into it. Then, they create an empty Terraform configuration file named 'main.tf' within that directory. This sets up the environment for managing Boundary resources with Terraform.

```bash
$ mkdir learn-boundary-oidc && cd learn-boundary-oidc/ 
$ touch main.tf
```

--------------------------------

### Terraform Enterprise Docker Compose Configuration

Source: https://developer.hashicorp.com/terraform/enterprise/v202406-1/flexible-deployments/install/docker/install

Example Docker Compose configuration for Terraform Enterprise, including settings for Redis, Vault, ports, and volumes. This configuration is a foundational setup for running TFE in a containerized environment.

```yaml
TFE_REDIS_USE_TLS: "<To use tls? e.g. false>"
TFE_REDIS_USE_AUTH: "<To use customized credential to authenticate? e.g. false>"

# Vault cluster settings.
# If you are using the default internal vault, this should be the private routable IP address of the node itself.
TFE_VAULT_CLUSTER_ADDRESS: "https://<private_ip_of_the_node>:8201"
cap_add:
  - IPC_LOCK
read_only: true
tmpfs:
  - /tmp:mode=01777
  - /run
  - /var/log/terraform-enterprise
ports:
  - "80:80"
  - "443:443"
  - "8201:8201"
volumes:
  - type: bind
    source: /var/run/docker.sock
    target: /run/docker.sock
  - type: bind
    source: ./certs
    target: /etc/ssl/private/terraform-enterprise
  - type: volume
    source: terraform-enterprise-cache
    target: /var/cache/tfe-task-worker/terraform
volumes:
  terraform-enterprise-cache:

```

--------------------------------

### Example Terraform Enterprise Settings JSON Output

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/install/automated/automating-the-installer

This is an example of the JSON output generated by `replicatedctl app-config export` for an instance configured in 'Mounted Disk' mode. It includes various configuration parameters such as disk path, hostname, and capacity settings. Note that parameters without a 'value' key can be omitted when creating a custom settings file.

```json
{
  "aws_access_key_id": {},
  "aws_instance_profile": {},
  "aws_secret_access_key": {},
  "azure_account_key": {},
  "azure_account_name": {},
  "azure_client_id": {},
  "azure_container": {},
  "azure_endpoint": {},
  "azure_use_msi": {},
  "backup_token": {},
  "ca_certs": {},
  "capacity_concurrency": {
    "value": "10"
  },
  "capacity_cpus": {},
  "capacity_memory": {
    "value": "512"
  },
  "custom_image_tag": {
    "value": "hashicorp/build-worker:now"
  },
  "disk_path": {
    "value": "/opt/terraform-enterprise"
  },
  "enable_active_active": {},
  "enc_password": {
    "value": "CHANGEME"
  },
  "extern_vault_addr": {},
  "extern_vault_enable": {},
  "extern_vault_namespace": {},
  "extern_vault_path": {},
  "extern_vault_propagate": {},
  "extern_vault_role_id": {},
  "extern_vault_secret_id": {},
  "extern_vault_token_renew": {},
  "extra_no_proxy": {},
  "force_tls": {},
  "gcs_bucket": {},
  "gcs_credentials": {},
  "gcs_project": {},
  "hairpin_addressing": {},
  "hostname": {
    "value": "terraform.example.org"
  },
  "iact_subnet_list": {},
  "iact_subnet_time_limit": {},
  "log_forwarding_config": {},
  "log_forwarding_enabled": {},
  "metrics_endpoint_enabled": {},
  "metrics_endpoint_port_http": {},
  "metrics_endpoint_port_https": {},
  "pg_dbname": {},
  "pg_extra_params": {},
  "pg_netloc": {},
  "pg_password": {},
  "pg_user": {},
  "placement": {},
  "production_type": {
    "value": "disk"
  },
  "redis_host": {},
  "redis_pass": {},
  "redis_port": {},
  "redis_use_password_auth": {},
  "redis_use_tls": {},
  "restrict_worker_metadata_access": {},
  "s3_bucket": {},
  "s3_endpoint": {},
  "s3_region": {},
  "s3_sse": {},
  "s3_sse_kms_key_id": {},
  "tbw_image": {
    "value": "default_image"
  },
  "tls_ciphers": {},
  "tls_vers": {
    "value": "tls_1_2_tls_1_3"
  }
}
```

--------------------------------

### Terraform Provider Installation Path for In-House Providers

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/run/install-software

This example illustrates the directory structure required for manually placing compiled in-house provider binaries. The path must follow the format `terraform.d/plugins/<SOURCE HOST>/<SOURCE NAMESPACE>/<PLUGIN NAME>/<VERSION>/<OS>_<ARCH>`, allowing Terraform to discover and use the custom provider.

```filepath
terraform.d/plugins/my-host/my-namespace/custom/1.0.0/linux_amd64/terraform-provider-custom
```

--------------------------------

### Terraform Provider Resource Structure and Initialization (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.14.x/deprecations

Defines the 'exampleWidgetResource' struct and provides a constructor function 'NewWidgetResource'. It also implements the Metadata function to set the resource type name.

```go
var _ resource.Resource = (*exampleWidgetResource)(nil)

type exampleWidgetResource struct{}

func NewWidgetResource() resource.Resource {
    return &exampleWidgetResource{}
}

func (e *exampleWidgetResource) Metadata(_ context.Context, req resource.MetadataRequest, resp *resource.MetadataResponse) {
    resp.TypeName = req.ProviderTypeName + "_widget"
}
```

--------------------------------

### Custom Dockerfile for Terraform Enterprise Worker (Ubuntu)

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/install/interactive/installer

This Dockerfile defines a custom image for Terraform Enterprise worker containers, based on Ubuntu. It installs necessary software packages like git, awscli, and ca-certificates, and includes a mechanism to add custom CA certificates. This allows runs to utilize tools not present in the default image.

```dockerfile
# This Dockerfile builds the image used for the worker containers.
FROM ubuntu:bionic

# Install required software for Terraform Enterprise.
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    sudo unzip daemontools git-core awscli ssh wget curl psmisc iproute2 openssh-client redis-tools netcat-openbsd ca-certificates

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/local/share/ca-certificates/
ADD example-intermediate-ca.crt /usr/local/share/ca-certificates/
```

--------------------------------

### Terraform Apply Command and Output Example

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/count

This demonstrates the command to apply Terraform configurations and shows a sample output after a successful apply. The output includes the instance IDs of the provisioned EC2 instances, the public DNS name of the load balancer, and the ARN of the VPC.

```bash
$ terraform apply
## ...

Apply complete! Resources: 8 added, 0 changed, 4 destroyed.

Outputs:

instance_ids = [
  "i-0bc4309c117df766a",
  "i-0aaa6de2b610ae749",
  "i-035ff2723aace0f12",
  "i-02640c564d3f08152",
]
public_dns_name = "lb-yksg-client-webapp-dev-702243816.us-west-2.elb.amazonaws.com"
vpc_arn = "arn:aws:ec2:us-west-2:561656980159:vpc/vpc-0195a5982b1ad302b"

```

--------------------------------

### Deploy Kubernetes Web App with Terraform CDK (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.12.x/concepts/constructs

This Go code snippet illustrates the initialization of a Terraform CDK application, configuration of the Kubernetes provider with a local kubeconfig file path, and deployment of a web application using the KubernetesWebAppDeployment construct. It specifies deployment parameters like image, replicas, and environment.

```go
package main

import (
    "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/kubernetes"
    "github.com/hashicorp/terraform-cdk/examples/go/documentation/myconstructs"
    "github.com/aws/constructs-go/constructs/v10"
    "github.com/aws/jsii-runtime-go"
    "github.com/hashicorp/terraform-cdk-go/cdktf"

    "os"
    "path"
)

func NewExampleCdktfDocumentationStack(scope constructs.Construct, name string) cdktf.TerraformStack {
    stack := cdktf.NewTerraformStack(scope, &name)

    cwd, _ := os.Getwd()

    kubernetes.NewKubernetesProvider(stack, jsii.String("kind"), &kubernetes.KubernetesProviderConfig{
        ConfigPath: jsii.String(path.Join(cwd, "kubeconfig.yaml")),
    })
    myconstructs.NewKubernetesWebAppDeployment(stack, "deployment", map[string]interface{}{
        "image":       jsii.String("nginx:latest"),
        "replicas":    jsii.Number(2),
        "app":         jsii.String("myapp"),
        "component":   jsii.String("frontend"),
        "environment": jsii.String("dev"),
    })

    return stack
}

func main() {
    app := cdktf.NewApp(nil)

    NewExampleCdktfDocumentationStack(app, "demo")

    app.Synth()
}
```

--------------------------------

### Main Application Entry Point (Python)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.20.x/concepts/providers

This Python code snippet shows the main application setup for the Terraform CDK. It creates an App instance, instantiates the stack, and synthesizes the Terraform configuration.

```python
from cdktf import App

app = App()
ProviderStack(app, "provider-stack")
app.synth()
```

--------------------------------

### Get Terraform IP Ranges using cURL

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/ip-ranges

This snippet demonstrates how to retrieve HCP Terraform's IP ranges using the cURL command-line tool. It includes the necessary GET request and an example of the If-Modified-Since header for conditional requests. The response contains IP ranges in CIDR notation for API, notifications, sentinel, and VCS.

```shell
curl \
  --request GET \
  -H "If-Modified-Since: Tue, 26 May 2020 15:10:05 GMT" \
  https://app.terraform.io/api/meta/ip-ranges
```

```shell
curl \
  --request GET \
  -H "If-Modified-Since: Tue, 26 May 2020 15:10:05 GMT" \
  https://app.terraform.io/api/meta/ip-ranges
```

--------------------------------

### Create S3 Buckets and Objects with Go Iterators

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/iterators

This Go code snippet demonstrates the equivalent functionality to the C# example, creating S3 buckets and objects using CDKTF. It defines a local configuration, iterates to create buckets, and uploads files, showcasing Go syntax for CDKTF resources and iterators.

```go
config := cdktf.NewTerraformLocal(stack, jsii.String("config-local"), []map[string]interface{}{
    {
        "name": "website-static-files",
        "tags": map[string]string{"app": "website"},
    },
    {
        "name": "images",
        "tags": map[string]string{"app": "image-converter"},
    },
})

s3BucketConfigurationIterator := cdktf.TerraformIterator_FromList(config.Expression())
s3Buckets := s3bucket.NewS3Bucket(stack, jsii.String("complex-iterator-buckets"), &s3bucket.S3BucketConfig{
    ForEach: s3BucketConfigurationIterator,
    Bucket:  s3BucketConfigurationIterator.GetString(jsii.String("name")),
    Tags:    s3BucketConfigurationIterator.GetStringMap(jsii.String("tags")),
})

s3BucketsIterator := cdktf.TerraformIterator_FromResources(s3Buckets)
helpFile := cdktf.NewTerraformAsset(stack, jsii.String("help"), &cdktf.TerraformAssetConfig{
    Path: jsii.String("./help"),
})
s3bucketobject.NewS3BucketObject(stack, jsii.String("object"), &s3bucketobject.S3BucketObjectConfig{
    ForEach: s3BucketsIterator,
    Bucket:  s3BucketsIterator.GetString(jsii.String("id")),
    Key:     jsii.String("help"),
    Source:  helpFile.Path(),
})
```

--------------------------------

### Update Replicated Service Proxy Settings in Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This snippet shows how to update proxy settings for Replicated services after Terraform Enterprise installation. It involves editing configuration files and adding proxy environment variables to the REPLICATED_OPTS or REPLICATED_OPERATOR_OPTS lines. This ensures that Replicated and its operator can correctly handle proxy configurations for outbound connections and exclusions.

```bash
# Example for replicated file:
# REPLICATED_OPTS="-e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>"
# Example for replicated-operator file:
# REPLICATED_OPERATOR_OPTS="-e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>"
```

--------------------------------

### Clone Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/cli/apply_utm_offer=ARTICLE_PAGE

Clones the 'learn-terraform-apply' repository from GitHub to your local machine. This repository contains example Terraform configurations for creating an EC2 instance.

```bash
# Clone the learn-terraform-apply repository
$ git clone https://github.com/hashicorp-education/learn-terraform-apply

```

--------------------------------

### Create and Navigate to Terraform Verification Directory

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-provider

Sets up a new directory for testing the local provider installation and changes the current working directory to it. This prepares the environment for creating the Terraform configuration file.

```bash
mkdir examples/provider-install-verification && cd "$_"
```

--------------------------------

### List All Organizations - cURL Example

Source: https://developer.hashicorp.com/terraform/enterprise/v202505-1/api-docs/admin/organizations

This cURL command demonstrates how to list all organizations in a Terraform Enterprise installation. It requires an authorization token and specifies the content type as JSON API.

```shell
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  "https://tfe.example.com/api/v2/admin/organizations"

```

--------------------------------

### Change Directory to Example Repository (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/applications/confluent-provider

Navigates into the cloned example repository directory. This is where you will execute Terraform commands for this tutorial.

```shell
cd learn-terraform-confluent-provider
```

--------------------------------

### Show Policy Set API Request (HTTP)

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/api-docs/policy-sets

This example demonstrates how to make an HTTP GET request to retrieve a specific policy set by its ID. The `:id` parameter in the URL should be replaced with the actual ID of the policy set.

```http
GET /api/v2/policy-sets/:id
```

--------------------------------

### Sample Response for Stack Configuration Summaries

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/stacks

This JSON object represents a sample response when fetching stack configuration summaries. It includes data on the status of configurations, deployment groups, and pagination links for navigating through results. The 'attributes' field provides a breakdown of deployment statuses like pending, deploying, succeeded, and failed.

```json
{
  "data": [
    {
      "id": "stc-jEvHkd8DXBK594WD-summary",
      "type": "stack-configuration-summaries",
      "attributes": {
        "status": "completed",
        "sequence-number": 1,
        "stack-deployment-group-status-summary": {
          "pending": 2,
          "deploying": 0,
          "succeeded": 0,
          "failed": 0,
          "abandoned": 0
        }
      },
      "relationships": {
        "stack-configuration": {
          "data": {
            "id": "stc-jEvHkd8DXBK594WD",
            "type": "stack-configurations"
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://app.terraform.io/api/v2/stacks/st-MfwPNTsAEejHJtDw/stack-configuration-summaries?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://app.terraform.io/api/v2/stacks/st-MfwPNTsAEejHJtDw/stack-configuration-summaries?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": null,
    "last": "https://app.terraform.io/api/v2/stacks/st-MfwPNTsAEejHJtDw/stack-configuration-summaries?page%5Bnumber%5D=1&page%5Bsize%5D=20"
  },
  "meta": {
    "pagination": {
      "current-page": 1,
      "page-size": 20,
      "prev-page": null,
      "next-page": null,
      "total-pages": 1,
      "total-count": 1
    }
  }
}

```

```json
{
  "data": [
    {
      "id": "stc-jEvHkd8DXBK594WD-summary",
      "type": "stack-configuration-summaries",
      "attributes": {
        "status": "completed",
        "sequence-number": 1,
        "stack-deployment-group-status-summary": {
          "pending": 2,
          "deploying": 0,
          "succeeded": 0,
          "failed": 0,
          "abandoned": 0
        }
      },
      "relationships": {
        "stack-configuration": {
          "data": {
            "id": "stc-jEvHkd8DXBK594WD",
            "type": "stack-configurations"
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://app.terraform.io/api/v2/stacks/st-MfwPNTsAEejHJtDw/stack-configuration-summaries?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://app.terraform.io/api/v2/stacks/st-MfwPNTsAEejHJtDw/stack-configuration-summaries?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": null,
    "last": "https://app.terraform.io/api/v2/stacks/st-MfwPNTsAEejHJtDw/stack-configuration-summaries?page%5Bnumber%5D=1&page%5Bsize%5D=20"
  },
  "meta": {
    "pagination": {
      "current-page": 1,
      "page-size": 20,
      "prev-page": null,
      "next-page": null,
      "total-pages": 1,
      "total-count": 1
    }
  }
}

```

--------------------------------

### Configure Provider Installation with Filesystem Mirror and Direct Methods

Source: https://developer.hashicorp.com/terraform/cli/config/config-file

This configuration block overrides Terraform's default provider installation behavior. It specifies that providers from 'example.com' should be installed from a local filesystem mirror, while all other providers are installed directly from their origin registries. The `include` and `exclude` patterns control which providers are affected by each method.

```hcl
provider_installation {
  filesystem_mirror {
    path    = "/usr/share/terraform/providers"
    include = ["example.com/*/*"]
  }
  direct {
    exclude = ["example.com/*/*"]
  }
}
```

--------------------------------

### Clone Example Repository using Git

Source: https://developer.hashicorp.com/terraform/tutorials/use-case/vsphere-provider/vmware-environment%3Avsphere

Clones the example repository containing Terraform and Packer configurations for vSphere. This is the initial step to obtain the necessary files for the tutorial.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-vsphere

```

--------------------------------

### Example of IACT Subnet List Configuration

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

Shows how to configure the `iact_subnet_list` setting, which is a comma-separated list of CIDR masks. This enables retrieval of IACT from outside the host, specifying which subnets are permitted.

```plaintext
10.0.0.0/24,10.0.1.0/24
```

--------------------------------

### Create Terraform Configuration Directory and File

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Ahcp_variants=boundary-deploy%3Adev

These commands create a new directory for the Terraform configuration and then create the main Terraform configuration file (`main.tf`). This setup is necessary before defining the Terraform provider and resources.

```bash
$ mkdir learn-boundary-oidc && cd learn-boundary-oidc/

$ touch main.tf
```

--------------------------------

### Install Terraform on Linux using a downloaded binary

Source: https://developer.hashicorp.com/terraform/install

Provides instructions for downloading and installing Terraform binaries for Linux distributions. This method is useful when package managers are not available or preferred.

```bash
# Example for downloading and installing on Linux (specific commands depend on architecture and download URL)
# wget <TERRAFORM_BINARY_URL>
# unzip <TERRAFORM_BINARY_FILE>
# sudo mv terraform /usr/local/bin/
```

--------------------------------

### Start Boundary in Dev Mode (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Adev

This command initiates a Boundary controller in development mode, suitable for testing OIDC integrations. It outputs configuration details and logs upon successful startup. No external dependencies are required beyond the Boundary CLI.

```shell
$ boundary dev
==> Boundary server configuration:

        [Controller] AEAD Key Bytes: hdcjQ5gegRbttzQ66D5GJjcxB+xtdHzL
          [Recovery] AEAD Key Bytes: E1/gdhTuDyhsvIm+tkQR0i4m/uSRrd5A
       [Worker-Auth] AEAD Key Bytes: gwo86AYxBlbPCLsw9lsBzZ4Fd7adcydw
               [Recovery] AEAD Type: aes-gcm
                   [Root] AEAD Type: aes-gcm
    [Worker-Auth-Storage] AEAD Type: aes-gcm
            [Worker-Auth] AEAD Type: aes-gcm
                                Cgo: disabled
     Controller Public Cluster Addr: 127.0.0.1:9201
             Dev Database Container: hardcore_keller
                   Dev Database Url: postgres://postgres:password@localhost:55000/boundary?sslmode=disable
         Generated Admin Login Name: admin
           Generated Admin Password: password
          Generated Host Catalog Id: hcst_1234567890
                  Generated Host Id: hst_1234567890
              Generated Host Set Id: hsst_1234567890
      Generated Oidc Auth Method Id: amoidc_1234567890
             Generated Org Scope Id: o_1234567890
  Generated Password Auth Method Id: ampw_1234567890
         Generated Project Scope Id: p_1234567890
                Generated Target Id: ttcp_1234567890
  Generated Unprivileged Login Name: user
    Generated Unprivileged Password: password
                         Listener 1: tcp (addr: "127.0.0.1:9200", cors_allowed_headers: "[]", cors_allowed_origins: "[*", cors_enabled: "true", max_request_duration: "1m30s", purpose: "api")
                         Listener 2: tcp (addr: "127.0.0.1:9201", max_request_duration: "1m30s", purpose: "cluster")
                         Listener 3: tcp (addr: "127.0.0.1:9203", max_request_duration: "1m30s", purpose: "ops")
                         Listener 4: tcp (addr: "127.0.0.1:9202", max_request_duration: "1m30s", purpose: "proxy")
                          Log Level: info
                              Mlock: supported: false, enabled: false
                            Version: Boundary v0.10.3
                        Version Sha: d9eba38993eb70820a396894f2f1e28601d13c3d
         Worker Auth Current Key Id: folic-obliged-dude-stroller-skinless-eloquence-legible-dispense
   Worker Auth Registration Request: GzusqckarbczHoLGQ4UA25uSRm41paoR5HikgcBsCT4PMDFT7StpsFy5xjiWJwxszReKwcfGniKLcdpQto5HjhH3PqmdLU8fdT9kM7RMLiyzLKWdLqVWBhhdUiEy7Re2ConJcGWdHsGK7Th6zVQ3SXjqND3dQ3ytcVtAhdEznJQ58ib6HoMvpMTs66TS5ULCBXxpQ1u2syC6ChNPEPbaSpQd9pKWjPcPRVDjKpMzp6cjw9LZSPxBdadM81f7yS3voWoM5yMciXdUW6rqSMaP1NxRvQUAdhVQsM1ZqGLHNV
           Worker Auth Storage Path: /var/folders/8g/4dnhwwzx2d771tkklxwrd0380000gp/T/nodeenrollment1533264699
           Worker Public Proxy Addr: 127.0.0.1:9202

==> Boundary server started! Log data will stream in below:

{
  "id": "GypYTtKfJI",
  "source": "https://hashicorp.com/boundary/localmachine/controller+worker",
  "specversion": "1.0",
  "type": "system",
  "data": {
    "version": "v0.1",
    "op": "github.com/hashicorp/boundary/internal/observability/event.(*HclogLoggerAdapter).writeEvent",
    "data": {
      "@original-log-level": "none",
      "@original-log-name": "aws",
      "msg": "configuring client automatic mTLS"
    }
  },
  "datacontentype": "text/plain",
  "time": "2022-09-06T14:14:37.939433-06:00"
}
...
...
...

```

--------------------------------

### Attribute Deprecation Warning Example in Terraform

Source: https://developer.hashicorp.com/terraform/plugin/framework/v0.17.x/schemas

Shows how a deprecation message for an attribute is displayed to practitioners. This warning is raised when the attribute is used in the configuration, guiding users to alternative configurations or removal.

```terraform
Warning: Attribute Deprecated

{Configuration file/line information}

{DeprecationMessage field value}

```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/internals/lifecycle

Initializes the Terraform working directory. This command downloads the necessary provider plugins (e.g., AWS) and sets up the backend. Requires Terraform to be installed.

```bash
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Installing hashicorp/aws v3.26.0...
- Installed hashicorp/aws v3.26.0 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.


```

--------------------------------

### Add Finalize Script to Dockerfile

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This snippet demonstrates how to add a custom shell script to a Docker image that will be executed after a Terraform Enterprise run. Ensure the script is executable and located at `/usr/local/bin/finalize_custom_worker.sh`.

```dockerfile
ADD finalize_custom_worker.sh /usr/local/bin/finalize_custom_worker.sh
```

--------------------------------

### Update Docker Compose Image Configuration

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/manage/upgrade

Example of updating the `compose.yaml` file to specify the new Terraform Enterprise image tag for Docker Compose installations. This ensures the latest version is pulled during the upgrade.

```yaml
  name: terraform-enterprise
  services:
    tfe:
      image: images.releases.hashicorp.com/hashicorp/terraform-enterprise:<vYYYYMM-#>
```

--------------------------------

### List Available Airgap Versions (CLI)

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/admin/infrastructure/upgrades

Lists the available airgap package versions for Terraform Enterprise upgrade using the replicatedctl command-line tool. This helps in selecting a specific version to install.

```bash
$ replicatedctl app-release ls

```

--------------------------------

### Configure Replicated Proxy Settings

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/interactive/installer

This snippet shows how to update the proxy settings for Replicated services by editing configuration files. It involves adding HTTP_PROXY and NO_PROXY environment variables to the service options.

```bash
# Example for replicated service
REPLICATED_OPTS="-e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>"

# Example for replicated-operator service
REPLICATED_OPERATOR_OPTS="-e HTTP_PROXY=<your proxy url> -e NO_PROXY=<list of no_proxy hosts>"
```

--------------------------------

### Terraform trimprefix Function Example

Source: https://developer.hashicorp.com/terraform/language/functions/trimprefix

The trimprefix function in Terraform removes a specified prefix from the start of a string. If the string does not begin with the prefix, it remains unchanged. This function is useful for cleaning up string data.

```terraform
output "trimmed_string" {
  value = trimprefix("helloworld", "hello")
}

output "unchanged_string" {
  value = trimprefix("helloworld", "cat")
}

output "partial_trim" {
  value = trimprefix("--hello", "-")
}
```

--------------------------------

### Stop and Disable Terraform Enterprise (Docker)

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/replicated/replicated-migration

This command stops the Terraform Enterprise service and prevents it from starting automatically on boot. It is part of the rollback procedure for mounted disk installations.

```bash
systemctl disable --now terraform-enterprise
```

--------------------------------

### Go Cloud Backend Configuration for CDKTF

Source: https://developer.hashicorp.com/terraform/cdktf/v0.15.x/concepts/remote-backends

Illustrates how to set up a CDKTF stack in Go, configuring a remote cloud backend with hostname, organization, and workspace details. This snippet utilizes the HashiCorp CDKTF Go bindings.

```go
import (
    "github.com/aws/constructs-go/constructs/v10"
    "github.com/aws/jsii-runtime-go"
    "github.com/hashicorp/terraform-cdk-go/cdktf"
)

func NewCloudBackendStack(scope constructs.Construct, name string) cdktf.TerraformStack {
    stack := cdktf.NewTerraformStack(scope, &name)

    cdktf.NewCloudBackend(stack, &cdktf.CloudBackendConfig{
        Hostname:     jsii.String("app.terraform.io"),
        Organization: jsii.String("company"),
        Workspaces:   cdktf.NewNamedCloudWorkspace(jsii.String("my-app-prod")),
    })

    cdktf.NewTerraformOutput(stack, jsii.String("dns-server"), &cdktf.TerraformOutputConfig{
        Value: "hello-world",
    })

    return stack
}
```

--------------------------------

### Test Mux Server Setup with Protocol Version 6 in Go

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/mux

This Go code snippet demonstrates how to set up and test a Mux server for Protocol Version 6. It utilizes the terraform-plugin-go and terraform-plugin-mux libraries to upgrade an SDK provider and combine it with a framework provider. The test verifies the provider factory setup and includes a placeholder for resource configuration.

```go
import (
    "context"
    "testing"

    "github.com/hashicorp/terraform-plugin-go/tfprotov6"
    "github.com/hashicorp/terraform-plugin-mux/tf5to6server"
    "github.com/hashicorp/terraform-plugin-mux/tf6muxserver"
    "github.com/hashicorp/terraform-plugin-testing/helper/resource"
)

func TestMuxServer(t *testing.T) {
    resource.Test(t, resource.TestCase{
        ProtoV6ProviderFactories: map[string]func() (tfprotov6.ProviderServer, error) {
            "examplecloud": func() (tfprotov6.ProviderServer, error) {
                ctx := context.Background()

                upgradedSdkServer, err := tf5to6server.UpgradeServer(
                    ctx,
                    Provider().GRPCProvider, // Example terraform-plugin-sdk provider
                )

                if err != nil {
                    return nil, err
                }

                providers := []func() tfprotov6.ProviderServer{
                    providerserver.NewProtocol6(New()), // Example terraform-plugin-framework provider
                    func() tfprotov6.ProviderServer {
                        return upgradedSdkServer
                    },
                }

                muxServer, err := tf6muxserver.NewMuxServer(ctx, providers...)

                if err != nil {
                    return nil, err
                }

                return muxServer.ProviderServer(), nil
            },
        },
        Steps: []resource.TestStep{
            {
                Config: "... configuration including simplest data source or managed resource",
            },
        },
    })
}

```

--------------------------------

### Basic Acceptance Test for Example Widget in Go

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/testing

This Go function `TestAccExampleWidget_basic` defines a basic acceptance test for the `example_widget` resource. It generates a random name, configures the resource, and asserts that the resource exists with the correct attributes after creation and that it is destroyed properly. It relies on helper functions like `acctest.RandStringFromCharSet` and `resource.Test` from the Terraform plugin SDK.

```go
func TestAccExampleWidget_basic(t *testing.T) {
    var widget example.Widget

    rName := acctest.RandStringFromCharSet(10, acctest.CharSetAlphaNum)

    resource.Test(t, resource.TestCase{
        PreCheck:     func() { testAccPreCheck(t) },
        Providers:    testAccProviders,
        CheckDestroy: testAccCheckExampleResourceDestroy,
        Steps: []resource.TestStep{
            {
                Config: testAccExampleResource(rName),
                Check: resource.ComposeTestCheckFunc(
                    testAccCheckExampleResourceExists("example_widget.foo", &widget),
                    testAccCheckExampleWidgetValues(widget, rName),
                    resource.TestCheckResourceAttr("example_widget.foo", "active", "true"),
                    resource.TestCheckResourceAttr("example_widget.foo", "name", rName),
                ),
            },
        },
    })
}
```

--------------------------------

### Retrieve Minio Instance Information

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/requirements/data-storage/minio-setup-guide

Uses Docker and jq to retrieve the IP address of the Minio container and its access/secret keys from the configuration file. These details are necessary for configuring Terraform Enterprise.

```bash
# IP address of the running container:
docker inspect minio | jq -r .[0].NetworkSettings.IPAddress

# Access key:
jq -r .credential.accessKey /var/run/minio/config/config.json

# Secret key:
jq -r .credential.secretKey /var/run/minio/config/config.json
```

--------------------------------

### Apply Start Message

Source: https://developer.hashicorp.com/terraform/internals/v1.9.x/machine-readable-ui

Indicates the start of an apply operation for a specific resource.

```APIDOC
## Apply Start Message

### Description
The `apply_start` message indicates that Terraform is beginning to apply changes to a specific resource. The `hook` object contains details about the resource and the action to be taken.

### Method
N/A (This is a message type, not an API endpoint)

### Endpoint
N/A

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```json
{
  "@level": "info",
  "@message": "random_pet.animal: Creating...",
  "@module": "terraform.ui",
  "@timestamp": "2021-05-25T13:32:41.825308-04:00",
  "hook": {
    "resource": {
      "addr": "random_pet.animal",
      "module": "",
      "resource": "random_pet.animal",
      "implied_provider": "random",
      "resource_type": "random_pet",
      "resource_name": "animal",
      "resource_key": null
    },
    "action": "create"
  },
  "type": "apply_start"
}
```

### Response
#### Success Response (200)
N/A

#### Response Example
```json
{
  "@level": "info",
  "@message": "random_pet.animal: Creating...",
  "@module": "terraform.ui",
  "@timestamp": "2021-05-25T13:32:41.825308-04:00",
  "hook": {
    "resource": {
      "addr": "random_pet.animal",
      "module": "",
      "resource": "random_pet.animal",
      "implied_provider": "random",
      "resource_type": "random_pet",
      "resource_name": "animal",
      "resource_key": null
    },
    "action": "create"
  },
  "type": "apply_start"
}
```
```

--------------------------------

### Example Sidekiq Component Log (JSON)

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/admin/infrastructure/consolidated-services

This snippet shows an example of a log entry from the 'sidekiq' component. The log is in standard JSON format and includes a 'component' attribute.

```json
{"component":"sidekiq","log":"2023-09-14 19:04:19 [INFO] msg=Worker finish worker=AgentStatusWorker"}
```

--------------------------------

### CDKTF TypeScript Application Code (main.ts)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.12.x/create-and-deploy/project-setup

The main TypeScript file for a CDKTF application, demonstrating how to import and use the 'random' provider and its resources. Provider bindings are generated by running `cdktf get`.

```typescript
// File: /tmp/cdktf-demo/main.ts

/*Provider bindings are generated by running cdktf get.
See https://github.com/hashicorp/terraform-cdk/blob/main/docs/working-with-cdk-for-terraform/using-providers.md#importing-providers-and-modules for more details.*/
import * as random from "./.gen/providers/random";

import { Construct } from "constructs";
import { App, TerraformStack } from "cdktf";

class MyStack extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);

    new random.RandomProvider(this, "random", {});
    new random.Pet(this, "server", {});
  }
}

const app = new App();
new MyStack(app, "cdktf-demo");
app.synth();

```

--------------------------------

### Implement Terraform Resource Create Method in Go

Source: https://developer.hashicorp.com/terraform/plugin/framework/resources/create

This Go code snippet demonstrates the implementation of the `Create` method for a Terraform resource. It includes reading data from the Terraform plan, converting it to an API model, making an HTTP POST request to create the resource, handling HTTP responses and JSON decoding, and finally updating the Terraform state. Dependencies include the Terraform SDK (`github.com/hashicorp/terraform-plugin-sdk/v2`), `net/http`, `encoding/json`, and `bytes`.

```go
// ThingResource defines the resource implementation.
// Some resource.Resource interface methods are omitted for brevity.
type ThingResource struct {
    // client is configured via a Configure method, which is not shown in this
    // example for brevity. Refer to the Configure Resources documentation for
    // additional details for setting up resources with external clients.
    client *http.Client
}

// ThingResourceModel describes the Terraform resource data model to match the
// resource schema.
type ThingResourceModel struct {
    Name types.String `tfsdk:"name"`
    Id   types.String `tfsdk:"id"`
}

// ThingResourceAPIModel describes the API data model.
type ThingResourceAPIModel struct {
    Name string `json:"name"`
    Id   string `json:"id"`
}

func (r ThingResource) Schema(ctx context.Context, req resource.SchemaRequest, resp *resource.SchemaResponse) {
    resp.Schema = schema.Schema{
        Attributes: map[string]schema.Attribute{
            "name": schema.StringAttribute{
                MarkdownDescription: "Name of the thing to be saved in the service.",
                Required:            true,
            },
            "id": schema.StringAttribute{
                Computed:            true,
                MarkdownDescription: "Service generated identifier for the thing.",
                PlanModifiers: []planmodifier.String{
                    stringplanmodifier.UseStateForUnknown(),
                },
            },
        },
        MarkdownDescription: "Manages a thing.",
    }
}

func (r ThingResource) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
    var data ThingResourceModel

    // Read Terraform plan data into the model
    resp.Diagnostics.Append(req.Plan.Get(ctx, &data)...)

    if resp.Diagnostics.HasError() {
        return
    }

    // Convert from Terraform data model into API data model
    createReq := ThingResourceAPIModel{
        Name: data.Name.ValueString(),
    }

    httpReqBody, err := json.Marshal(createReq)

    if err != nil {
        resp.Diagnostics.AddError(
            "Unable to Create Resource",
            "An unexpected error occurred while creating the resource create request. " +
                "Please report this issue to the provider developers.\n\n" +
                "JSON Error: "+err.Error(),
        )

        return
    }

    // Create HTTP request
    httpReq := http.NewRequestWithContext(
        ctx,
        http.MethodPost,
        "http://example.com/things",
        bytes.NewBuffer(httpReqBody),
    )

    // Send HTTP request
    httpResp, err := d.client.Do(httpReq)
    defer httpResp.Body.Close()

    if err != nil {
        resp.Diagnostics.AddError(
            "Unable to Create Resource",
            "An unexpected error occurred while attempting to create the resource. " +
                "Please retry the operation or report this issue to the provider developers.\n\n" +
                "HTTP Error: "+err.Error(),
        )

        return
    }

    // Return error if the HTTP status code is not 200 OK
    if httpResp.StatusCode != http.StatusOK {
        resp.Diagnostics.AddError(
            "Unable to Create Resource",
            "An unexpected error occurred while attempting to create the resource. " +
                "Please retry the operation or report this issue to the provider developers.\n\n" +
                "HTTP Status: "+httpResp.Status,
        )

        return
    }

    var createResp ThingResourceAPIModel

    err = json.NewDecoder(httpResp.Body).Decode(&createResp)

    if err != nil {
        resp.Diagnostics.AddError(
            "Unable to Create Resource",
            "An unexpected error occurred while parsing the resource creation response. " +
                "Please report this issue to the provider developers.\n\n" +
                "JSON Error: "+err.Error(),
        )

        return
    }

    // Convert from the API data model to the Terraform data model
    // and set any unknown attribute values.
    data.Id = types.StringValue(createResp.Id)

    // Save data into Terraform state
    resp.Diagnostics.Append(resp.State.Set(ctx, &data)...)
}

```

--------------------------------

### Get Ingress Resource Details

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/flexible-deployments/install/kubernetes/install

Retrieves information about Kubernetes ingress resources, specifically looking for the Terraform Enterprise ingress. This command helps in identifying the hostname and IP address configured for external access.

```bash
$ kubectl get ingress
NAME                   CLASS   HOSTS        ADDRESS         PORTS     AGE
terraform-enterprise   nginx   <hostname>    <ip>           80, 443   60s
```

--------------------------------

### Get Attribute Path in List Item (Terraform Schema)

Source: https://developer.hashicorp.com/terraform/plugin/framework/handling-data/paths

Demonstrates how to access an attribute within a specific list item using `AtName()`. This example retrieves the path for 'block_string_attribute' in the first item of 'root_list_block'.

```go
path.Root("root_list_block").AtListIndex(0).AtName("block_string_attribute")

```

--------------------------------

### Apply Start Message

Source: https://developer.hashicorp.com/terraform/internals/v1.4.x/machine-readable-ui

The `apply_start` message indicates the beginning of an apply operation for a resource. The `hook` object includes the resource details, the action being taken (e.g., `create`, `update`, `delete`), and optionally an identifier for the resource instance.

```APIDOC
## Apply Start

The `apply_start` message `hook` object has the following keys:
  * `resource`: a `resource` object identifying the resource
  * `action`: the action to be taken for the resource. Values: `noop`, `create`, `read`, `update`, `replace`, `delete`
  * `id_key` and `id_value`: a key/value pair used to identify this instance of the resource, omitted when unknown

### Example
```json
{
  "@level": "info",
  "@message": "random_pet.animal: Creating...",
  "@module": "terraform.ui",
  "@timestamp": "2021-05-25T13:32:41.825308-04:00",
  "hook": {
    "resource": {
      "addr": "random_pet.animal",
      "module": "",
      "resource": "random_pet.animal",
      "implied_provider": "random",
      "resource_type": "random_pet",
      "resource_name": "animal",
      "resource_key": null
    },
    "action": "create"
  },
  "type": "apply_start"
}
```
```

--------------------------------

### API Pagination Example

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/admin

Demonstrates how to use `page[number]` and `page[size]` query parameters to paginate through API responses that return lists of objects. The response includes `links` and `meta` attributes for navigation and pagination details.

```json
{
  "data": [...],
  "links": {
    "self": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=2&page%5Bsize%5D=20",
    "last": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=2&page%5Bsize%5D=20"
  },
  "meta": {
    "pagination": {
      "current-page": 1,
      "prev-page": null,
      "next-page": 2,
      "total-pages": 2,
      "total-count": 21
    }
  }
}
```

```json
{
  "data": [...],
  "links": {
    "self": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=2&page%5Bsize%5D=20",
    "last": "https://app.terraform.io/api/v2/organizations/hashicorp/workspaces?page%5Bnumber%5D=2&page%5Bsize%5D=20"
  },
  "meta": {
    "pagination": {
      "current-page": 1,
      "prev-page": null,
      "next-page": 2,
      "total-pages": 2,
      "total-count": 21
    }
  }
}
```

--------------------------------

### Get Ingress Controller Address

Source: https://developer.hashicorp.com/terraform/enterprise/v202407-1/flexible-deployments/install/kubernetes/install

Retrieves information about ingress resources, specifically looking for the address (external IP) assigned to the Terraform Enterprise ingress. This is used when configuring custom ingress controllers like Nginx.

```bash
NAME                   CLASS   HOSTS        ADDRESS         PORTS     AGE
terraform-enterprise   nginx   <hostname>    <ip>           80, 443   60s
```

--------------------------------

### Remove Example Data Sources and Resources (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This shell command removes example directories for data sources and resources. This is typically done to clean up the project before adding custom examples or generating documentation.

```shell
$ rm -r examples/data-sources/scaffolding_example && rm -r examples/resources/scaffolding_example

```

--------------------------------

### Provision Start Event

Source: https://developer.hashicorp.com/terraform/internals/v1.11.x/machine-readable-ui

This event is triggered when a resource begins provisioning.

```APIDOC
## Provision Start Event

### Description
This event is triggered when a resource begins provisioning.

### Method
N/A (Event-driven)

### Endpoint
N/A (Event-driven)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
- **@level** (string) - The logging level of the message.
- **@message** (string) - The main log message.
- **@module** (string) - The module generating the log.
- **@timestamp** (string) - The timestamp of the event.
- **hook** (object) - An object containing details about the provisioning hook.
  - **resource** (object) - An object identifying the resource being provisioned.
    - **addr** (string) - The address of the resource.
    - **module** (string) - The module the resource belongs to.
    - **resource** (string) - The full resource identifier.
    - **implied_provider** (string) - The implied provider for the resource.
    - **resource_type** (string) - The type of the resource.
    - **resource_name** (string) - The name of the resource.
    - **resource_key** (integer) - The key of the resource if it's part of a list or map.
  - **provisioner** (string) - The type of provisioner being used.
- **type** (string) - The type of the event, which is 'provision_start'.
```

--------------------------------

### Example of Extra No Proxy Configuration

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

Illustrates the format for the `extra_no_proxy` setting, which specifies a comma-separated list of hosts to exclude from proxying. This setting is useful for ensuring direct connections to specific internal or trusted external services.

```plaintext
127.0.0.1,tfe.myapp.com,myco.github.com
```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/modules/module-use/terraform-workflow%3Ahcp

The `terraform init` command initializes the working directory, downloading provider plugins and setting up HCP Terraform integration. It prepares the environment for subsequent Terraform commands like `plan` and `apply`.

```bash
$ terraform init
Initializing HCP Terraform...
Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Installing hashicorp/aws v4.49.0...
- Installed hashicorp/aws v4.49.0 (signed by HashiCorp)
HCP Terraform has been successfully initialized!
You may now begin working with HCP Terraform. Try running "terraform plan" to
see any changes that are required for your infrastructure.
If you ever set or change modules or Terraform Settings, run "terraform init"
again to reinitialize your working directory.
```

--------------------------------

### Terraform Enterprise Application Settings JSON Example

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

This JSON file defines the application settings for Terraform Enterprise, such as hostname, disk path, and encrypted password. It must be valid JSON and is referenced in the Replicated configuration.

```json
{
  "hostname": {
    "value": "terraform.example.com"
  },
  "disk_path": {
    "value": "/opt/terraform-enterprise"
  },
  "enc_password": {
    "value": "CHANGEME"
  }
}
```

--------------------------------

### Terraform Enterprise Docker Compose Environment Variables

Source: https://developer.hashicorp.com/terraform/enterprise/v202404-1/flexible-deployments/install/docker/install

Defines environment variables for Terraform Enterprise within a Docker Compose file. These include settings for Redis TLS and authentication, and Vault cluster address.

```yaml
      TFE_REDIS_USE_TLS: "<To use tls? e.g. false>"
      TFE_REDIS_USE_AUTH: "<To use customized credential to authenticate? e.g. false>"

      # Vault cluster settings.
      # If you are using the default internal vault, this should be the private routable IP address of the node itself.
      TFE_VAULT_CLUSTER_ADDRESS: "https://<private_ip_of_the_node>:8201"
```

--------------------------------

### Initialize Terraform Configuration with Providers and Modules

Source: https://developer.hashicorp.com/terraform/tutorials/cli/plan_utm_offer=ARTICLE_PAGE

This command initializes a Terraform configuration, downloading and installing the necessary provider plugins (AWS and random) and modules referenced in the configuration. It shows the process of reusing existing provider versions from a lock file and installing new ones if required. Successful initialization prepares the working directory for subsequent Terraform commands like 'plan' or 'apply'.

```bash
$ terraform init
Initializing the backend...
Initializing modules...
- ec2-instance in modules/aws-ec2-instance
Downloading registry.terraform.io/joatmon08/hello/random 6.0.0 for hello...
- hello in .terraform/modules/hello
Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/aws v6.2.0...
- Installed hashicorp/aws v6.2.0 (signed by HashiCorp)
- Installing hashicorp/random v3.5.1...
- Installed hashicorp/random v3.5.1 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Initialize Terraform with Google Provider

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-migrate

This command initializes a Terraform working directory, downloading the Google provider and its dependencies, and creating a lock file for reproducible builds. It's crucial to re-run after module or setting changes.

```bash
$ terraform init
Initializing HCP Terraform...
Initializing modules...
- terraform_module in terraform_modules
Initializing provider plugins...
- Finding hashicorp/google versions matching "~> 6.50.0"...
- Finding hashicorp/tls versions matching "~> 4.1.0"...
- Finding hashicorp/random versions matching "~> 3.7.2"...
- Installing hashicorp/google v6.50.0...
- Installed hashicorp/google v6.50.0 (signed by HashiCorp)
- Installing hashicorp/tls v4.1.0...
- Installed hashicorp/tls v4.1.0 (signed by HashiCorp)
- Installing hashicorp/random v3.7.2...
- Installed hashicorp/random v3.7.2 (signed by HashiCorp)
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.
HCP Terraform has been successfully initialized!

You may now begin working with HCP Terraform. Try running "terraform plan" to
see any changes that are required for your infrastructure.
```

--------------------------------

### Get Root List Block Path (Terraform Schema)

Source: https://developer.hashicorp.com/terraform/plugin/framework/handling-data/paths

Shows how to obtain the root path for a list nested block named 'root_list_block' using `path.Root()`. This is the starting point for navigating within the block structure.

```go
path.Root("root_list_block")

```

--------------------------------

### Stop and Disable Terraform Enterprise (Docker) for Rollback

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated-migration

This command stops the Docker Compose-based Terraform Enterprise service and disables it from starting on boot. This is the first step in rolling back to a Replicated installation.

```bash
$ systemctl disable --now terraform-enterprise

```

--------------------------------

### Terraform Initialization and Import Process

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/resources

Logs detailing Terraform's initialization process, including backend and provider setup, and the preparation and refresh stages for importing an AWS S3 bucket.

```text
ts-import-with-configuration  Initializing the backend...
ts-import-with-configuration  Initializing provider plugins...
                              - Reusing previous version of hashicorp/aws from the dependency lock file
ts-import-with-configuration  - Using previously-installed hashicorp/aws v5.18.1

                              Terraform has been successfully initialized!
ts-import-with-configuration
                              You may now begin working with Terraform. Try running "terraform plan" to see
                              any changes that are required for your infrastructure. All Terraform commands
                              should now work.

                              If you ever set or change modules or backend configuration for Terraform,
                              rerun this command to reinitialize your working directory. If you forget, other
                              commands will detect it and remind you to do so if necessary.
ts-import-with-configuration  aws_s3_bucket.bucket: Preparing import... [id=best-bucket-in-the-world]
ts-import-with-configuration  aws_s3_bucket.bucket: Refreshing state... [id=best-bucket-in-the-world]
ts-import-with-configuration  Terraform will perform the following actions:
ts-import-with-configuration    # aws_s3_bucket.bucket will be imported
                                # (config will be generated)
                                  resource "aws_s3_bucket" "bucket" {
                                      arn                         = "arn:aws:s3:::best-bucket-in-the-world"
                                      bucket                      = "best-bucket-in-the-world"

```

--------------------------------

### Terraform Configuration Keys Example

Source: https://developer.hashicorp.com/terraform/enterprise/v202507-1/admin/application/automated-license-utilization-reporting

This snippet demonstrates the structure of configuration keys within a Terraform Enterprise/Cloud setup. It includes keys for VCS providers, environment reporting, and various resource counts.

```hcl
{
    "gcp_provider_present": {
        "key": "gcp_provider_present",
        "value": 0,
        "mode": "write"
    },
    "github_vcs_present": {
        "key": "github_vcs_present",
        "value": 0,
        "mode": "write"
    },
    "gitlab_vcs_present": {
        "key": "gitlab_vcs_present",
        "value": 0,
        "mode": "write"
    },
    "installation_reporting_environment_type": {
        "key": "installation_reporting_environment_type",
        "value": 0,
        "mode": "write"
    },
    "operational_mode": {
        "key": "operational_mode",
        "value": 0,
        "mode": "write"
    },
    "org_admin_count": {
        "key": "org_admin_count",
        "value": 1,
        "mode": "write"
    },
    "org_count": {
        "key": "org_count",
        "value": 1,
        "mode": "write"
    },
    "private_modules_count": {
        "key": "private_modules_count",
        "value": 0,
        "mode": "write"
    },
    "product_usage_reporting_opt_in": {
        "key": "product_usage_reporting_opt_in",
        "value": 1,
        "mode": "write"
    },
    "project_count": {
        "key": "project_count",
        "value": 1,
        "mode": "write"
    },
    "run_concurrency": {
        "key": "run_concurrency",
        "value": 0,
        "mode": "write"
    },
    "run_tasks_count": {
        "key": "run_tasks_count",
        "value": 0,
        "mode": "write"
    },
    "run_tasks_used_last_90_days": {
        "key": "run_tasks_used_last_90_days",
        "value": 0,
        "mode": "write"
    },
    "run_triggers_used_last_90_days": {
        "key": "run_triggers_used_last_90_days",
        "value": 0,
        "mode": "write"
    },
    "sentinel_used_last_90_days": {
        "key": "sentinel_used_last_90_days",
        "value": 0,
        "mode": "write"
    },
    "servicenow_catalog_billable_rum_count": {
        "key": "servicenow_catalog_billable_rum_count",
        "value": 0,
        "mode": "write"
    },
    "servicenow_catalog_run_count": {
        "key": "servicenow_catalog_run_count",
        "value": 0,
        "mode": "write"
    },
    "servicenow_catalog_workspace_count": {
        "key": "servicenow_catalog_workspace_count",
        "value": 0,
        "mode": "write"
    },
    "teams_count": {
        "key": "teams_count",
        "value": 1,
        "mode": "write"
    },
    "user_count": {
        "key": "user_count",
        "value": 1,
        "mode": "write"
    },
    "using_admin_api": {
        "key": "using_admin_api",
        "value": 0,
        "mode": "write"
    },
    "using_iam_auth_s3": {
        "key": "using_iam_auth_s3",
        "value": 0,
        "mode": "write"
    },
    "varsets_count": {
        "key": "varsets_count",
        "value": 0,
        "mode": "write"
    }
}
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/azure/azure-virtual-machine-scale-sets

Clones the example Terraform repository for managing Azure Virtual Machine Scale Sets. This repository contains the necessary configuration files for the tutorial.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-azure-scale-sets

```

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-azure-scale-sets

```

--------------------------------

### Terraform API Resource Inclusion Example

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/admin/terraform-versions

Shows how to request related resources using the 'include' query parameter in a GET request to the Terraform API. The response includes an 'included' section containing details of the requested related resources, such as users associated with a team.

```shell
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/teams/team-n8UQ6wfhyym25sMe?include=users

```

--------------------------------

### tf-migrate Configuration Example

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/migrate/tf-migrate/reference/configuration

Example tf-migrate configuration file demonstrating how to set skip directories, define projects with their respective directories, and configure workspaces with environment variables and Terraform variable files.

```hcl
skip-dir = ["example/skip/dir1", "example/skip/dir2"]

projects = [
    {
        dir = "example/project1"
        workspaces = [
            {
                name = "staging"
                env-vars = {
                    "TF_VAR_region": "us-east-2"
                }
                terraform-vars = ["staging.tfvars"]
            },
            {
                name = "dev"
                terraform-vars = ["dev.tfvars"]
            }
        ]
    }
]

```

--------------------------------

### CDKTF Stack Dependency Example in Go

Source: https://developer.hashicorp.com/terraform/cdktf/v0.19.x/concepts/stacks

This Go program defines source and dependency stacks using CDKTF. It demonstrates creating instances, managing dependencies, and exposing merged resources via `TerraformLocal`. The `main` function orchestrates the creation of these stacks.

```go
import (
    "github.com/aws/constructs-go/constructs/v10"
    "github.com/aws/jsii-runtime-go"
    "github.com/hashicorp/terraform-cdk-go/cdktf"
    "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/aws/instance"
    aws "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/aws/provider"
)

type SourceStack struct {
    Instance instance.Instance
}

func NewSourceStack(scope constructs.Construct, name string) SourceStack {
    stack := cdktf.NewTerraformStack(scope, &name)

    aws.NewAwsProvider(stack, jsii.String("aws"), &aws.AwsProviderConfig{
        Region: jsii.String("us-east-1"),
    })

    instance := instance.NewInstance(stack, jsii.String("Hello"), &instance.InstanceConfig{
        Ami:          jsii.String("ami-abcde123"),
        InstanceType: jsii.String("t2.micro"),
    })

    return SourceStack{
        Instance: instance,
    }
}

type DependencyStack struct {
    AllResources *[]*string
}

func NewDependencyStack(scope constructs.Construct, name string, dependencies []*SourceStack) DependencyStack {
    stack := cdktf.NewTerraformStack(scope, &name)

    ids := make([]*string, 0)
    for _, dep := range dependencies {
        ids = append(ids, dep.Instance.Id())
    }

    allResources := cdktf.NewTerraformLocal(stack, jsii.String("merged_items"), ids)

    return DependencyStack{
        AllResources: allResources.AsList(),
    }
}

func NewNestedDependencyStack(scope constructs.Construct, name string, allResources []*string) cdktf.TerraformStack {
    stack := cdktf.NewTerraformStack(scope, &name)

    cdktf.NewTerraformOutput(stack, jsii.String("all_resources"), &cdktf.TerraformOutputConfig{
        Value: allResources,
    })

    return stack
}

func main() {
    app := cdktf.NewApp(nil)

    stackA := NewSourceStack(app, "stack-a")
    stackB := NewSourceStack(app, "stack-b")

    stackC := NewDependencyStack(app, "stack-c", []*SourceStack{&stackA, &stackB})

    NewNestedDependencyStack(app, "stack-d", *stackC.AllResources)

    app.Synth()
}

```

```go
import (
    "github.com/aws/constructs-go/constructs/v10"
    "github.com/aws/jsii-runtime-go"
    "github.com/hashicorp/terraform-cdk-go/cdktf"
    "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/aws/instance"
    aws "github.com/hashicorp/terraform-cdk/examples/go/documentation/generated/hashicorp/aws/provider"
)

type SourceStack struct {
    Instance instance.Instance
}

func NewSourceStack(scope constructs.Construct, name string) SourceStack {
    stack := cdktf.NewTerraformStack(scope, &name)

    aws.NewAwsProvider(stack, jsii.String("aws"), &aws.AwsProviderConfig{
        Region: jsii.String("us-east-1"),
    })

    instance := instance.NewInstance(stack, jsii.String("Hello"), &instance.InstanceConfig{
        Ami:          jsii.String("ami-abcde123"),
        InstanceType: jsii.String("t2.micro"),
    })

    return SourceStack{
        Instance: instance,
    }
}

type DependencyStack struct {
    AllResources *[]*string
}


```

--------------------------------

### Terraform Enterprise Docker Compose Container Settings

Source: https://developer.hashicorp.com/terraform/enterprise/v202404-1/flexible-deployments/install/docker/install

Configures container settings for Terraform Enterprise in Docker Compose, including capabilities, read-only status, temporary file systems, port mappings, and volume mounts.

```yaml
    cap_add:
      - IPC_LOCK
    read_only: true
    tmpfs:
      - /tmp:mode=01777
      - /run
      - /var/log/terraform-enterprise
    ports:
      - "80:80"
      - "443:443"
      - "8201:8201"
    volumes:
      - type: bind
        source: /var/run/docker.sock
        target: /run/docker.sock
      - type: bind
        source: ./certs
        target: /etc/ssl/private/terraform-enterprise
      - type: volume
        source: terraform-enterprise-cache
        target: /var/cache/tfe-task-worker/terraform
```

--------------------------------

### Glob Pattern Examples for Run Triggering

Source: https://developer.hashicorp.com/terraform/enterprise/v202505-1/workspaces/settings/vcs

Examples demonstrating the use of glob patterns for specifying file paths that should trigger automatic runs in Terraform. These patterns support wildcards for flexible matching.

```text
  "/**/*"         # Matches every file in every directory
  "/module/**/*"    # Matches all files in any directory below the `module` directory
  "/**/networking/*" # Matches every file that is inside any `networking` directory
  "/**/networking/**/*" # Matches every file that has `networking` directory on its path
  "/**/*.tf"       # Matches every file in any directory that has the `.tf` extension
  "/submodule/*.???" # Matches every file inside `submodule` directory which has three characters long extension.
```

--------------------------------

### Example: Inspecting Licensing Service Logs

Source: https://developer.hashicorp.com/terraform/enterprise/v202311-1/flexible-deployments/troubleshooting

Demonstrates how to inspect the logs for the `tfe:licensing` service. The output shows both informational messages and a specific error related to database connection failures, highlighting a common issue with the 'terraform-enterprise' role not existing.

```bash
$ cat /var/log/terraform-enterprise/licensing.log
{"@level":"info","@message":"initializing database","@module":"tfe-licensing","@timestamp":"2023-05-10T20:46:26.379084Z"}
{"@level":"error","@message":"error opening database connection","@module":"tfe-licensing","@timestamp":"2023-05-10T20:46:26.399064Z","error":"failed to connect to `host=/var/run/postgresql user=terraform-enterprise database=`: server error (FATAL: role \"terraform-enterprise\" does not exist (SQLSTATE 28000))"}

```

--------------------------------

### Create Terraform Configuration File

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Adev

This command creates an empty file named 'main.tf' in the current directory. This file will contain the Terraform configuration for setting up the Boundary provider and resources.

```bash
$ touch main.tf
```

--------------------------------

### Disable SAML SSO in Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-2/saml/troubleshooting

To disable SAML SSO, navigate to the SAML administration page in Terraform Enterprise and uncheck the 'Enable SAML Single Sign-On' option. This is a prerequisite for troubleshooting and ensuring a clean setup.

```text
https://<TFE HOSTNAME>/app/admin/saml
```

--------------------------------

### Get Ingress Address with Kubectl

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/kubernetes

This command retrieves the ingress resource details, showing the name, class, hosts, IP address, and ports. This is useful for verifying the ingress setup and obtaining the address for accessing Terraform Enterprise.

```bash
$ kubectl get ingress
NAME                   CLASS   HOSTS        ADDRESS         PORTS     AGE
terraform-enterprise   nginx   <hostname>    <ip>           80, 443   60s

```

--------------------------------

### Implement Simplified Update Function (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/deprecations

Handles updating the 'example_widget' resource with the simplified schema. It retrieves the 'new_attribute' and applies the update to the provider API. The function then calls the read function to update the resource's state.

```go
func resourceExampleWidgetUpdate(d *schema.ResourceData, meta interface{}) error {
    // ... other logic ...

    newAttribute := d.Get("new_attribute").(string)
    // add attribute to provider update API call

    // ... other logic ...
    return resourceExampleWidgetRead(d, meta)
}
```

--------------------------------

### Clone Terraform Expressions Repository

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/expressions

Clone the example repository containing Terraform configurations for AWS network components, EC2 instances, and load balancers. This repository will be modified using Terraform expressions throughout the tutorial. Ensure you have Git installed.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-expressions
```

--------------------------------

### Navigate to Configuration Directory

Source: https://developer.hashicorp.com/terraform/tutorials/cli/cloud-migrate

Changes the current working directory to the cloned example configuration directory. This step is necessary to execute Terraform commands within the project context. No specific inputs or outputs are generated, but it prepares the environment for subsequent commands.

```bash
$ cd learn-state-migration

```

--------------------------------

### Example CA Certificate Formatting for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/v202304-1/install/automated/automating-the-installer

Demonstrates how to format custom certificate authority (CA) bundles for Terraform Enterprise. Newline characters within the certificate data must be replaced with '\n' for proper JSON parsing.

```plaintext
---\nX509 CERT ---\naabbccddeeff\n---\nX509 CERT ---\n
```

--------------------------------

### Retrieve Minio Instance Information

Source: https://developer.hashicorp.com/terraform/enterprise/v202212-2/requirements/data-storage/minio-setup-guide

Commands to retrieve the IP address, access key, and secret key of the running Minio Docker container. These details are necessary for configuring Terraform Enterprise to use Minio for object storage.

```bash
# IP address of the running container: 
docker inspect minio | jq -r .[0].NetworkSettings.IPAddress
# Access key: 
jq -r .credential.accessKey /var/run/minio/config/config.json
# Secret key: 
jq -r .credential.secretKey /var/run/minio/config/config.json
```

--------------------------------

### Terraform formatlist Function Examples

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/functions/formatlist

These examples demonstrate the usage of the `formatlist` function in Terraform. They show how to format a list of names with a static prefix and how to format a list of names with a dynamic prefix.

```terraform
> formatlist("Hello, %s!", ["Valentina", "Ander", "Olivia", "Sam"])
[
  "Hello, Valentina!",
  "Hello, Ander!",
  "Hello, Olivia!",
  "Hello, Sam!",
]
> formatlist("%s, %s!", "Salutations", ["Valentina", "Ander", "Olivia", "Sam"])
[
  "Salutations, Valentina!",
  "Salutations, Ander!",
  "Salutations, Olivia!",
  "Salutations, Sam!",
]
```

--------------------------------

### Retrieve Node IDs (cURL)

Source: https://developer.hashicorp.com/terraform/enterprise/api-docs/nodes

This cURL command demonstrates how to make a GET request to the /api/v1/nodes endpoint to retrieve a list of all node IDs in a Terraform Enterprise installation. It requires an Authorization header with a bearer token.

```curl
curl \
  --header "Authorization: Bearer $TOKEN" \
  --request GET \
  https://tfe.example.com:8443/api/v1/nodes
```

--------------------------------

### Implement Simplified Read Function (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/deprecations

Handles reading the state of the 'example_widget' resource with the simplified schema. It sets the 'new_attribute' in the state. This function is part of the resource's lifecycle management.

```go
func resourceExampleWidgetRead(d *schema.ResourceData, meta interface{}) error {
    // ... other logic ...

    d.Set("new_attribute", /* ... */)

    // ... other logic ...
    return nil
}
```

--------------------------------

### Get Nested Attribute Path in Nested List (Terraform Schema)

Source: https://developer.hashicorp.com/terraform/plugin/framework/handling-data/paths

Illustrates how to construct a path to an attribute within a nested list block. This example navigates to 'nested_block_string_attribute' within the first item of 'nested_list_block', which is itself within the first item of 'root_list_block'.

```go
path.Root("root_list_block").AtListIndex(0).AtName("nested_list_block").AtListIndex(0).AtName("nested_block_string_attribute")

```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/azure/entra-id

Initializes the Terraform configuration directory. This command downloads and installs the necessary providers, such as the `azuread` provider, and prepares the working directory for use. It's a prerequisite before running other Terraform commands like `plan` or `apply`.

```bash
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp.com/edu/azuread from the dependency lock file
- Installing hashicorp.com/edu/azuread v2.41.0...
- Installed hashicorp.com/edu/azuread v2.41.0 (unauthenticated)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Wait for Replicated to Start

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/admin/infrastructure/automated-recovery

This code snippet waits for the Replicated service to become ready before proceeding with the snapshot restoration. It checks the status of Replicated and Retraced using 'replicatedctl' and waits until both are in the 'ready' state. It uses a loop with a sleep interval.

```bash
until replicatedctl system status --template '{{and (eq .Replicated \"ready\") (eq .Retraced \"ready\")}}' | grep -q true; do
  sleep 1
  echo "Replicated is not yet ready."
done
echo "Replicated is ready."
```

--------------------------------

### Establish Redis Session with Boundary Connect

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

This example demonstrates establishing a session to a Redis target using 'boundary connect -exec'. It executes the 'redis-cli ping' command through the established proxy, displaying proxy listening information before the client response. The {{boundary.port}} variable is dynamically replaced with the assigned proxy port.

```bash
$ boundary connect -exec redis-cli -target-name redis -target-scope-name databases -- -h 127.0.0.1 -p {{boundary.port}} ping

Proxy listening information:
  Address:             127.0.0.1
  Connection Limit:    -1
  Expiration:          Mon, 04 Oct 2021 17:56:11 MDT
  Port:                52015
  Protocol:            tcp
  Session ID:          s_qYgkJk8KdB
PONG

```

--------------------------------

### GET /feature-sets, GET /workspaces/:workspace_id/notification-configurations, GET /organizations/:organization_name/oauth-clients, GET /oauth-clients/:oauth_client_id/oauth-tokens, GET /organizations/:organization_name/feature-sets, GET /organizations, GET /runs/:run_id/policy-checks, GET /policy-sets/:policy_set_id/parameters, GET /organizations/:organization_name/ssh-keys, GET /users/:user_id/authentication-tokens - Pagination Support

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/api-docs/changelog

These endpoints now support pagination, allowing for more efficient retrieval of large datasets. This improves performance and usability.

```APIDOC
## GET /feature-sets

### Description
Retrieves a list of feature sets with pagination support.

### Method
GET

### Endpoint
/feature-sets

### Parameters
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /feature-sets?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **feature_sets** (array) - An array of feature set objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "feature_sets": [
    { /* feature set object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /workspaces/:workspace_id/notification-configurations

### Description
Retrieves a list of notification configurations for a workspace with pagination support.

### Method
GET

### Endpoint
/workspaces/:workspace_id/notification-configurations

### Parameters
#### Path Parameters
- **workspace_id** (string) - Required - The ID of the workspace.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /workspaces/workspace-xxxxxxxxxxxxxxxx/notification-configurations?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **notification_configurations** (array) - An array of notification configuration objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "notification_configurations": [
    { /* notification configuration object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /organizations/:organization_name/oauth-clients

### Description
Retrieves a list of OAuth clients for an organization with pagination support.

### Method
GET

### Endpoint
/organizations/:organization_name/oauth-clients

### Parameters
#### Path Parameters
- **organization_name** (string) - Required - The name of the organization.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /organizations/your-org-name/oauth-clients?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **oauth_clients** (array) - An array of OAuth client objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "oauth_clients": [
    { /* oauth client object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /oauth-clients/:oauth_client_id/oauth-tokens

### Description
Retrieves a list of OAuth tokens for an OAuth client with pagination support.

### Method
GET

### Endpoint
/oauth-clients/:oauth_client_id/oauth-tokens

### Parameters
#### Path Parameters
- **oauth_client_id** (string) - Required - The ID of the OAuth client.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /oauth-clients/oauth-client-xxxxxxxxxxxxxxxx/oauth-tokens?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **oauth_tokens** (array) - An array of OAuth token objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "oauth_tokens": [
    { /* oauth token object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /organizations/:organization_name/feature-sets

### Description
Retrieves a list of feature sets for an organization with pagination support.

### Method
GET

### Endpoint
/organizations/:organization_name/feature-sets

### Parameters
#### Path Parameters
- **organization_name** (string) - Required - The name of the organization.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /organizations/your-org-name/feature-sets?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **feature_sets** (array) - An array of feature set objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "feature_sets": [
    { /* feature set object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /organizations

### Description
Retrieves a list of organizations with pagination support.

### Method
GET

### Endpoint
/organizations

### Parameters
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /organizations?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **organizations** (array) - An array of organization objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "organizations": [
    { /* organization object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /runs/:run_id/policy-checks

### Description
Retrieves a list of policy checks for a run with pagination support.

### Method
GET

### Endpoint
/runs/:run_id/policy-checks

### Parameters
#### Path Parameters
- **run_id** (string) - Required - The ID of the run.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /runs/run-xxxxxxxxxxxxxxxx/policy-checks?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **policy_checks** (array) - An array of policy check objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "policy_checks": [
    { /* policy check object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /policy-sets/:policy_set_id/parameters

### Description
Retrieves a list of policy set parameters with pagination support.

### Method
GET

### Endpoint
/policy-sets/:policy_set_id/parameters

### Parameters
#### Path Parameters
- **policy_set_id** (string) - Required - The ID of the policy set.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /policy-sets/policy-set-xxxxxxxxxxxxxxxx/parameters?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **parameters** (array) - An array of policy set parameter objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "parameters": [
    { /* parameter object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /organizations/:organization_name/ssh-keys

### Description
Retrieves a list of SSH keys for an organization with pagination support.

### Method
GET

### Endpoint
/organizations/:organization_name/ssh-keys

### Parameters
#### Path Parameters
- **organization_name** (string) - Required - The name of the organization.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /organizations/your-org-name/ssh-keys?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **ssh_keys** (array) - An array of SSH key objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "ssh_keys": [
    { /* ssh key object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```

## GET /users/:user_id/authentication-tokens

### Description
Retrieves a list of authentication tokens for a user with pagination support.

### Method
GET

### Endpoint
/users/:user_id/authentication-tokens

### Parameters
#### Path Parameters
- **user_id** (string) - Required - The ID of the user.
#### Query Parameters
- **page[number]** (integer) - Optional - The page number for pagination.
- **page[size]** (integer) - Optional - The number of items per page.

### Request Example
```
GET /users/user-xxxxxxxxxxxxxxxx/authentication-tokens?page[number]=1&page[size]=10
```

### Response
#### Success Response (200)
- **authentication_tokens** (array) - An array of authentication token objects.
- **meta** (object) - Pagination metadata.

#### Response Example
```json
{
  "authentication_tokens": [
    { /* authentication token object */ }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "page_size": 10,
      "total": 100
    }
  }
}
```
```

--------------------------------

### Callback Payload Example

Source: https://developer.hashicorp.com/terraform/enterprise/api-docs/run-tasks/run-tasks-integration

This section provides a complete example of a callback payload, illustrating the data structure and all necessary fields.

```APIDOC
## GET /websites/developer_hashicorp_terraform/callback

### Description
This endpoint provides a complete callback payload example, detailing the structure of data returned upon task completion.

### Method
GET

### Endpoint
/websites/developer_hashicorp_terraform/callback

### Parameters
#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **data** (object) - The main payload object.
  - **type** (string) - The type of the payload, e.g., "task-results".
  - **attributes** (object) - Contains status and message information.
    - **status** (string) - The status of the task (e.g., "failed").
    - **message** (string) - A summary message of the task outcome.
    - **url** (string) - A URL to view the external service result.
  - **relationships** (object) - Contains related data, such as task outcomes.
    - **outcomes** (object) - Details about the task outcomes.
      - **data** (array) - An array of outcome objects.
        - **type** (string) - The type of the outcome, e.g., "task-result-outcomes".
        - **attributes** (object) - Attributes of the specific outcome.
          - **outcome-id** (string) - Unique identifier for the outcome.
          - **description** (string) - A description of the issue or finding.
          - **tags** (object) - Key-value pairs for categorizing the outcome.
            - **Status** (array) - An array of status objects (e.g., "Denied").
            - **Severity** (array) - An array of severity objects (e.g., "High").
            - **Cost Centre** (array) - An array of cost center objects (e.g., "IT-OPS").
          - **body** (string) - Detailed explanation or resolution steps for the outcome.
          - **url** (string) - A URL to view the specific outcome details.

#### Response Example
```json
{
  "data": {
    "type": "task-results",
    "attributes": {
      "status": "failed",
      "message": "0 passed, 0 skipped, 1 failed",
      "url": "https://external.service.dev/terraform-plan-checker/run-i3Df5to9ELvibKpQ"
    },
    "relationships": {
      "outcomes": {
        "data": [
          {
            "type": "task-result-outcomes",
            "attributes": {
              "outcome-id": "PRTNR-CC-TF-127",
              "description": "ST-2942: S3 Bucket will not enforce MFA login on delete requests",
              "tags": {
                "Status":  [
                  {
                    "label": "Denied",
                    "level": "error"
                  }
                ],
                "Severity": [
                  {
                    "label": "High",
                    "level": "error"
                  },
                  {
                    "label": "Recoverable",
                    "level": "info"
                  }
                ],
                "Cost Centre": [
                  {
                    "label": "IT-OPS"
                  }
                ]
              },
              "body": "# Resolution for issue ST-2942\n\n## Impact\n\nFollow instructions in the [AWS S3 docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/MultiFactorAuthenticationDelete.html) to manually configure the MFA setting.\n—-- Payload truncated —--",
              "url": "https://external.service.dev/result/PRTNR-CC-TF-127"
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

### Initialize Terraform Project and Configuration

Source: https://developer.hashicorp.com/terraform/intro/v1.1.x/core-workflow

This snippet demonstrates initializing a new Terraform project by creating a directory, initializing a Git repository, writing an initial Terraform configuration file (main.tf), and then running 'terraform init' to set up the project and download provider plugins. It's the first step in managing infrastructure as code.

```shell
# Create repository
$ git init my-infra && cd my-infra

Initialized empty Git repository in /.../my-infra/.git/

# Write initial config
$ vim main.tf

# Initialize Terraform
$ terraform init

Initializing provider plugins...
# ...
Terraform has been successfully initialized!

```

--------------------------------

### Get the path of a specific module

Source: https://developer.hashicorp.com/terraform/enterprise/v202402-1/policy-enforcement/sentinel/import/tfstate

This example shows how to retrieve the path of a specific module from the Terraform state. It uses the `tfstate.module()` function to access the module's details and then checks if its `path` contains a specific string, confirming the module's location.

```hcl
import "tfstate"

main = rule {
  tfstate.module(["foo"]).path contains "foo"
}
```

--------------------------------

### Configure External Vault Integration for Terraform Enterprise

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/install/automated/automating-the-installer

This example shows how to configure Terraform Enterprise to use an external HashiCorp Vault cluster for managing secrets. It requires enabling external Vault and providing the necessary connection details and authentication credentials.

```hcl
extern_vault_enable = 1
extern_vault_addr = "https://vault.example.com:8200"
extern_vault_role_id = "your-role-id"
extern_vault_secret_id = "your-secret-id"
```

--------------------------------

### Show a Policy Set API Request (HTTP)

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-2/api-docs/policy-sets

This example demonstrates how to make an HTTP GET request to retrieve a specific policy set by its ID. The `:id` path parameter is required. The `include` query parameter is optional and can be used to fetch related resources like workspaces or policies.

```http
GET /api/v2/policy-sets/:id?include=workspaces,policies HTTP/1.1
Host: app.terraform.io
Authorization: Bearer YOUR_API_TOKEN


```

--------------------------------

### Provisioner Failure Behavior Example (Terraform)

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/resources/provisioners

This example illustrates how to configure the failure behavior of a provisioner in Terraform using the `on_failure` attribute. Setting it to `continue` allows Terraform to proceed even if the provisioner fails.

```terraform
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    command    = "echo The server's IP address is ${self.private_ip}"
    on_failure = continue
  }
}

```

--------------------------------

### Terraform Lookup Function Examples

Source: https://developer.hashicorp.com/terraform/language/v1.15.x/functions/lookup

These examples demonstrate how to use the 'lookup' function in Terraform. The first example shows retrieving an existing key's value, while the second shows returning the default value for a non-existent key.

```hcl
> lookup({a="ay", b="bee"}, "a", "what?")
ay
> lookup({a="ay", b="bee"}, "c", "what?")
what?
```

```hcl
> lookup({a="ay", b="bee"}, "a", "what?")
ay
> lookup({a="ay", b="bee"}, "c", "what?")
what?
```

--------------------------------

### Terraform Input Variable Validation with String Prefix

Source: https://developer.hashicorp.com/terraform/language/v1.10.x/expressions/custom-conditions

Validates a string input variable to ensure it starts with a specific prefix. This is useful for enforcing formats like AMI IDs. It uses a condition to check the length and substring, and an error message to guide the user.

```Terraform
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```

--------------------------------

### Terraform Apply Command and Output

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/helm-provider

Demonstrates the terraform apply command and its output, showing the plan for resource creation and the final apply complete message with output values. This is a standard workflow for provisioning infrastructure with Terraform.

```shell
$ terraform apply
Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

## ...

Plan: 55 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + cluster_endpoint          = (known after apply)
  + cluster_name              = (known after apply)
  + cluster_security_group_id = (known after apply)
  + region                    = "us-east-2"

Do you want to perform these actions in workspace "learn-terraform-eks"?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

## ...

Apply complete! Resources: 55 added, 0 changed, 0 destroyed.

Outputs:

cluster_endpoint = "https://XXXXX.gr7.us-east-2.eks.amazonaws.com"
cluster_name = "education-eks-XXXX"
cluster_security_group_id = "sg-XXXX"
region = "us-east-2"
```

--------------------------------

### Operation Messages - Apply Start

Source: https://developer.hashicorp.com/terraform/internals/v1.10.x/machine-readable-ui

Indicates the start of an apply operation for a specific resource. Includes details about the resource, the action to be taken (create, update, delete, etc.), and resource identification.

```APIDOC
## Operation Messages - Apply Start

### Description
This message signals the beginning of an apply operation for a resource. It includes the resource's address, module, type, name, and the specific action (e.g., `create`, `update`, `delete`) that will be performed.

### Method
N/A (Log Message)

### Endpoint
N/A (Log Message)

### Parameters
N/A

### Request Example
```json
{
  "@level": "info",
  "@message": "random_pet.animal: Creating...",
  "@module": "terraform.ui",
  "@timestamp": "2021-05-25T13:32:41.825308-04:00",
  "hook": {
    "resource": {
      "addr": "random_pet.animal",
      "module": "",
      "resource": "random_pet.animal",
      "implied_provider": "random",
      "resource_type": "random_pet",
      "resource_name": "animal",
      "resource_key": null
    },
    "action": "create"
  },
  "type": "apply_start"
}
```

### Response
#### Success Response (200)
N/A (Log Message)

#### Response Example
```json
{
  "@level": "info",
  "@message": "random_pet.animal: Creating...",
  "@module": "terraform.ui",
  "@timestamp": "2021-05-25T13:32:41.825308-04:00",
  "hook": {
    "resource": {
      "addr": "random_pet.animal",
      "module": "",
      "resource": "random_pet.animal",
      "implied_provider": "random",
      "resource_type": "random_pet",
      "resource_name": "animal",
      "resource_key": null
    },
    "action": "create"
  },
  "type": "apply_start"
}
```
```

--------------------------------

### Install yum-utils for Repository Management

Source: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Installs the `yum-utils` package, which provides the `yum-config-manager` utility. This utility is essential for managing repositories on systems that use YUM, such as older versions of Amazon Linux.

```bash
sudo yum install -y yum-utils
```

--------------------------------

### Create and Apply Saved Plan via CLI

Source: https://developer.hashicorp.com/terraform/enterprise/v202502-2/workspaces/run/remote-operations

This example illustrates using `terraform plan -out <FILE>` to create and save a plan, and `terraform apply <FILE>` to apply a previously saved plan. This requires Terraform CLI v1.6.0 or later and the CLI integration configured with HCP Terraform.

```bash
terraform plan -out plan.tfplan
terraform apply plan.tfplan
```

--------------------------------

### Setup Terraform Environment for CI

Source: https://developer.hashicorp.com/terraform/plugin/testing/acceptance-tests/continuous-integration

Installs a specific version of Terraform using the hashicorp/setup-terraform action. It allows specifying the Terraform version and whether to use a Terraform wrapper. This is essential for running Terraform commands within a CI pipeline.

```yaml
      - uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: ${{ matrix.terraform-version }}
          terraform_wrapper: false
```

--------------------------------

### Install Terraform Provider (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/providers-plugin-framework-lab

This command builds and installs the Terraform provider locally. After running this, Terraform will be able to use the newly developed or updated provider in your configurations.

```bash
$ go install

```

--------------------------------

### List Docker Containers - sudo docker ps

Source: https://developer.hashicorp.com/terraform/enterprise/v202401-2/replicated/replicated-migration

Lists all currently running Docker containers. This command is used to verify that the Docker containers for Terraform Enterprise are up and running after an upgrade or during the setup of a new Flexible Deployment Options installation.

```shell
sudo docker ps

```

```shell
sudo docker ps

```

--------------------------------

### Define Resource Metadata and Schema in Framework

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/resources

This Go code defines the `Metadata` and `Schema` methods for a Framework resource (`exampleResource`). It sets the resource type name to 'example_resource' and defines a required string attribute 'attribute' with replacement-on-change and one-of validation.

```go
func (r *exampleResource) Metadata(ctx context.Context, req resource.MetadataRequest, resp *resource.MetadataResponse) {
    resp.TypeName = "example_resource"
}

func (r *exampleResource) Schema(_ context.Context, _ resource.SchemaRequest, resp *resource.SchemaResponse) {
    resp.Schema = schema.Schema{
        Attributes: map[string]schema.Attribute{
            // Required attributes
            "attribute": schema.StringAttribute{
                Required: true,
                PlanModifiers: []planmodifier.String{
                    stringplanmodifier.RequiresReplace(),
                },
                Validators: []validator.String{
                    stringvalidator.OneOf([]string{"a", "b"}...),
                },
            },
            /* ... */
        },
    }
}

```

--------------------------------

### Create Minio Bucket using AWS CLI

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/requirements/data-storage/minio-setup-guide

Creates an S3 bucket named 'tfe' in Minio using the AWS CLI. This requires setting environment variables for access key, secret key, and specifying the Minio endpoint URL.

```bash
export AWS_ACCESS_KEY_ID="<access key from above>"
export AWS_SECRET_ACCESS_KEY="<secret key from above>"

aws --region us-east-1 --endpoint-url http://<ip address from above>:9000 s3 mb s3://tfe
```

--------------------------------

### Configure Project Context in App Instantiation (TypeScript)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.12.x/create-and-deploy/project-setup

Provides project configuration context when instantiating the `App` class in TypeScript. This context can be accessed by constructs within the application after `cdktf synth` is run. This example demonstrates setting a custom tag value.

```typescript
import {
  Construct
} from "constructs";
import {
  App,
  TerraformStack
} from "cdktf";
import {
  AwsProvider,
  EC2
} from "./.gen/providers/aws";

class MyStack extends TerraformStack {
  constructor(scope: Construct, id: string) {
    super(scope, id);

    new AwsProvider(this, "aws", {
      region: "us-east-1",
    });

    new EC2.Instance(this, "Hello", {
      ami: "ami-2757f631",
      instanceType: "t2.micro",
      tags: {
        myConfig: this.node.getContext("myConfig"),
      },
    });
  }
}

const app = new App({ context: { myConfig: "value" } });
new MyStack(app, "hello-cdktf");
app.synth();

```

--------------------------------

### Define DynamoDB Table Provisioner with addOverride in Java

Source: https://developer.hashicorp.com/terraform/cdktf/v0.18.x/concepts/resources

This Java example demonstrates creating a DynamoDB table and then using `addOverride` to configure a `local-exec` provisioner. This provisioner is responsible for creating a backup of the DynamoDB table using an AWS CLI command.

```java
String tableName = "my-table";

DynamodbTable table = new DynamodbTable(this, "Hello", DynamodbTableConfig.builder()
                .name(tableName)
                .hashKey("id")
                .attribute(Arrays.asList(
                                DynamodbTableAttribute.builder() 
                                                .name("id")
                                                .type("S")
                                                .build()))
                .build());

table.addOverride("provisioner", Arrays.asList(
                new HashMap() {
                        {
                                put("local-exec", new HashMap<String, String>() {
                                        {
                                                put("command", "aws dynamodb create-backup --table-name " 
                                                                + tableName + " --backup-name " 
                                                                + tableName + "-backup");
                                        }
                                });
                        }
                }));
```

--------------------------------

### Authenticate Backup and Restore API Requests

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/administration/infrastructure/backup-restore

This example demonstrates how to authenticate API requests to the Terraform Enterprise backup and restore API. It shows the required `Authorization` header format, which includes the `Bearer` token. This token is specific to the TFE installation and must be protected.

```http
Authorization: Bearer <TOKEN>
```

--------------------------------

### Implement Open Method for Ephemeral Resource (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.13.x/ephemeral-resources/open

This Go code snippet demonstrates the implementation of the `Open` method for an ephemeral resource. It reads configuration from `ephemeral.OpenRequest`, simulates an external call to set a token, and writes the data to `ephemeral.OpenResponse.Result`. It also includes the `Schema` method for defining the resource's attributes.

```go
// ThingEphemeralResource defines the ephemeral resource implementation.
// Some ephemeral.EphemeralResource interface methods are omitted for brevity.
type ThingEphemeralResource struct {}

type ThingEphemeralResourceModel struct {
    Name  types.String `tfsdk:"name"
    Token types.String `tfsdk:"token"
}

func (e *ThingEphemeralResource) Schema(ctx context.Context, req ephemeral.SchemaRequest, resp *ephemeral.SchemaResponse) {
    resp.Schema = schema.Schema{
        Attributes: map[string]schema.Attribute{
            "name": schema.StringAttribute{
                Description: "Name of the thing to retrieve a token for.",
                Required:    true,
            },
            "token": schema.StringAttribute{
                Description: "Token for the thing.",
                Computed:    true,
            },
        },
    }
}

func (e *ThingEphemeralResource) Open(ctx context.Context, req ephemeral.OpenRequest, resp *ephemeral.OpenResponse) {
    var data ThingEphemeralResourceModel

    // Read Terraform config data into the model
    resp.Diagnostics.Append(req.Config.Get(ctx, &data)...)
    if resp.Diagnostics.HasError() {
        return
    }

    // Typically ephemeral resources will make external calls, however this example
    // hardcodes setting the token attribute to a specific value for brevity.
    data.Token = types.StringValue("token-123")

    // Save data into ephemeral result data
    resp.Diagnostics.Append(resp.Result.Set(ctx, &data)...)
}

```

--------------------------------

### Start Vault Development Server (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/codify-mgmt-enterprise

Starts a Vault development server with a predefined root token and TLS enabled. This command is used for local testing and development, providing a convenient way to run Vault without complex configuration.

```bash
vault server -dev -dev-root-token-id root -dev-tls
```

--------------------------------

### Terraform Enterprise Active/Active Deployment with Docker Compose

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/flexible-deployments/install/docker/install

This Docker Compose configuration deploys Terraform Enterprise in active/active mode. It requires external PostgreSQL, S3-compatible object storage, and Redis. Ensure you replace placeholder values with your actual credentials and configurations.

```yaml
---
name: terraform-enterprise
services:
  tfe:
    image: images.releases.hashicorp.com/hashicorp/terraform-enterprise:<vYYYYMM-#>
    environment:
      TFE_LICENSE: "<Hashicorp license>"
      TFE_HOSTNAME: "<TFE hostname (DNS) e.g. terraform.example.com>"
      TFE_ENCRYPTION_PASSWORD: "<Encryption password>"
      TFE_OPERATIONAL_MODE: "active-active"
      TFE_DISK_CACHE_VOLUME_NAME: "${COMPOSE_PROJECT_NAME}_terraform-enterprise-cache"
      TFE_TLS_CERT_FILE: "/etc/ssl/private/terraform-enterprise/cert.pem"
      TFE_TLS_KEY_FILE: "/etc/ssl/private/terraform-enterprise/key.pem"
      TFE_TLS_CA_BUNDLE_FILE: "/etc/ssl/private/terraform-enterprise/bundle.pem"
      TFE_IACT_SUBNETS: "<IACT subnet, eg. 10.0.0.0/8,192.168.0.0/24>"

      # Database settings. See the configuration reference for more settings.
      TFE_DATABASE_USER: "<Database user e.g. postgres>"
      TFE_DATABASE_PASSWORD: "<Database password e.g. postgres>"
      TFE_DATABASE_HOST: "<Database hostname and port e.g. postgres:5432>"
      TFE_DATABASE_NAME: "<Database name e.g. hashicorp>"
      TFE_DATABASE_PARAMETERS: "<Database parameters e.g. sslmode=disable>"

      # Object storage settings. See the configuration reference for more settings.
      TFE_OBJECT_STORAGE_TYPE: "s3"
      TFE_OBJECT_STORAGE_S3_ACCESS_KEY_ID: "<AWS Access Key ID>"
      TFE_OBJECT_STORAGE_S3_SECRET_ACCESS_KEY: "<AWS Secret Access Key>"
      TFE_OBJECT_STORAGE_S3_REGION: "<AWS Region e.g.us-east-1>"
      TFE_OBJECT_STORAGE_S3_BUCKET: "<Bucket name>"

      # Redis settings. See the configuration reference for more settings.
      TFE_REDIS_HOST: "<Redis hostname and port e.g. redis:6379>"
      TFE_REDIS_USER: "<Redis username>"
      TFE_REDIS_PASSWORD: "<Redis password>"
      TFE_REDIS_USE_TLS: "<To use tls? e.g. false>"
      TFE_REDIS_USE_AUTH: "<To use customized credential to authenticate? e.g. false>"

      # Vault cluster settings.
      # If you are using the default internal vault, this should be the private routable IP address of the node itself.
      TFE_VAULT_CLUSTER_ADDRESS: "https://<private_ip_of_the_node>:8201"
    cap_add:
      - IPC_LOCK
    read_only: true
    tmpfs:
      - "/tmp:mode=01777"
      - "/run"
      - "/var/log/terraform-enterprise"
    ports:
      - "80:80"
      - "443:443"
      - "8201:8201"
    volumes:
      - type: bind
        source: /var/run/docker.sock
        target: /run/docker.sock
      - type: bind
        source: ./certs
        target: /etc/ssl/private/terraform-enterprise
      - type: volume
        source: terraform-enterprise-cache
        target: /var/cache/tfe-task-worker/terraform
volumes:
  terraform-enterprise-cache:

```

--------------------------------

### Terraform Plan Command Output

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/provider-versioning

This example demonstrates the output of the 'terraform plan' command after potential provider upgrades. It shows that no changes are needed, indicating the infrastructure matches the configuration with the current provider versions. This step is vital for verifying compatibility before applying changes.

```bash
$ terraform plan
random_pet.petname: Refreshing state... [id=gratefully-radically-quickly-fitting-troll]
aws_s3_bucket.sample: Refreshing state... [id=gratefully-radically-quickly-fitting-troll]

No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and
found no differences, so no changes are needed.

```

--------------------------------

### Change Directory to Terraform AWS ASG Example

Source: https://developer.hashicorp.com/terraform/tutorials/aws/aws-asg

Navigates into the cloned Terraform AWS ASG example repository directory. This is necessary to access and modify the configuration files.

```bash
cd learn-terraform-aws-asg

```

--------------------------------

### Define AWS Instance Resource in Terraform

Source: https://developer.hashicorp.com/terraform/tutorials/cli/state-cli

This Terraform configuration defines an AWS EC2 instance with specified AMI, instance type, security group, and user data for initial setup. The user data script installs Apache, configures it to listen on port 8080, and creates a simple index.html.

```hcl
resource "aws_instance" "example_new" {
  ami                    = data.aws_ami.ubuntu.id
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.sg_8080.id]
  user_data              = <<-EOF
              #!/bin/bash
              apt-get update
              apt-get install -y apache2
              sed -i -e 's/80/8080/' /etc/apache2/ports.conf
              echo "Hello World" > /var/www/html/index.html
              systemctl restart apache2
              EOF
  tags = {
    Name = "terraform-learn-state-ec2"
  }
}
```

--------------------------------

### Launch Go Web Application

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/packer

Execute the Go web application using the `go run` command. This command compiles and runs the specified Go file.

```bash
$ go run webapp.go
```

--------------------------------

### Common SAML Configuration Errors and Resolutions

Source: https://developer.hashicorp.com/terraform/enterprise/v202302-1/saml/troubleshooting

This section lists common configuration errors encountered during SAML SSO setup in Terraform Enterprise and provides specific resolution steps for each. These errors typically stem from incorrect URL configurations or invalid NameID formats.

```text
**CONFIGURATION ERROR: `https://<TFE HOSTNAME>/metadata` is not a valid audience for this Response - Valid audiences: `https://<TFE HOSTNAME>/users/saml/metadata`**
Resolution: Correct the audience URL in the identity provider settings by pasting the ACS Consumer URL from Terraform Enterprise.

**CONFIGURATION ERROR: The response was received at `https://<TFE HOSTNAME>/auth` instead of `https://<TFE HOSTNAME>/users/saml/auth`**
Resolution: Correct the recipient URL in the identity provider settings by pasting the Metadata URL from Terraform Enterprise.

**ERROR: Validation failed: Email is invalid, Email is not a valid email address, Username has already been taken**
Resolution: Configure the identity provider to use an email address as the NameID value.

**ERROR: Mail::AddressList can not parse |{onelogin:email}|: Only able to parse up to "{onelogin:email}"**
Resolution: Ensure the NameID is not blank by configuring the identity provider to send an email address for NameID.

**ERROR: nested asn1 error**
Resolution: Verify the identity provider certificate is valid and correctly pasted into Terraform Enterprise.

**ERROR: Issuer of assertion not found or multiple**
Resolution: If using an F5 load balancer, ensure it's signing responses as per the 'Using APM as a SAML IdP' guide. Otherwise, contact support.
```

--------------------------------

### Build AWS Provider and VPC Module (TypeScript)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.11.x/create-and-deploy/configuration-file

This example demonstrates how to use `cdktf get` to build both the AWS provider and a specific Terraform module (e.g., `terraform-aws-modules/vpc/aws`). It specifies the desired provider version and the module to be fetched. The output is a JSON configuration for the CDKTF CLI.

```json
{
  "language": "typescript",
  "app": "npm run --silent compile && node main.js",
  "terraformModules": ["terraform-aws-modules/vpc/aws"],
  "terraformProviders": ["aws@~> 2.0"]
}
```

```json
{
  "language": "typescript",
  "app": "npm run --silent compile && node main.js",
  "terraformModules": ["terraform-aws-modules/vpc/aws"],
  "terraformProviders": ["aws@~> 2.0"]
}
```

--------------------------------

### Complete Terraform Configuration for OIDC Auth

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0/boundary-deploy%3Adev

This is a complete `main.tf` file demonstrating the setup of an OIDC authentication method and account using the HashiCorp Boundary Terraform provider. It includes provider configuration, the `boundary_auth_method_oidc` resource, and the `boundary_account_oidc` resource. Remember to replace placeholder values with your actual credentials and configuration.

```terraform
terraform {
  required_providers {
    boundary = {
      source  = "hashicorp/boundary"
      version = "1.0.12"
    }
  }
}

output "auth-method-id" {
  value = boundary_auth_method_oidc.provider.id
}

provider "boundary" {
  addr             = "http://127.0.0.1:9200"
  recovery_kms_hcl = <<EOT
kms "aead" {
  purpose = "recovery"
  aead_type = "aes-gcm"
  key = "gm0aHvU1ENpc9mrB5Kt2bqCyh9PODOqnDznryFksyI0="
  key_id = "global_recovery"
}
EOT
}

resource "boundary_auth_method_oidc" "provider" {
  name               = "Auth0"
  description        = "OIDC auth method for Auth0"
  scope_id           = "o_1234567890"
  issuer             = "https://dev-1vdl8c0q.us.auth0.com/"
  client_id          = "zbaJLTZh3n14WqSV7qQ9onuIVRDaZdzx"
  client_secret      = "t35c9NNw1aZ8haQKYJjCL0lauNOSp5UNPovUJXo8Ea2sPZAR1DszEowX-5-lg-Xr"
  signing_algorithms = ["RS256"]
  api_url_prefix     = "http://localhost:9200"
}

resource "boundary_account_oidc" "oidc_user" {
  name           = "user1"
  description    = "OIDC account for user1"
  auth_method_id = boundary_auth_method_oidc.provider.id
  issuer  = "https://dev-1vdl8c0q.us.auth0.com/"
  subject = "auth0|6077581e2ce19d006dfaf211"
}

```

--------------------------------

### Declare Terraform Variable with Validation

Source: https://developer.hashicorp.com/terraform/docs/configuration/variables

This example demonstrates how to add validation rules to a Terraform variable. The `image_id` variable includes a `validation` block that checks if the input string is longer than 4 characters and starts with 'ami-'. If the condition fails, a custom error message is displayed.

```Terraform
variable "image_id" {
  type        = string
  description = "The ID of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI ID, starting with \"ami-\"."
  }
}

```

--------------------------------

### Initialize Terraform and Install Providers

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/kubernetes-crd-faas

The `terraform init` command initializes the Terraform working directory. It downloads and installs the necessary provider plugins (e.g., `hashicorp/helm`, `hashicorp/time`, `hashicorp/kubernetes`) as specified in your Terraform configuration. This step is required before running other Terraform commands like `plan` or `apply`.

```bash
$ terraform init
Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/helm from the dependency lock file
- Reusing previous version of hashicorp/time from the dependency lock file
- Reusing previous version of hashicorp/kubernetes from the dependency lock file
- Installing hashicorp/helm v2.2.0...
- Installed hashicorp/helm v2.2.0 (signed by HashiCorp)
- Installing hashicorp/time v0.7.2...
- Installed hashicorp/time v0.7.2 (signed by HashiCorp)
- Installing hashicorp/kubernetes v2.6.1...
- Installed hashicorp/kubernetes v2.6.1 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Run HCP Terraform Agent with Docker

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/agents

This snippet demonstrates how to start the HCP Terraform agent using the official Docker image. It requires setting the agent token and optionally a name as environment variables. The agent then connects to an HCP Terraform agent pool.

```shell
export TFC_AGENT_TOKEN=your-token
export TFC_AGENT_NAME=your-agent-name
docker run --platform=linux/amd64 -e TFC_AGENT_TOKEN -e TFC_AGENT_NAME hashicorp/tfc-agent:latest

```

--------------------------------

### Get GKE Node Pool Locations

Source: https://developer.hashicorp.com/terraform/tutorials/kubernetes/gke

Retrieves the locations (zones) where the GKE cluster's node pools are deployed. This command uses `gcloud` to describe the cluster and formats the output to show only the locations. This is useful for understanding the high availability setup of the cluster.

```bash
gcloud container clusters describe $(terraform output -raw kubernetes_cluster_name) --region us-central1 --format='default(locations)'
```

```bash
gcloud container clusters describe $(terraform output -raw kubernetes_cluster_name) --region us-central1 --format='default(locations)'
```

--------------------------------

### Navigate to Terraform Examples Directory

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-resource-update

This command changes the current directory to the 'examples/order' directory, which contains a sample Terraform configuration for the HashiCups provider.

```shell
$ cd examples/order
```

```shell
$ cd examples/order
```

--------------------------------

### Terraform Configuration Examples for Variadic Dynamic Arguments

Source: https://developer.hashicorp.com/terraform/plugin/framework/functions/parameters/dynamic

Provides examples of Terraform configurations calling a function with a variadic dynamic parameter. These examples demonstrate how different argument types (none, string, boolean/number, string/tuple/list) are passed and how they are represented as `[]types.Dynamic` within the function.

```hcl
# []types.Dynamic{}
provider::example::example()

# []types.Dynamic{types.String}
provider::example::example("hello world")

# []types.Dynamic{types.Bool, types.Number}
provider::example::example(true, 1)

# []types.Dynamic{types.String, types.Tuple[types.String, types.String], types.List[types.String]}
provider::example::example("hello", ["one", "two"], tolist(["one", "two"]))

```

--------------------------------

### Sample GitHub App Installations List Response (JSON)

Source: https://developer.hashicorp.com/terraform/enterprise/v202401-2/api-docs/github-app-installations

This is a sample JSON response when listing GitHub App installations. It includes details such as the installation's ID, type, name, GitHub installation ID, icon URL, installation type, and a URL to manage the installation on GitHub.

```json
{
    "data": [
        {
            "id": "ghain-BYrbNeGQ8nAzKouu",
            "type": "github-app-installations",
            "attributes": {
                "name": "octouser",
                "installation-id": 54810170,
                "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
                "installation-type": "User",
                "installation-url": "https://github.com/settings/installations/54810170"
            }
        }
    ]
}

```

--------------------------------

### Update CA Certificates - RHEL 7

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-3/install/interactive/installer

Updates the CA certificates bundle on RHEL 7 UBI minimal images. This command ensures that custom CA certificates are trusted by the system. It is used in conjunction with adding certificate files to the appropriate trust store directory.

```dockerfile
RUN update-ca-trust
```

--------------------------------

### Update CA Certificates in RHEL 7 Dockerfile

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/install/interactive/installer

This snippet shows how to update CA certificates in a RHEL 7 UBI minimal Docker image. It adds custom certificates to the trust anchor directory and then uses 'update-ca-trust' to integrate them. This is essential for secure communication with private resources.

```dockerfile
FROM registry.access.redhat.com/ubi7/ubi-minimal:7.9-503

# Update installed packages and clear cache
RUN microdnf --assumeyes update && rm --recursive --force /var/cache/yum

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/share/pki/ca-trust-source/anchors
ADD example-intermediate-ca.crt /usr/share/pki/ca-trust-source/anchors

# Update the CA certificates bundle to include newly added CA certificates.
RUN update-ca-trust

# Install required software for Terraform Enterprise.
RUN microdnf --assumeyes install \
  unzip sudo git openssh wget curl psmisc iproute nmap-ncat openssl && \
  microdnf clean all && \
  curl --location --output /usr/local/bin/envdir \
  https://github.com/jezdez/envdir/releases/download/0.7/envdir-0.7.pyz && \
  chmod +x /usr/local/bin/envdir
```

--------------------------------

### Configure Security Group Ingress/Egress (Go)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.17.x/concepts/resources

This Go code example illustrates how to configure a security group, including defining ingress rules for specific ports and an egress rule allowing all outbound traffic. It uses helper functions for string and number conversions.

```go
    ports := []float64{22, 80, 443, 5432}
    ingress := make([]securitygroup.SecurityGroupIngress, 0)
    for _, port := range ports {
        ingress = append(ingress, securitygroup.SecurityGroupIngress{
            FromPort:   jsii.Number(port),
            ToPort:     jsii.Number(port),
            CidrBlocks: &[]*string{jsii.String("0.0.0.0/0")},
            Protocol:   jsii.String("-1"),
        })
    }

    securitygroup.NewSecurityGroup(stack, jsii.String("security2"), &securitygroup.SecurityGroupConfig{
        Name:  jsii.String("security2"),
        VpcId: jsii.String("vpcs"),
        Egress: &[]securitygroup.SecurityGroupEgress{
            {
                FromPort:   jsii.Number(0),
                ToPort:     jsii.Number(0),
                CidrBlocks: &[]*string{jsii.String("0.0.0.0/0")},
                Protocol:   jsii.String("-1"),
            },
        },
        Ingress: &ingress,
    })
```

--------------------------------

### Remove Example Files - Shell Script

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This command removes example resource, data source, and function files from the internal provider directory. It's a preparatory step for developing a custom provider.

```shell
$ rm internal/provider/example_*

```

--------------------------------

### Import and Use Generated Classes in Java

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/providers

This Java example demonstrates importing and initializing the AwsProvider, Instance, DnsimpleProvider, and ZoneRecord resources using CDKTF. It shows how to configure providers with variables and create resources with dependencies.

```java
import com.hashicorp.cdktf.TerraformVariableConfig;
import software.constructs.Construct;
import com.hashicorp.cdktf.TerraformStack;
import com.hashicorp.cdktf.TerraformVariable;
import imports.aws.instance.Instance;
import imports.aws.instance.InstanceConfig;
import imports.aws.provider.AwsProvider;
import imports.aws.provider.AwsProviderConfig;
import imports.dnsimple.provider.DnsimpleProvider;
import imports.dnsimple.provider.DnsimpleProviderConfig;
import imports.dnsimple.zone_record.ZoneRecord;
import imports.dnsimple.zone_record.ZoneRecordConfig;

public class MainImportClasses extends TerraformStack {

    public MainImportClasses(Construct scope, String id){
        super(scope, id);

        new AwsProvider(this, "aws", AwsProviderConfig.builder() 
                .region("us-east-1")
                .build()
        );

        Instance instance = new Instance(this, "Hello", InstanceConfig.builder() 
                .ami("ami-2757f631")
                .instanceType("t2.micro")
                .build()
        );

        TerraformVariable dnsimpleToken = new TerraformVariable(this, "dnsimpleToken", TerraformVariableConfig.builder() 
                .type("string")
                .description("dnsimple token")
                .sensitive(true)
                .build()
        );

        TerraformVariable dnsimpleAccount = new TerraformVariable(this, "dnsimpleAccount", TerraformVariableConfig.builder() 
                .type("string")
                .description("dnsimple account")
                .sensitive(true)
                .build()
        );

        new DnsimpleProvider(this, "dnsimple", DnsimpleProviderConfig.builder() 
                .token(dnsimpleToken.getStringValue())
                .account(dnsimpleAccount.getStringValue())
                .build()
        );

        new ZoneRecord(this, "web-www", ZoneRecordConfig.builder() 
                .zoneName("example.com")
                .name("web")
                .value(instance.getPublicIp())
                .type("A")
                .build()
        );
    }

     public static void main(String[] args) {
     final App app = new App();

```

--------------------------------

### Update CA Certificates in Ubuntu Dockerfile

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/install/interactive/installer

This snippet demonstrates how to add custom CA certificates to the trust store in an Ubuntu-based Docker image. It involves adding certificate files and then running 'update-ca-certificates' to apply the changes. This is crucial for establishing secure connections to internal or private services.

```dockerfile
FROM ubuntu:bionic

# Install required software for Terraform Enterprise.
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    sudo unzip daemontools git-core awscli ssh wget curl psmisc iproute2 openssh-client redis-tools netcat-openbsd ca-certificates

# Include all necessary CA certificates.
ADD example-root-ca.crt /usr/local/share/ca-certificates/
ADD example-intermediate-ca.crt /usr/local/share/ca-certificates/

# Update the CA certificates bundle to include newly added CA certificates.
RUN update-ca-certificates
```

--------------------------------

### Add Initialize Script to Custom Worker Image

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/interactive/installer

This Dockerfile snippet demonstrates how to add a custom initialization script to a worker image. The script, located at `/usr/local/bin/init_custom_worker.sh`, will be executed before Terraform Enterprise runs `terraform init` during plans and applies. This is applicable only to the `legacy` run pipeline mode.

```dockerfile
ADD init_custom_worker.sh /usr/local/bin/init_custom_worker.sh

```

```dockerfile
ADD init_custom_worker.sh /usr/local/bin/init_custom_worker.sh

```

--------------------------------

### Clone Terraform Provider Versioning Repository

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/provider-versioning

Clones the example repository for the Terraform provider versioning tutorial. This repository contains pre-initialized Terraform configurations necessary for the tutorial.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-provider-versioning

```

--------------------------------

### Example output of tf-migrate execute

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/migrate/tf-migrate/reference/execute

This example demonstrates the successful execution of the `tf-migrate execute` command. It shows the output of the init, plan, and apply commands, a summary of the migration metrics, workspace URLs, and a pull request link if applicable.

```bash
$ tf-migrate execute
✓ Init command ran successfully
✓ Plan command ran successfully and changes are detected
✓ Apply command ran successfully
Apply complete! Resources: 7 added, 0 changed, 0 destroyed.


Migration Summary
┌───────────────────────────────┬───────┐
│             Metric            │ Count │
├───────────────────────────────┼───────┤
│ Number of Projects Migrated   │     2 │
│ Number of Directories Skipped │     0 │
│ Number of New Workspaces      │     2 │
│ Number of Variables Migrated  │     8 │
└───────────────────────────────┴───────┘
┌───────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                           Workspace URLs                                          │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ https://app.terraform.io//workspaces/web_default                                             │
│ https://app.terraform.io//workspaces/api_default                                             │
└───────────────────────────────────────────────────────────────────────────────────────────────────┘
┌────────────────────────────────────────────────────────────────────────┐
│                            Pull Request Link                           │
├────────────────────────────────────────────────────────────────────────┤
│ https://github.com//learn-terraform-migrate/pull/1                │
└────────────────────────────────────────────────────────────────────────┘

```

```bash
$ tf-migrate execute
✓ Init command ran successfully
✓ Plan command ran successfully and changes are detected
✓ Apply command ran successfully
Apply complete! Resources: 7 added, 0 changed, 0 destroyed.
 
 
Migration Summary
┌───────────────────────────────┬───────┐
│             Metric            │ Count │
├───────────────────────────────┼───────┤
│ Number of Projects Migrated   │     2 │
│ Number of Directories Skipped │     0 │
│ Number of New Workspaces      │     2 │
│ Number of Variables Migrated  │     8 │
└───────────────────────────────┴───────┘
┌───────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                           Workspace URLs                                          │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ https://app.terraform.io//workspaces/web_default                                             │
│ https://app.terraform.io//workspaces/api_default                                             │
└───────────────────────────────────────────────────────────────────────────────────────────────────┘
┌────────────────────────────────────────────────────────────────────────┐
│                            Pull Request Link                           │
├────────────────────────────────────────────────────────────────────────┤
│ https://github.com//learn-terraform-migrate/pull/1                │
└────────────────────────────────────────────────────────────────────────┘


```

--------------------------------

### Terraform pathexpand Function Examples

Source: https://developer.hashicorp.com/terraform/language/v1.12.x/functions/pathexpand

Demonstrates the usage of the pathexpand function in Terraform to expand paths starting with '~' to the user's home directory. This function is useful for locating files like SSH keys but should be used cautiously in resource arguments to avoid diffing issues.

```terraform
pathexpand("~/.ssh/id_rsa")
# Expected output: /home/steve/.ssh/id_rsa

pathexpand("/etc/resolv.conf")
# Expected output: /etc/resolv.conf
```

--------------------------------

### Configure Request Forwarding

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/v1.25.x/agents

Enables HCP Terraform to securely access private infrastructure resources by forwarding requests. By default, request forwarding is disabled. To enable it, start the agent with the `-request-forwarding` command line argument. Workload types can be modified via the `-accept` parameter.

```APIDOC
## Agent Configuration for Request Forwarding

### Description
Configure the agent to accept forwarded requests from HCP Terraform, allowing secure access to private infrastructure resources. This feature can be enabled using a command-line argument and its behavior can be further customized.

### Method
Command Line Argument

### Endpoint
N/A

### Parameters
#### Command Line Arguments
- **-request-forwarding** (flag) - Required - Enables request forwarding.
- **-accept** (string) - Optional - Modifies workload types handled by the agent (e.g., "plans,applies,request-forwarding").

### Request Example
```bash
./agent -request-forwarding
./agent -accept="plans,applies" -request-forwarding
```

### Response
N/A (Configuration is applied on agent startup)

### Error Handling
- If request forwarding is not enabled, agents will not process forwarded requests.
- Incorrect values for the `-accept` parameter may lead to unexpected agent behavior.
```

--------------------------------

### Instantiate KubernetesWebAppDeployment Construct in Java

Source: https://developer.hashicorp.com/terraform/cdktf/v0.13.x/concepts/constructs

This Java example shows how to use the 'KubernetesWebAppDeployment' construct within a CDK for Terraform application. It configures the Kubernetes provider and defines the deployment's properties, including image, replicas, and application details. Requires 'cdktf' and 'constructs' Java libraries.

```java
package com.mycompany.app;

import java.nio.file.Paths;

import com.hashicorp.cdktf.App;
import com.hashicorp.cdktf.TerraformStack;
import software.constructs.Construct;
import java.util.*;
import imports.kubernetes.provider.*;

public class Main extends TerraformStack {
    public Main(final Construct scope, final String name) {
        super(scope, name);

        KubernetesProvider.Builder.create(this, "kind")
                .configPath(Paths.get(System.getProperty("user.dir"), "kubeconfig.yaml").toString())
                .build();

        final HashMap<String, String> properties = new HashMap<>();
        properties.put("image", "lambci/lambda:latest");
        properties.put("replicas", "2");
        properties.put("app", "myapp");
        properties.put("component", "frontend");
        properties.put("environment", "dev");

        new KubernetesWebAppDeployment(this, "deployment", properties);
    }
    public static void main(String[] args) {
        final App app = new App();
        new Main(app, "demo");
        app.synth();

```

--------------------------------

### Enable Request Forwarding for HCP Terraform Agent

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/agents

To enable request forwarding for HCP Terraform agents, start the agent process with the `-request-forwarding` command-line argument. This allows HCP Terraform to securely access private infrastructure resources. By default, request forwarding is disabled.

```bash
agent -request-forwarding
```

--------------------------------

### Create and Run Docker Container with NGINX

Source: https://developer.hashicorp.com/terraform/tutorials/cli/state-import

This command creates a Docker container named 'hashicorp-learn' using the latest NGINX image. It runs in detached mode and publishes port 80 of the container to port 8080 on the host machine. The output shows the process of pulling the image if it's not found locally and starting the container.

```bash
$ docker run --name hashicorp-learn --detach --publish "0.0.0.0:8080:80" nginx:latest
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
afb6ec6fdc1c: Pull complete
dd3ac8106a0b: Pull complete
8de28bdda69b: Pull complete
a2c431ac2669: Pull complete
e070d03fd1b5: Pull complete
Digest: sha256:883874c218a6c71640579ae54e6952398757ec65702f4c8ba7675655156fcca6
Status: Downloaded newer image for nginx:latest
e7ba41fd94e51c501533241e4cffd307fbda81c5b402c372d989c4578518d2e5

```

--------------------------------

### Create HashiCups Order Resource Directory (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-documentation-generation

Creates a new directory for the `hashicups_order` resource using `mkdir -p`. This command ensures parent directories are created if they don't exist.

```shell
$ mkdir -p examples/resources/hashicups_order
```

--------------------------------

### Configure Project Context via App Instantiation

Source: https://developer.hashicorp.com/terraform/cdktf/v0.16.x/create-and-deploy/project-setup

Provides project configuration context when instantiating the `App` class in your CDKTF application. This method allows dynamic context setting at runtime, which can be passed to constructs. The example demonstrates setting a custom tag for an AWS EC2 instance.

```typescript
import {
  Construct
} from "constructs";
import { App, TerraformStack } from "cdktf";
import { AwsProvider } from "./.gen/providers/aws/provider";
import { Instance } from "./.gen/providers/aws/instance";

class MyStack extends TerraformStack {
  constructor(scope: Construct, id: string) {
    super(scope, id);

    new AwsProvider(this, "aws", {
      region: "us-east-1",
    });

    new Instance(this, "Hello", {
      ami: "ami-2757f631",
      instanceType: "t2.micro",
      tags: {
        myConfig: this.node.getContext("myConfig"),
      },
    });
  }
}

const app = new App({ context: { myConfig: "value" } });
new MyStack(app, "hello-cdktf");
app.synth();

```

--------------------------------

### Clone GitHub Repository

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

Clones the specified GitHub repository to download the example files locally. This is the initial step to obtain the project's codebase.

```bash
$ git clone git@github.com:hashicorp-education/learn-boundary-target-aware-workers.git

```

--------------------------------

### Sample Specific GitHub App Installation Response (JSON)

Source: https://developer.hashicorp.com/terraform/enterprise/v202401-2/api-docs/github-app-installations

This is a sample JSON response when retrieving details for a specific GitHub App installation. It contains the installation's ID, type, name, GitHub installation ID, icon URL, installation type, and a URL to manage the installation on GitHub.

```json
{
    "data": {
        "id": "ghain-R4xmKTaxnhLFioUq",
        "type": "github-app-installations",
        "attributes": {
            "name": "octouser",
            "installation-id": 54810170,
            "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
            "installation-type": "User",
            "installation-url": "https://github.com/settings/installations/54810170"
        }
    }
}

```

--------------------------------

### Example Output of Configuration Watch

Source: https://developer.hashicorp.com/terraform/cloud-docs/stacks/create

This is an example of the output from the `terraform stacks configuration watch` command, showing the status of different deployment groups within a Stack. It indicates completion, pending status, or failure.

```text
[Stack Id: st-MLQLSJVrdtGazA4aU]
✓ Configuration: 'stc-6fSRO81hOzTPKMM'                    [Completed]    [11s]
↻ Deployment Group: 'many_default'                        [Pending]      [58s]
↻ Deployment Group: 'some_default'                        [Pending]      [58s]
↻ Deployment Group: 'single_default'                      [Failed]       [6s]

Press q to quit
```

--------------------------------

### Start HashiCups Service with Docker Compose

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-resource-delete

This command starts the HashiCups service using Docker Compose. The service will be accessible on port 19090 and will print log messages to the terminal.

```bash
$ docker-compose up
```

--------------------------------

### Verify Provider Server Execution Output

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-provider

This output demonstrates the result of manually running the Go provider server executable. It shows an error message indicating that the binary is a plugin and not meant to be executed directly, which is the expected outcome for verification.

```bash
$ go run main.go
This binary is a plugin. These are not meant to be executed directly.
Please execute the program that consumes these plugins, which will
load any plugins automatically
exit status 1
```

--------------------------------

### Install Terraform MCP Server Development Version (Go)

Source: https://developer.hashicorp.com/terraform/docs/tools/mcp-server/deploy

This Go command installs the development version of the terraform-mcp-server from the main branch. It's useful for accessing the latest features or contributing to development.

```bash
$ go install github.com/hashicorp/terraform-mcp-server/cmd/terraform-mcp-server@main
```

--------------------------------

### Get AI Resources from Google Provider (JSON Request)

Source: https://developer.hashicorp.com/terraform/docs/tools/mcp-server/prompt

This snippet shows the JSON request payload sent to the Terraform MCP server to retrieve a list of AI-related resources from the Google provider. It specifies the data type, provider name, namespace, version, and a service slug for filtering.

```json
{
  "provider_Data_Type": "resources",
  "provider_Name": "google",
  "provider_Namespace": "hashicorp",
  "providerVersion": "latest",
  "serviceSlug": "ai"
}
```

--------------------------------

### Initialize Terraform pg Backend with Partial Configuration

Source: https://developer.hashicorp.com/terraform/language/v1.3.x/settings/backends/pg

This demonstrates initializing the Terraform pg backend using a partial configuration and providing the connection string via the `init` command. This is recommended for managing sensitive credentials.

```bash
terraform init -backend-config="conn_str=postgres://user:pass@db.example.com/terraform_backend"

```

--------------------------------

### Setup Terraform Provider Schema with SDKv2

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/providers

This Go code snippet illustrates how to define a Terraform provider schema, including its attributes, configuration function, and maps for resources and data sources using the SDKv2. It's a foundational example for creating custom Terraform providers.

```go
func New() (*schema.Provider, error) {
    return &schema.Provider{
        Schema: map[string]*schema.Schema{
            "attribute": {
                /* ... */
            },
        },
        ConfigureContextFunc: configureProvider,
        ResourcesMap: map[string]*schema.Resource{
            "exampleResource": exampleResource(),
            /* ... */
        },
        DataSourcesMap: map[string]*schema.Resource{
            "exampleDataSource": exampleDataSource(),
            /* ... */
        },
    }, nil
}

```

```go
func New() (*schema.Provider, error) {
    return &schema.Provider{
        Schema: map[string]*schema.Schema{
            "attribute": {
                /* ... */
            },
        },
        ConfigureContextFunc: configureProvider,
        ResourcesMap: map[string]*schema.Resource{
            "exampleResource": exampleResource(),
            /* ... */
        },
        DataSourcesMap: map[string]*schema.Resource{
            "exampleDataSource": exampleDataSource(),
            /* ... */
        },
    }, nil
}

```

--------------------------------

### Provision Start Event

Source: https://developer.hashicorp.com/terraform/internals/v1.4.x/machine-readable-ui

Indicates the beginning of a provisioning process for a resource using a specific provisioner.

```APIDOC
## Provision Start Event

### Description
This event marks the start of a provisioning action for a resource, specifying the type of provisioner being used.

### Method
N/A (This is a log/event message, not an API endpoint)

### Endpoint
N/A

### Parameters
#### Query Parameters
N/A

#### Request Body
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```json
{
  "@level": "info",
  "@message": "null_resource.none[0]: Provisioning with 'local-exec'...",
  "@module": "terraform.ui",
  "@timestamp": "2021-03-26T16:38:43.997431-04:00",
  "hook": {
    "resource": {
      "addr": "null_resource.none[0]",
      "module": "",
      "resource": "null_resource.none[0]",
      "implied_provider": "null",
      "resource_type": "null_resource",
      "resource_name": "none",
      "resource_key": 0
    },
    "provisioner": "local-exec"
  },
  "type": "provision_start"
}
```
```

--------------------------------

### Terraform File Provisioner Example

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/upgrade-guides/1-1

This snippet demonstrates the usage of the `file` provisioner in Terraform. It uploads a local file to a specified destination on a remote system. In Terraform v1.1 and later, relative paths are interpreted relative to the target user's home directory by default, without shell expansion.

```terraform
provisioner "file" {
  source      = "local.txt"
  destination = "remote.txt"
}

```

--------------------------------

### Example Widget Terraform Configuration in Go

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/v2.15.x/best-practices/testing

The `testAccExampleResource` function in Go generates a Terraform configuration string for an `example_widget` resource. It takes a `name` as input and returns a formatted string that defines the resource with `active = true` and the provided name. This is used within acceptance tests to provision a widget for testing.

```go
func testAccExampleResource(name string) string {
    return fmt.Sprintf(`
resource "example_widget" "foo" {
  active = true
  name = "%s"
}`, name)
}
```

--------------------------------

### Poll Terraform Enterprise Health Check Endpoint

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

This command polls the `/_health_check` endpoint of Terraform Enterprise until a 200 OK response is received, indicating the application has started successfully. It uses `curl` with SSL verification disabled and a connection timeout of 5 seconds, retrying every 5 seconds.

```shell
while ! curl -ksfS --connect-timeout 5 https://tfe.example.com/_health_check; do
    sleep 5
done

```

--------------------------------

### Define and Deprecate example_widget Resource (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.12.x/deprecations

This Go code defines the schema for the 'example_widget' resource, including a deprecation message. It also shows how the Create, Read, Update, and Delete operations append a deprecation diagnostic. This ensures users are notified about the deprecation when interacting with the resource.

```go
package main

import (
	"context"

	"github.com/hashicorp/terraform-plugin-framework/diag"
	"github.com/hashicorp/terraform-plugin-framework/resource"
	"github.com/hashicorp/terraform-plugin-framework/resource/schema"
)

type exampleWidgetResource struct {
	// ... other fields ...
}

func NewWidgetResource() resource.Resource {
	return &exampleWidgetResource{}
}

func (e *exampleWidgetResource) Schema(ctx context.Context, req resource.SchemaRequest, resp *resource.SchemaResponse) {
	resp.Schema = schema.Schema{
		// ... other configuration ...

		Attributes: map[string]schema.Attribute{
			// ... other attributes ...
		},
		DeprecationMessage: "use example_thing resource instead",
	}
}

func (e *exampleWidgetResource) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

func (e *exampleWidgetResource) Read(ctx context.Context, req resource.ReadRequest, resp *resource.ReadResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

func (e *exampleWidgetResource) Update(ctx context.Context, req resource.UpdateRequest, resp *resource.UpdateResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

func (e *exampleWidgetResource) Delete(ctx context.Context, req resource.DeleteRequest, resp *resource.DeleteResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

```

--------------------------------

### Install Terraform on macOS using Homebrew

Source: https://developer.hashicorp.com/terraform/install

Installs Terraform on macOS using the Homebrew package manager. This is a convenient way to manage Terraform installations and updates.

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

--------------------------------

### Implement resource.Resource Interface in Framework

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/resources

An example resource in the Terraform Plugin Framework implements the `resource.Resource` interface, requiring `Metadata`, `Schema`, `Create`, `Read`, `Update`, and `Delete` methods. The `Metadata` method defines the resource type name, and the `Schema` method defines its attributes.

```go
type resourceExample struct{}

func (r *resourceExample) Metadata(ctx context.Context, req resource.MetadataRequest, resp *resource.MetadataResponse) {
    /* ... */
}

func (r *resourceExample) Schema(ctx context.Context, req resource.SchemaRequest, resp *resource.SchemaResponse) {
    /* ... */
}

func (r *resourceExample) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
    /* ... */
}

func (r *resourceExample) Read(ctx context.Context, req resource.ReadRequest, resp *resource.ReadResponse) {
    /* ... */
}

```

--------------------------------

### Minimal Terraform Module Structure Example

Source: https://developer.hashicorp.com/terraform/language/v1.7.x/modules/develop/structure

This example demonstrates the minimal recommended file and directory structure for a Terraform module. It includes the essential files: README.md for documentation, main.tf as the entrypoint, variables.tf for input declarations, and outputs.tf for output declarations. This structure is a best practice for organizing reusable Terraform code.

```tree
$
 tree minimal-module/
 .
 ├── README.md
 ├── main.tf
 ├── variables.tf
 └── outputs.tf

```

```tree
$
 tree minimal-module/
 .
 ├── README.md
 ├── main.tf
 ├── variables.tf
 └── outputs.tf

```

--------------------------------

### API Request to Show a Policy Set

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-3/api-docs/policy-sets

This example shows the HTTP GET request format to retrieve a specific policy set using its ID. The `:id` placeholder should be replaced with the actual ID of the policy set you wish to fetch. The `include` query parameter can be used to fetch related resources.

```http
GET /api/v2/policy-sets/:id?include=workspaces,policies
```

--------------------------------

### Terraform Initialization and Import Refresh

Source: https://developer.hashicorp.com/terraform/cdktf/v0.19.x/concepts/resources

This output shows the process of initializing Terraform, including backend and provider setup, and refreshing the state of resources to be imported. It confirms successful initialization and prepares for the import of an AWS S3 bucket.

```bash
ts-import-with-configuration  Initializing the backend...
ts-import-with-configuration  Initializing provider plugins...
                              - Reusing previous version of hashicorp/aws from the dependency lock file
ts-import-with-configuration  - Using previously-installed hashicorp/aws v5.18.1
 
                              Terraform has been successfully initialized!
ts-import-with-configuration
                              You may now begin working with Terraform. Try running "terraform plan" to see
                              any changes that are required for your infrastructure. All Terraform commands
                              should now work.
 
                              If you ever set or change modules or backend configuration for Terraform,
                              rerun this command to reinitialize your working directory. If you forget, other
                              commands will detect it and remind you to do so if necessary.
ts-import-with-configuration  aws_s3_bucket.bucket: Preparing import... [id=best-bucket-in-the-world]
ts-import-with-configuration  aws_s3_bucket.bucket: Refreshing state... [id=best-bucket-in-the-world]
ts-import-with-configuration  Terraform will perform the following actions:
ts-import-with-configuration    # aws_s3_bucket.bucket will be imported
                                # (config will be generated)
                                  resource "aws_s3_bucket" "bucket" {
                                      arn                         = "arn:aws:s3:::best-bucket-in-the-world"
                                      bucket                      = "best-bucket-in-the-world"

```

--------------------------------

### Terraform substr Function Syntax and Examples

Source: https://developer.hashicorp.com/terraform/language/v1.15.x/functions/substr

The `substr` function in Terraform extracts a portion of a string. It takes the string, a starting offset, and a maximum length as arguments. The function supports Unicode characters and allows for negative offsets relative to the end of the string, as well as a length of -1 to return the remainder of the string.

```terraform
substr(string, offset, length)
```

```terraform
> substr("hello world", 1, 4)
ell
```

```terraform
> substr("🤔🤷", 0, 1)
🤔
```

```terraform
> substr("hello world", -5, -1)
world
```

```terraform
> substr("hello world", 6, 10)
world
```

--------------------------------

### Minimal Terraform Module Structure Example

Source: https://developer.hashicorp.com/terraform/language/v1.6.x/modules/develop/structure

This example demonstrates the minimal recommended file structure for a Terraform module. It includes the essential files for a basic, reusable module.

```shell
$ tree minimal-module/
.
├── README.md
├── main.tf
├── variables.tf
└── outputs.tf

```

```shell
$ tree minimal-module/
.
├── README.md
├── main.tf
├── variables.tf
└── outputs.tf

```

--------------------------------

### Install DNF Plugins Core for DNF Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Installs the `dnf-plugins-core` package, which provides the `dnf config-manager` command. This command is necessary for managing repositories and configurations with DNF on Fedora and similar systems.

```bash
sudo dnf install -y dnf-plugins-core
```

--------------------------------

### Start Terraform Agent with Environment Variables (Docker)

Source: https://developer.hashicorp.com/terraform/cloud-docs/agents/v1.10.x/agents

This snippet demonstrates how to run the Terraform Cloud agent using a Docker container. It involves pulling the latest agent image and then running a container, passing the agent token and name as environment variables. This method isolates the agent process within a container.

```bash
docker pull hashicorp/tfc-agent:latest
docker run -e TFC_AGENT_TOKEN=your-token -e TFC_AGENT_NAME=your-agent-name hashicorp/tfc-agent
```

--------------------------------

### Apply Terraform Configuration with Azure Resource Group

Source: https://developer.hashicorp.com/terraform/tutorials/azure-get-started/azure-build

Demonstrates the `terraform apply` command to create an Azure resource group. It shows the execution plan, prompts for user approval, and confirms the creation. The output includes resource creation details and a summary of changes.

```bash
$ terraform apply
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.rg will be created
  + resource "azurerm_resource_group" "rg" {
      + id       = (known after apply)
      + location = "westus2"
      + name     = "myTFResourceGroup"
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes
azurerm_resource_group.rg: Creating...
azurerm_resource_group.rg: Creation complete after 1s [id=/subscriptions/c9ed8610-47a3-4107-a2b2-a322114dfb29/resourceGroups/myTFResourceGroup]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/cli/outputs

Clones the example Terraform repository containing configurations for a web application. This repository includes definitions for VPC, load balancer, EC2 instances, and a database.

```bash
$ git clone https://github.com/hashicorp-education/learn-terraform-outputs

```

--------------------------------

### Install Terraform on Fedora using dnf

Source: https://developer.hashicorp.com/terraform/install

Installs Terraform on Fedora Linux using the dnf package manager. It adds the HashiCorp repository and installs the terraform package.

```bash
sudo dnf install -y dnf-plugins-core
sudo dnf config-manager addrepo --from-repofile=https://rpm.releases.hashicorp.com/fedora/hashicorp.repo
sudo dnf -y install terraform
```

--------------------------------

### Provision Start Hook

Source: https://developer.hashicorp.com/terraform/internals/machine-readable-ui

The `provision_start` hook signals the beginning of a provisioning step for a resource.

```APIDOC
## Provision Start

### Description
The `provision_start` message `hook` object indicates the initiation of a provisioning process for a resource.

### Method
N/A (This is a message hook, not an API endpoint)

### Endpoint
N/A

### Parameters
#### Hook Object
- **resource** (object) - Identifies the resource for which provisioning is starting.
  - **addr** (string) - The address of the resource.
  - **module** (string) - The module the resource belongs to.
  - **resource** (string) - The full resource identifier.
  - **implied_provider** (string) - The implied provider for the resource.
  - **resource_type** (string) - The type of the resource.
  - **resource_name** (string) - The name of the resource.
  - **resource_key** (integer or null) - The key of the resource if it's part of a list or map.
- **provisioner** (string) - The type of provisioner being used.

### Request Example
(No specific example provided in the source text for `provision_start` hook)

### Response
N/A (This is a message hook)

#### Success Response (N/A)

#### Response Example
N/A
```

--------------------------------

### Terraform Example Widget Resource Schema and Operations (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.13.x/deprecations

Defines the schema and implements the Create, Read, Update, and Delete operations for the deprecated example_widget resource. All operations append a deprecation diagnostic message instructing users to switch to the example_thing resource.

```go
package main

import (
	"context"

	"github.com/hashicorp/terraform-plugin-framework/diag"
	"github.com/hashicorp/terraform-plugin-framework/resource"
	"github.com/hashicorp/terraform-plugin-framework/resource/schema"
)

type exampleWidgetResource struct {}

func NewWidgetResource() resource.Resource {
	return &exampleWidgetResource{}
}

func (e *exampleWidgetResource) Schema(ctx context.Context, req resource.SchemaRequest, resp *resource.SchemaResponse) {
	resp.Schema = schema.Schema{
		// ... other configuration ...

		Attributes: map[string]schema.Attribute{
			// ... other attributes ...
		},
		DeprecationMessage: "use example_thing resource instead",
	}
}

func (e *exampleWidgetResource) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

func (e *exampleWidgetResource) Read(ctx context.Context, req resource.ReadRequest, resp *resource.ReadResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

func (e *exampleWidgetResource) Update(ctx context.Context, req resource.UpdateRequest, resp *resource.UpdateResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

func (e *exampleWidgetResource) Delete(ctx context.Context, req resource.DeleteRequest, resp *resource.DeleteResponse) {
	resp.Diagnostics.Append(
		diag.NewErrorDiagnostic("example_widget resource deprecated", "use example_thing resource instead"),
	)
}

```

--------------------------------

### Install Terraform on Amazon Linux using yum

Source: https://developer.hashicorp.com/terraform/install

Installs Terraform on Amazon Linux using the yum package manager. It adds the HashiCorp repository and installs the terraform package.

```bash
sudo yum install -y yum-utils shadow-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum install terraform
```

--------------------------------

### Get AI Resources from Google Provider using Terraform MCP

Source: https://developer.hashicorp.com/terraform/mcp-server/prompt

This snippet demonstrates how to prompt the Terraform MCP server to retrieve a list of AI-related resources available in the Google provider. It requires the Terraform MCP server to be deployed and configured. The prompt specifies the provider and a service slug ('ai') to filter the results.

```plaintext
I need help understanding what resources are available 
in the Google provider that are for AI
```

--------------------------------

### Example Output of Terraform Workspace Show (CLI)

Source: https://developer.hashicorp.com/terraform/cli/v1.15.x/commands/workspace/show

This example demonstrates the typical output when running the 'terraform workspace show' command. The output is the name of the active workspace, such as 'development'.

```bash
$ terraform workspace show
development
```

--------------------------------

### Terraform Provider File Path Structure

Source: https://developer.hashicorp.com/terraform/enterprise/v202302-1/run/install-software

This example illustrates the expected directory structure for manually placing compiled Terraform provider binaries. The path includes the source host, namespace, plugin name, version, and operating system architecture, allowing Terraform to discover and use the custom provider.

```plaintext
terraform.d/plugins/<SOURCE HOST>/<SOURCE NAMESPACE>/<PLUGIN NAME>/<VERSION>/linux_amd64
```

--------------------------------

### Retrieve State Version with Included Outputs

Source: https://developer.hashicorp.com/terraform/enterprise/v202311-1/api-docs/state-versions

This example shows how to retrieve a state version and include its parsed outputs directly in the response using the 'include' query parameter. This can be more efficient than making a separate API call for outputs.

```bash
curl \
  --header "Authorization: Bearer $TF_API_TOKEN" \
  "https://app.terraform.io/api/v2/state-versions/sv-g4rqST72reoHMM5a?include=outputs"
```

--------------------------------

### List Variables in Terraform Cloud Variable Set (curl)

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-2/api-docs/variable-sets

This example shows how to list all variables associated with a specific Terraform Cloud variable set using a curl command. It uses the GET HTTP method and requires the variable set ID. The endpoint targets the relationships/vars endpoint for the specified variable set.

```curl
GET varsets/:varset_id/relationships/vars
```

--------------------------------

### Provision Start Event

Source: https://developer.hashicorp.com/terraform/internals/v1.9.x/machine-readable-ui

This event is triggered when a resource provisioning process begins. It includes details about the resource and the provisioner being used.

```APIDOC
## Provision Start Event

### Description
This event signifies the commencement of a resource provisioning operation. It provides information about the specific resource being provisioned and the method (provisioner) employed.

### Method
POST (or relevant event ingestion method)

### Endpoint
/events/provision/start

### Parameters
#### Request Body
- **@level** (string) - Log level (e.g., "info").
- **@message** (string) - A human-readable message describing the event.
- **@module** (string) - The module generating the log (e.g., "terraform.ui").
- **@timestamp** (string) - The time the event occurred in ISO 8601 format.
- **hook** (object) - An object containing details about the provisioning hook.
  - **resource** (object) - An object identifying the resource being provisioned.
    - **addr** (string) - The address of the resource.
    - **module** (string) - The module path of the resource.
    - **resource** (string) - The full resource identifier.
    - **implied_provider** (string) - The implied provider for the resource.
    - **resource_type** (string) - The type of the resource.
    - **resource_name** (string) - The name of the resource.
    - **resource_key** (integer) - The key of the resource if it's part of a list or map.
  - **provisioner** (string) - The type of provisioner being used (e.g., "local-exec").
- **type** (string) - The event type, which is "provision_start" for this event.

### Request Example
```json
{
  "@level": "info",
  "@message": "null_resource.none[0]: Provisioning with 'local-exec'வுகளை...",
  "@module": "terraform.ui",
  "@timestamp": "2021-03-26T16:38:43.997431-04:00",
  "hook": {
    "resource": {
      "addr": "null_resource.none[0]",
      "module": "",
      "resource": "null_resource.none[0]",
      "implied_provider": "null",
      "resource_type": "null_resource",
      "resource_name": "none",
      "resource_key": 0
    },
    "provisioner": "local-exec"
  },
  "type": "provision_start"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates the success of the event ingestion.

#### Response Example
```json
{
  "status": "success"
}
```
```

--------------------------------

### Get AI Resources from Google Provider (Text Response)

Source: https://developer.hashicorp.com/terraform/docs/tools/mcp-server/prompt

This snippet shows a text response from the Terraform MCP server detailing AI-related resources available in the Google provider, primarily under Vertex AI and Document AI services. It lists specific resource types for managing AI/ML workflows on Google Cloud.

```text
The Google Terraform provider offers several resources related to AI, primarily under the Vertex AI and Document AI services. Here are the main AI-related resources available:

**Vertex AI Resources**

- `vertex_ai_dataset`
- `vertex_ai_deployment_resource_pool`
- `vertex_ai_endpoint`
- `vertex_ai_endpoint_iam`
- `vertex_ai_feature_group`
- `vertex_ai_featurestore`
- `vertex_ai_index`
- `vertex_ai_metadata_store`
- `vertex_ai_tensorboard`
- `document_ai_processor`
- `document_ai_warehouse_document_schema`
 
These resources allow you to manage datasets, endpoints, feature stores, indexes, metadata, and more for AI/ML workflows on Google Cloud, as well as Document AI processors and schemas.
```

--------------------------------

### Build Path Expression with List Index

Source: https://developer.hashicorp.com/terraform/plugin/framework/path-expressions

Demonstrates the builder pattern for path expressions by chaining methods. This example points to any element within a list attribute.

```go
path.MatchRoot("example_list_attribute").AtAnyListIndex()

```

--------------------------------

### Terraform Remote-Exec Provisioner Script Path Example

Source: https://developer.hashicorp.com/terraform/language/v1.1.x/upgrade-guides/1-1

This snippet illustrates how the `remote-exec` provisioner can be configured to upload and execute scripts. The `script_path` argument within the `connection` block specifies the remote location for the script. Similar to the `file` provisioner, Terraform v1.1 onwards handles these paths verbatim, without shell expansion.

```terraform
provisioner "remote-exec" {
  inline = [
    "echo 'Hello, World!' > remote.txt"
  ]

  connection {
    type        = "ssh"
    user        = "user"
    private_key = file("~/.ssh/id_rsa")
    script_path = "/tmp/script.sh"
  }
}

```

--------------------------------

### Initialize Terraform Project

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-deploy

Initializes the Terraform working directory, downloading necessary provider plugins and setting up the backend. This command must be run before any other Terraform commands to prepare the environment for infrastructure management.

```bash
$ terraform init
Initializing the backend...
Initializing provider plugins...
- Reusing previous version of hashicorp/azuread from the dependency lock file
- Reusing previous version of hashicorp/azurerm from the dependency lock file
- Installing hashicorp/azuread v3.4.0...
- Installed hashicorp/azuread v3.4.0 (signed by HashiCorp)
- Installing hashicorp/azurerm v4.34.0...
- Installed hashicorp/azurerm v4.34.0 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Sentinel Configuration for 'sentinel apply'

Source: https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement/sentinel/mock

Example Sentinel configuration file ('sentinel.hcl') demonstrating how to reference mock data for 'sentinel apply'. Paths to mock data are relative to the working directory, typically the repository root.

```hcl
mock "tfconfig" {
  module {
    source = "testdata/mock-tfconfig.sentinel"
  }
}

mock "tfconfig/v1" {
  module {
    source = "testdata/mock-tfconfig.sentinel"
  }
}

mock "tfconfig/v2" {
  module {
    source = "testdata/mock-tfconfig-v2.sentinel"
  }
}

mock "tfplan" {
  module {
    source = "testdata/mock-tfplan.sentinel"
  }
}

mock "tfplan/v1" {
  module {
    source = "testdata/mock-tfplan.sentinel"
  }
}

mock "tfplan/v2" {
  module {
    source = "testdata/mock-tfplan-v2.sentinel"
  }
}

mock "tfstate" {
  module {
    source = "testdata/mock-tfstate.sentinel"
  }
}

mock "tfstate/v1" {
  module {
    source = "testdata/mock-tfstate.sentinel"
  }
}

mock "tfstate/v2" {
  module {
    source = "testdata/mock-tfstate-v2.sentinel"
  }
}

mock "tfrun" {
  module {
    source = "testdata/mock-tfrun.sentinel"
  }
}
```

--------------------------------

### Install Terraform using DNF

Source: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Installs Terraform from the newly added HashiCorp Fedora repository using the `dnf` package manager. This command ensures Terraform is installed with the `-y` flag for non-interactive installation.

```bash
sudo dnf -y install terraform
```

--------------------------------

### Install Terraform on Ubuntu/Debian using apt

Source: https://developer.hashicorp.com/terraform/install

Installs Terraform on Ubuntu and Debian-based Linux distributions using the apt package manager. It adds the HashiCorp repository and installs the terraform package.

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

--------------------------------

### Generate Provider Documentation (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-function-only

This shell command initiates the documentation generation process for a Terraform provider using `go generate ./...`. It compiles the provider, initializes Terraform, retrieves the schema, and generates markdown documentation for resources, data sources, and functions.

```shell
$ go generate ./...
rendering website for provider "exampletime" (as "exampletime")
exporting schema from Terraform
compiling provider "exampletime"
using Terraform CLI binary from PATH if available, otherwise downloading latest Terraform CLI binary
running terraform init
getting provider schema
generating missing templates
generating missing resource content
generating missing data source content
generating missing function content
generating new template for function "rfc3339_parse"
generating missing provider content
generating new template for "exampletime"
rendering static website
cleaning rendered website dir
removing directory: "data-sources"
removing directory: "functions"
removing file: "index.md"
removing directory: "resources"
rendering templated website to static markdown
rendering "functions/rfc3339_parse.md.tmpl"
rendering "index.md.tmpl"

```

--------------------------------

### Install Terraform on CentOS/RHEL using yum

Source: https://developer.hashicorp.com/terraform/install

Installs Terraform on CentOS, RHEL, and similar Linux distributions using the yum package manager. It configures the HashiCorp repository and installs the terraform package.

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install terraform
```

--------------------------------

### Initialize Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/aws/aws-asg

Initializes the Terraform working directory. This command downloads provider plugins and sets up the backend configuration. It's essential to run this before other Terraform commands.

```bash
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Installing hashicorp/aws v3.50.0...
- Installed hashicorp/aws v3.50.0 (signed by HashiCorp)

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

--------------------------------

### Accessing Attribute Values in Terraform SDKv2

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.15.x/migrating/benefits

Demonstrates how Terraform SDKv2 handles attribute value states (null, unknown, known) using Get(), GetOk(), and GetOkExists() methods. It shows that SDKv2 often returns Go type zero-values for null states and that GetOk() and GetOkExists() behavior can vary. This example assumes a schema with a computed and optional string attribute.

```go
// Assuming a schema of:
//
//   "string_attribute": &schema.Schema{
//     Computed: true,
//     Optional: true,
//     Type:     schema.TypeString,
//   }
//
// and a configuration that does not set the value (null state).
//
// resource “examplecloud_thing” “example” {
//     # no string_attribute = “...”
// }

func ThingResourceUpdate(ctx context.Context, d *schema.ResourceData, meta any) diag.Diagnostics {
  d.Get("string_attribute") // ""
  d.GetOk("string_attribute") // may return true depending on prior state
  d.GetOkExists("string_attribute") // may return true depending on prior state
}

```

--------------------------------

### Terraform Configuration Parameters

Source: https://developer.hashicorp.com/terraform/enterprise/replicated/administration/license/automated-license-utilization-reporting

This snippet shows example Terraform configuration parameters for an installation. It includes settings for RUM (Real User Monitoring), VCS (Version Control System) presence, and various counts of resources like organizations, projects, and modules. These are typically defined within a Terraform configuration file.

```hcl
{
    "billable_rum_count_workspace_max": {
        "key": "billable_rum_count_workspace_max",
        "value": 0,
        "mode": "write"
    },
    "billable_rum_count_workspace_median": {
        "key": "billable_rum_count_workspace_median",
        "value": 0,
        "mode": "write"
    },
    "billable_rum_count_workspace_min": {
        "key": "billable_rum_count_workspace_min",
        "value": 0,
        "mode": "write"
    },
    "billable_rum_opt_in": {
        "key": "billable_rum_opt_in",
        "value": 1,
        "mode": "write"
    },
    "bitbucket_vcs_present": {
        "key": "bitbucket_vcs_present",
        "value": 0,
        "mode": "write"
    },
    "continuous_validation_used_last_90_days": {
        "key": "continuous_validation_used_last_90_days",
        "value": 0,
        "mode": "write"
    },
    "daily_api_runs": {
        "key": "daily_api_runs",
        "value": 0,
        "mode": "write"
    },
    "daily_cli_runs": {
        "key": "daily_cli_runs",
        "value": 0,
        "mode": "write"
    },
    "daily_runs": {
        "key": "daily_runs",
        "value": 0,
        "mode": "write"
    },
    "daily_vcs_runs": {
        "key": "daily_vcs_runs",
        "value": 0,
        "mode": "write"
    },
    "deployment_option": {
        "key": "deployment_option",
        "value": 0,
        "mode": "write"
    },
    "drift_detection_used_last_90_days": {
        "key": "drift_detection_used_last_90_days",
        "value": 0,
        "mode": "write"
    },
    "gcp_provider_present": {
        "key": "gcp_provider_present",
        "value": 0,
        "mode": "write"
    },
    "github_vcs_present": {
        "key": "github_vcs_present",
        "value": 0,
        "mode": "write"
    },
    "gitlab_vcs_present": {
        "key": "gitlab_vcs_present",
        "value": 0,
        "mode": "write"
    },
    "installation_reporting_environment_type": {
        "key": "installation_reporting_environment_type",
        "value": 0,
        "mode": "write"
    },
    "operational_mode": {
        "key": "operational_mode",
        "value": 0,
        "mode": "write"
    },
    "org_admin_count": {
        "key": "org_admin_count",
        "value": 1,
        "mode": "write"
    },
    "org_count": {
        "key": "org_count",
        "value": 1,
        "mode": "write"
    },
    "private_modules_count": {
        "key": "private_modules_count",
        "value": 0,
        "mode": "write"
    },
    "product_usage_reporting_opt_in": {
        "key": "product_usage_reporting_opt_in",
        "value": 1,
        "mode": "write"
    },
    "project_count": {
        "key": "project_count",
        "value": 1,
        "mode": "write"
    },
    "run_concurrency": {
        "key": "run_concurrency",
        "value": 0,
        "mode": "write"
    }
}
```

--------------------------------

### Terraform Configuration Example: Unknown Values

Source: https://developer.hashicorp.com/terraform/plugin/framework/handling-data/terraform-concepts

This example demonstrates how Terraform handles unknown values. The `example_baz.quux` resource depends on the `id` attribute of `example_foo.bar`, which is not known until after the apply. During the plan phase, `foo_id` in `example_baz.quux` will be an unknown value.

```terraform
resource "example_foo" "bar" {
  hello = "world"
  demo = true
}

resource "example_baz" "quux" {
  foo_id = example_foo.bar.id
}
```

--------------------------------

### Terraform Enterprise External Deployment with Docker Compose

Source: https://developer.hashicorp.com/terraform/enterprise/v202309-1/flexible-deployments/install/docker/install

This Docker Compose configuration deploys Terraform Enterprise in external services mode. It requires pre-configured external PostgreSQL and S3-compatible object storage. Key environment variables for license, hostname, encryption, database connection, and object storage credentials must be provided.

```yaml
---
name: terraform-enterprise
services:
  tfe:
    image: images.releases.hashicorp.com/hashicorp/terraform-enterprise:<vYYYYMM-#>
    environment:
      TFE_LICENSE: "<Hashicorp license>"
      TFE_HOSTNAME: "<TFE hostname (DNS) e.g. terraform.example.com>"
      TFE_ENCRYPTION_PASSWORD: "<Encryption password>"
      TFE_OPERATIONAL_MODE: "external"
      TFE_DISK_CACHE_VOLUME_NAME: "${COMPOSE_PROJECT_NAME}_terraform-enterprise-cache"
      TFE_TLS_CERT_FILE: "/etc/ssl/private/terraform-enterprise/cert.pem"
      TFE_TLS_KEY_FILE: "/etc/ssl/private/terraform-enterprise/key.pem"
      TFE_TLS_CA_BUNDLE_FILE: "/etc/ssl/private/terraform-enterprise/bundle.pem"
      TFE_IACT_SUBNETS: "<IACT subnet, eg. 10.0.0.0/8,192.168.0.0/24>"

      # Database settings. See the configuration reference for more settings.
      TFE_DATABASE_USER: "<Database user e.g. postgres>"
      TFE_DATABASE_PASSWORD: "<Database password e.g. postgres>"
      TFE_DATABASE_HOST: "<Database hostname and port e.g. postgres:5432>"
      TFE_DATABASE_NAME: "<Database name e.g. hashicorp>"
      TFE_DATABASE_PARAMETERS: "<Database parameters e.g. sslmode=disable>"

      # Object storage settings. See the configuration reference for more settings.
      TFE_OBJECT_STORAGE_TYPE: "s3"
      TFE_OBJECT_STORAGE_S3_ACCESS_KEY_ID: "<AWS Access Key ID>"
      TFE_OBJECT_STORAGE_S3_SECRET_ACCESS_KEY: "<AWS Secret Access Key>"
      TFE_OBJECT_STORAGE_S3_REGION: "<AWS Region e.g.us-east-1>"
      TFE_OBJECT_STORAGE_S3_BUCKET: "<Bucket name>"
    cap_add:
      - IPC_LOCK
    read_only: true
    tmpfs:
      - "/tmp:mode=01777"
      - "/run"
      - "/var/log/terraform-enterprise"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - type: bind
        source: /var/run/docker.sock
        target: /run/docker.sock
      - type: bind
        source: ./certs
        target: /etc/ssl/private/terraform-enterprise
      - type: volume
        source: terraform-enterprise-cache
        target: /var/cache/tfe-task-worker/terraform
volumes:
  terraform-enterprise-cache:

```

--------------------------------

### Create Workspace (VCS with Git Tags Regex)

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/api-docs/workspaces

This example shows creating a workspace with a VCS repository and a regular expression for Git tags.

```APIDOC
## POST /api/v2/workspaces

### Description
Creates a new HCP Terraform workspace linked to a VCS repository, triggering runs based on Git tags matching a specified regular expression.

### Method
POST

### Endpoint
/api/v2/workspaces

### Parameters
#### Request Body
- **data** (object) - Required - The workspace object.
  - **attributes** (object) - Required - Workspace attributes.
    - **name** (string) - Required - The name of the workspace.
    - **terraform_version** (string) - Optional - The Terraform version to use.
    - **file-triggers-enabled** (boolean) - Optional - Whether file triggers are enabled.
    - **working-directory** (string) - Optional - The working directory within the VCS repository.
    - **vcs-repo** (object) - Required - VCS repository configuration.
      - **identifier** (string) - Required - The VCS repository identifier (e.g., "owner/repo").
      - **oauth-token-id** (string) - Required - The ID of the OAuth token for VCS authentication.
      - **branch** (string) - Optional - The specific branch to use. If empty, the default branch is used.
      - **tags-regex** (string) - Required - A regular expression to filter Git tags for triggering runs (e.g., `\d+\.\d+\.\d+` for SemVer).
  - **type** (string) - Required - Must be "workspaces".

### Request Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-3",
      "terraform_version": "0.12.1",
      "file-triggers-enabled": false,
      "working-directory": "/networking",
      "vcs-repo": {
        "identifier": "example/terraform-test-proj-monorepo",
        "oauth-token-id": "ot-hmAyP66qk2AMVdbJ",
        "branch": "",
        "tags-regex": "\\d+\\.\\d+\\.\\d+" 
      }
    },
    "type": "workspaces"
  }
}
```

### Response
#### Success Response (201 Created)
- **data** (object) - The created workspace object.
  - **attributes** (object) - Workspace attributes.
    - **name** (string) - The name of the workspace.
    - **terraform_version** (string) - The Terraform version used.
    - **file-triggers-enabled** (boolean) - Status of file triggers.
    - **working-directory** (string) - The working directory.
    - **vcs-repo** (object) - VCS repository configuration.
      - **identifier** (string) - The VCS repository identifier.
      - **oauth-token-id** (string) - The ID of the OAuth token.
      - **branch** (string) - The branch used.
      - **tags-regex** (string) - The regex for filtering Git tags.
  - **type** (string) - The type of the resource, "workspaces".

#### Response Example
```json
{
  "data": {
    "attributes": {
      "name": "workspace-3",
      "terraform_version": "0.12.1",
      "file-triggers-enabled": false,
      "working-directory": "/networking",
      "vcs-repo": {
        "identifier": "example/terraform-test-proj-monorepo",
        "oauth-token-id": "ot-hmAyP66qk2AMVdbJ",
        "branch": "",
        "tags-regex": "\\d+\\.\\d+\\.\\d+" 
      }
    },
    "type": "workspaces"
  }
}
```
```

--------------------------------

### Provision Start Message

Source: https://developer.hashicorp.com/terraform/internals/v1.2.x/machine-readable-ui

Details the structure of the 'provision_start' message, indicating the beginning of a provisioner execution.

```APIDOC
## Provision Start

The `provision_start` message indicates that a provisioner is about to start executing for a resource.

### Hook Object Keys

*   `resource`: A `resource` object identifying the resource for which provisioning is starting.
*   `provisioner`: The type of provisioner being used (e.g., 'local-exec', 'remote-exec').

### Example

```json
{
  "@level": "info",
  "@message": "null_resource.none[0]: Provisioning with 'local-exec'...",
  "@module": "terraform.ui",
  "@timestamp": "2021-03-26T16:38:43.997431-04:00",
  "hook": {
    "resource": {
      "addr": "null_resource.none[0]",
      "module": "",
      "resource": "null_resource.none[0]",
      "implied_provider": "null",
      "resource_type": "null_resource",
      "resource_name": "none",
      "resource_key": 0
    },
    "provisioner": "local-exec"
  },
  "type": "provision_start"
}
```
```

--------------------------------

### Validate S3 Bucket Prefix in Java (CDKTF)

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/aspects

This Java code defines a CDKTF Aspect for validating S3 bucket names. It implements the `IAspect` interface and the `visit` method checks if an `S3Bucket` construct starts with the specified prefix. If not, an error is reported using `Annotations.of(node).addError`. The example also shows how to instantiate and apply this Aspect within a `TerraformStack`.

```java
    public class ValidateS3IsPrefixed implements IAspect {

        private final String prefix;

        public ValidateS3IsPrefixed(String prefix) {
            this.prefix = prefix;
        }

        // This method is called on every Construct within the defined scope (resource,
        // data sources, etc.).
        public void visit(IConstruct node) {
            if (node instanceof S3Bucket) {
                if (((S3Bucket) node).getBucketInput() != null && !((S3Bucket) node).getBucketInput().startsWith(this.prefix)) {
                    // You can include `addInfo`, `addWarning`, and `addError`.
                    // CDKTF prints these messages when the user runs `synth`, `plan`, or `deploy`.
                    Annotations.of(node).addError(
                            "Each S3 Bucket name needs to start with " + this.prefix);
                }
            }
        }
    }

        // Check the prefix for every resource within `myStack`.
        Aspects.of(bucket).add(new ValidateS3IsPrefixed("myPrefix"));
```

--------------------------------

### Terraform Framework Data Access Examples

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.3.x/migrating/benefits

Demonstrates how the Terraform Framework exposes configuration, plan, and state data as separate attributes on request and response types for different operations (Create, Read, Update, Delete). This approach clarifies data availability for each operation.

```go
func (r ThingResource) Create(ctx context.Context, req resource.CreateRequest, resp *resource.CreateResponse) {
  req.Config // configuration data
  req.Plan // plan data
  // No req.State as it is always null
  // No resp.Config as configuration cannot be set by provider during creation
  // No resp.Plan as plan cannot be set by provider during creation
  resp.State // new state data to save
}

func (r ThingResource) Read(ctx context.Context, req resource.ReadRequest, resp *resource.CreateResponse) {
  // No req.Config as configuration cannot be read by provider during read
  // No req.Plan as there is no plan during read
  req.State // prior state data
  // No resp.Config as configuration cannot be set by provider during read
  // No resp.Plan as there is no plan during read
  resp.State // new state data to save
}

func (r ThingResource) Update(ctx context.Context, req resource.UpdateRequest, resp *resource.UpdateResponse) {
  req.Config // configuration data
  req.Plan // plan data
  req.State // prior state data
  // No resp.Config as configuration cannot be set by provider during update
  // No resp.Plan as plan cannot be set by provider during update
  resp.State // new state data to save
}

func (r ThingResource) Delete(ctx context.Context, req resource.DeleteRequest, resp *resource.DeleteResponse) {
  // No req.Config as configuration cannot be read by provider during delete
  // No req.Plan as it is always null
  req.State // prior state data
  // No resp.Config as configuration cannot be set by provider during delete
  // No resp.Plan as it is always null
  // No resp.State as resource destroy leaves no state
}

```

--------------------------------

### Terraform file Function Example

Source: https://developer.hashicorp.com/terraform/language/v1.10.x/functions/file

An example demonstrating how to use the `file` function to read the content of 'hello.txt' located within the current module's path. The output will be the content of the file.

```Terraform
> file("${path.module}/hello.txt")
Hello World
```

```Terraform
> file("${path.module}/hello.txt")
Hello World

```

--------------------------------

### GitHub App Installation APIs

Source: https://developer.hashicorp.com/terraform/enterprise/v202304-1/api-docs/changelog

APIs for managing GitHub App installations, used for connecting Terraform resources to GitHub App installations.

```APIDOC
## GitHub App Installation APIs

### Description
These APIs facilitate the management of GitHub App installations, enabling connections between Terraform resources and GitHub App installations.

### Method
GET, POST, PUT, DELETE

### Endpoint
/api/v2/github-app-installations

### Parameters
(Specific parameters depend on the exact operation: list, create, update, delete installation)

### Request Example (Conceptual - Creating a workspace with GitHub App Installation)
```json
{
  "name": "my-workspace",
  "vcs_repo": {
    "identifier": "my-org/my-repo",
    "use_ssh": false,
    "github_app_installation_id": "app-install-123"
  }
}
```

### Response
#### Success Response (200 or 201)
- Details of the GitHub App Installation or the resource referencing it.

#### Response Example (Conceptual)
```json
{
  "id": "ws-45678",
  "name": "my-workspace",
  "vcs_repo": {
    "identifier": "my-org/my-repo",
    "github_app_installation_id": "app-install-123"
  }
}
```
```

--------------------------------

### Deploy Kubernetes Web App (C#)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.16.x/concepts/constructs

Deploys a web application to Kubernetes using the `KubernetesWebAppDeployment` construct in C#. It configures the image, replicas, app name, component, and environment. This requires the `cdktf-cli` and relevant providers.

```csharp
new KubernetesProvider(this, "kind", new KubernetesProviderConfig
{
    ConfigPath = Path.Join(Environment.CurrentDirectory, "../kubeconfig.yaml")
});
new KubernetesWebAppDeployment(this, "deployment", new Dictionary<string, object> {
    { "image", "nginx:latest" },
    { "replicas", 2 },
    { "app", "myapp" },
    { "component", "frontend" },
    { "environment", "dev" }
});
        }
    }
}
```

--------------------------------

### Build AWS VPC Module using String Format in cdktf.json

Source: https://developer.hashicorp.com/terraform/cdktf/create-and-deploy/configuration-file

This example shows how to declare the AWS VPC module from the Terraform Registry using the string format within cdktf.json. The 'terraformModules' property lists the module source and version constraint ('terraform-aws-modules/vpc/aws'). Executing 'cdktf get' will download and generate code for this module.

```json
{
  "language": "typescript",
  "app": "npm run --silent compile && node main.js",
  "terraformModules": ["terraform-aws-modules/vpc/aws"]
}
```

--------------------------------

### Terraform StringFunc Check Example

Source: https://developer.hashicorp.com/terraform/plugin/testing/acceptance-tests/known-value-checks/string

This Go code snippet demonstrates how to use the StringFunc check within a Terraform resource's state check. It defines a custom validation function to ensure a string attribute starts with 'str'. This requires the 'hashicorp/terraform' testing package and its associated statecheck and knownvalue modules.

```go
func TestExpectKnownValue_CheckState_StringFunc(t *testing.T) {
    t.Parallel()

    resource.Test(t, resource.TestCase{
        // Provider definition omitted.
        Steps: []resource.TestStep{
            {
                // Example resource containing a string attribute named "configurable_attribute"
                Config: `resource "test_resource" "one" {}`,
                ConfigStateChecks: []statecheck.StateCheck{
                    statecheck.ExpectKnownValue(
                        "test_resource.one",
                        tfjsonpath.New("configurable_attribute"),
                        knownvalue.StringFunc(func(v string) error {
                            if !strings.HasPrefix(v, "str") {
                                return fmt.Errorf("value must start with 'str'")
                            }
                            return nil
                        }),
                    ),
                },
            },
        },
    })
}
```

--------------------------------

### Show GitHub App Installation

Source: https://developer.hashicorp.com/terraform/enterprise/v202405-1/api-docs/github-app-installations

Retrieves details for a specific GitHub App installation using its ID.

```APIDOC
## GET /github-app/installation/:gh_app_installation_id

### Description
This endpoint retrieves details for a specific GitHub App installation.

### Method
GET

### Endpoint
/github-app/installation/:gh_app_installation_id

### Path Parameters
- **gh_app_installation_id** (string) - Required - The HCP Terraform ID of the GitHub App installation.

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installation/ghain-R4xmKTaxnhLFioUq
```

### Response
#### Success Response (200)
- **data** (object) - A GitHub App installation object.
  - **id** (string) - The unique identifier for the GitHub App installation.
  - **type** (string) - The resource type, always 'github-app-installations'.
  - **attributes** (object) - Contains details about the installation.
    - **name** (string) - The name of the GitHub organization or user.
    - **installation-id** (integer) - The GitHub installation ID.
    - **icon-url** (string) - The URL of the GitHub App icon.
    - **installation-type** (string) - The type of installation (e.g., 'User', 'Organization').
    - **installation-url** (string) - The URL to manage the installation on GitHub.

#### Response Example
```json
{
    "data": {
        "id": "ghain-R4xmKTaxnhLFioUq",
        "type": "github-app-installations",
        "attributes": {
            "name": "octouser",
            "installation-id": 54810170,
            "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
            "installation-type": "User",
            "installation-url": "https://github.com/settings/installations/54810170"
        }
    }
}
```
```

--------------------------------

### Apply Terraform Configuration

Source: https://developer.hashicorp.com/terraform/tutorials/azure-get-started/azure-variables

This snippet demonstrates the basic execution of `terraform apply` to create infrastructure. It shows the confirmation prompt and the output indicating resource creation. This command is used after `terraform plan` to provision the resources defined in your configuration.

```shell
$ terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:
##...
Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

azurerm_resource_group.rg: Creating...
azurerm_resource_group.rg: Creation complete after 1s [id=/subscriptions/c9ed8610-47a3-4107-a2b2-a322114dfb29/resourceGroups/myTFResourceGroup]
azurerm_virtual_network.vnet: Creating...
azurerm_virtual_network.vnet: Creation complete after 7s [id=/subscriptions/c9ed8610-47a3-4107-a2b2-a322114dfb29/resourceGroups/myTFResourceGroup/providers/Microsoft.Network/virtualNetworks/myTFVnet]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

```

--------------------------------

### List GitHub App Installations

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/github-app-installations

This endpoint lists GitHub App installations available to the current user. Queries only return GitHub App Installations that the current user has access to within GitHub.

```APIDOC
## GET /github-app/installations

### Description
Lists GitHub App installations available to the current user. Queries only return GitHub App Installations that the current user has access to within GitHub.

### Method
GET

### Endpoint
/github-app/installations

### Parameters
#### Query Parameters
- **filter[name]** (string) - Optional - If present, returns a list of available GitHub App installations that match the GitHub organization or login.
- **filter[installation_id]** (integer) - Optional - If present, returns a list of available GitHub App installations that match the installation ID within GitHub. (Not HCP Terraform)

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installations
```

### Response
#### Success Response (200)
- **data** (array) - An array of GitHub App installation objects.
  - **id** (string) - The unique identifier for the GitHub App installation.
  - **type** (string) - The resource type, always "github-app-installations".
  - **attributes** (object) - Contains the details of the installation.
    - **name** (string) - The name of the GitHub organization or user.
    - **installation-id** (integer) - The GitHub installation ID.
    - **icon-url** (string) - The URL of the installation's icon.
    - **installation-type** (string) - The type of installation (e.g., "User", "Organization").
    - **installation-url** (string) - The URL to the installation settings in GitHub.

#### Response Example
```json
{
    "data": [
        {
            "id": "ghain-BYrbNeGQ8nAzKouu",
            "type": "github-app-installations",
            "attributes": {
                "name": "octouser",
                "installation-id": 54810170,
                "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
                "installation-type": "User",
                "installation-url": "https://github.com/settings/installations/54810170"
            }
        }
    ]
}
```
```

--------------------------------

### Apply Terraform Configuration for Resource Deployment

Source: https://developer.hashicorp.com/terraform/tutorials/azure/microsoft-caf-enterprise-scale

This snippet demonstrates the command-line execution of `terraform apply` to provision resources. It includes the interactive prompt to confirm the actions and the success message upon completion.

```bash
$ terraform apply

## ...

Plan: 111 to add, 0 to change, 26 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

Apply complete! Resources: 111 added, 0 changed, 26 destroyed.

```

--------------------------------

### Declare AWS Provider with Version Constraint in cdktf.json

Source: https://developer.hashicorp.com/terraform/cdktf/create-and-deploy/configuration-file

This example demonstrates how to declare the AWS provider in cdktf.json using the JSON format. It specifies the provider's name, source (including the organization), and a version constraint using the '~>' operator for a compatible version range. This configuration is used with 'cdktf get' to generate code bindings.

```json
{
  //...
  "terraformProviders": [
    {
      "name": "aws",
      "source": "hashicorp/aws",
      "version": "~> 3.22"
    }
  ]
}
```

--------------------------------

### Deploy Terraform Enterprise with Mounted Disk (YAML)

Source: https://developer.hashicorp.com/terraform/enterprise/v202404-1/flexible-deployments/install/docker/install

This Docker Compose configuration deploys Terraform Enterprise using a bind mount for persistent data storage. It requires a pre-existing host path for data and specifies volumes for TLS certificates and cache. Ensure the source path for the bind mount exists and is backed by durable storage.

```yaml
---
name: terraform-enterprise
services:
  tfe:
    image: images.releases.hashicorp.com/hashicorp/terraform-enterprise:<vYYYYMM-#>
    environment:
      TFE_LICENSE: "<Hashicorp license>"
      TFE_HOSTNAME: "<TFE hostname (DNS) e.g. terraform.example.com>"
      TFE_ENCRYPTION_PASSWORD: "<Encryption password>"
      TFE_OPERATIONAL_MODE: "disk"
      TFE_DISK_CACHE_VOLUME_NAME: "${COMPOSE_PROJECT_NAME}_terraform-enterprise-cache"
      TFE_TLS_CERT_FILE: "/etc/ssl/private/terraform-enterprise/cert.pem"
      TFE_TLS_KEY_FILE: "/etc/ssl/private/terraform-enterprise/key.pem"
      TFE_TLS_CA_BUNDLE_FILE: "/etc/ssl/private/terraform-enterprise/bundle.pem"
      TFE_IACT_SUBNETS: "<IACT subnet, eg. 10.0.0.0/8,192.168.0.0/24>"
    cap_add:
      - IPC_LOCK
    read_only: true
    tmpfs:
      - "/tmp:mode=01777"
      - "/run"
      - "/var/log/terraform-enterprise"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - type: bind
        source: /var/run/docker.sock
        target: /run/docker.sock
      - type: bind
        source: ./certs
        target: /etc/ssl/private/terraform-enterprise
      - type: bind
        source: <mounted_disk_path_on_host>
        target: /var/lib/terraform-enterprise
      - type: volume
        source: terraform-enterprise-cache
        target: /var/cache/tfe-task-worker/terraform
volumes:
  terraform-enterprise-cache:


```

--------------------------------

### Setup Go for Unit Tests (YAML)

Source: https://developer.hashicorp.com/terraform/plugin/testing/v1.13.x/acceptance-tests/continuous-integration

Checks out the repository code and configures the Go environment using the go.mod file for running unit tests.

```yaml
- uses: actions/checkout@v3
- uses: actions/setup-go@v4
    with:
      go-version-file: 'go.mod'
- run: go test -v -cover ./...
```

--------------------------------

### Create a Provider Platform

Source: https://developer.hashicorp.com/terraform/enterprise/v202206-1/registry/publish-providers

Creates a platform for a provider version, specifying the operating system and architecture. It returns a URL for uploading the provider binary.

```APIDOC
## POST /providers/{namespace}/{provider}/versions/{version}/platforms

### Description
Creates a platform for a provider version, specifying the operating system and architecture. It returns a URL for uploading the provider binary.

### Method
POST

### Endpoint
/providers/{namespace}/{provider}/versions/{version}/platforms

### Parameters
#### Path Parameters
- **namespace** (string) - Required - The namespace of the provider.
- **provider** (string) - Required - The name of the provider.
- **version** (string) - Required - The version string of the provider.

#### Query Parameters
- **os** (string) - Required - The target operating system (e.g., "linux", "windows").
- **arch** (string) - Required - The target architecture (e.g., "amd64", "386").
- **filename** (string) - Required - The name of the provider binary file.
- **download_url** (string) - Required - The URL where the binary will be hosted.
- **sha256** (string) - Required - The SHA256 checksum of the binary file.

### Response
#### Success Response (201 Created)
- **os** (string) - The operating system of the platform.
- **arch** (string) - The architecture of the platform.
- **filename** (string) - The filename of the provider binary.
- **download_url** (string) - The URL where the binary will be hosted.
- **sha256** (string) - The SHA256 checksum of the binary file.
- **links** (object) - URL for uploading the provider binary.
  - **provider_binary_upload** (string) - URL to upload the provider binary file.

#### Response Example
```json
{
  "os": "linux",
  "arch": "amd64",
  "filename": "terraform-provider-random_3.1.3_linux_amd64.zip",
  "download_url": "https://example.com/terraform-provider-random_3.1.3_linux_amd64.zip",
  "sha256": "...",
  "links": {
    "provider_binary_upload": "https://archivist.terraform.io/v1/object/dmF1b45c367djh45nj78"
  }
}
```
```

--------------------------------

### Validate S3 Bucket Prefix in TypeScript (CDKTF)

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/aspects

This TypeScript code defines a CDKTF Aspect that validates if S3 bucket names start with a given prefix. It implements the `IAspect` interface and visits each construct, checking `S3Bucket` instances. Errors are reported using `Annotations.of(node).addError` if the prefix requirement is not met. This snippet also includes the setup of an `AspectValidationStack` that applies this validation.

```typescript
import { Annotations, Aspects, IAspect, TerraformStack } from "cdktf";
import { Construct, IConstruct } from "constructs";
import { AwsProvider } from "./.gen/providers/aws/provider";
import { S3Bucket } from "./.gen/providers/aws/s3-bucket";

export class ValidateS3IsPrefixed implements IAspect {
  constructor(private prefix: string) {}

  // This method is called on every Construct within the defined scope (resource, data sources, etc.).
  visit(node: IConstruct) {
    if (node instanceof S3Bucket) {
      if (node.bucketInput && !node.bucketInput.startsWith(this.prefix)) {
        // You can include `addInfo`, `addWarning`, and `addError`.
        // CDKTF prints these messages when the user runs `synth`, `plan`, or `deploy`.
        Annotations.of(node).addError(
          `Each S3 Bucket name needs to start with ${this.prefix}`,
        );
      }
    }
  }
}

export class AspectValidationStack extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);

    new AwsProvider(this, "aws", {
      region: "us-west-2",
    });

    new S3Bucket(this, "bucket", {
      bucket: "myPrefixDemo",
    });

    Aspects.of(this).add(new ValidateS3IsPrefixed("myPrefix"));
  }
}
```

--------------------------------

### Execute Airgap Installation Script

Source: https://developer.hashicorp.com/terraform/enterprise/v202207-1/install/automated/automating-the-installer

This script is used to perform an airgapped installation of Terraform Enterprise. It requires the installer bootstrapper to be present and assumes it is unarchived in `/tmp`. The script takes several arguments, including installation mode, proxy settings, Docker version, and network addresses. Ensure you are in the directory containing the script before execution.

```shell
cd /tmp
./install.sh \
    airgap \
    no-proxy \
    docker-version=20.10.17 \
    private-address=1.2.3.4 \
    public-address=5.6.7.8
```

--------------------------------

### Terraform Import Block Configuration Example

Source: https://developer.hashicorp.com/terraform/language/block/import

This example demonstrates a complete `import` block configuration in Terraform, showcasing all supported arguments including `to`, `id`, `for_each` (for lists and maps), and `provider`. It's useful for understanding the structure and options available when importing resources.

```terraform
import {
  to = resource.type.address
  id = "cloud-provider-id"
  for_each = {                # `for_each` accepts a map or a set of strings
    <KEY> = <VALUE>
  }
  for_each = [            # `for_each` accepts a map or a set of strings
    "<VALUE>",
    "<VALUE>"
  ]
  provider = provider-name.alias
}

```

--------------------------------

### List GitHub App Installations using cURL

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/github-app-installations

This snippet demonstrates how to list all GitHub App installations accessible to the authenticated user using a cURL command. It requires an authorization token and specifies the content type. The response includes details for each installation, such as its ID, name, and associated GitHub installation ID.

```shell
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installations
```

--------------------------------

### Deploy Lab Environment

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

Executes a script to deploy the entire lab environment, including Docker Compose services and Terraform provisioning. This command initiates the setup process.

```bash
$ ./run all

```

--------------------------------

### Terraform 'contains' Function Examples

Source: https://developer.hashicorp.com/terraform/language/v1.8.x/functions/contains

These examples demonstrate the usage of the 'contains' function in Terraform. The first example shows a successful match, returning true, while the second example shows an unsuccessful match, returning false.

```hcl
> contains(["a", "b", "c"], "a")
true
> contains(["a", "b", "c"], "d")
false
```

```hcl
> contains(["a", "b", "c"], "a")
true
> contains(["a", "b", "c"], "d")
false
```

--------------------------------

### Show GitHub App Installation

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/github-app-installations

Retrieves details for a specific GitHub App installation using its ID.

```APIDOC
## GET /github-app/installation/:gh_app_installation_id

### Description
Retrieves details for a specific GitHub App installation using its ID.

### Method
GET

### Endpoint
/github-app/installation/:gh_app_installation_id

### Parameters
#### Path Parameters
- **gh_app_installation_id** (string) - Required - The Github App Installation ID.

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installation/ghain-R4xmKTaxnhLFioUq
```

### Response
#### Success Response (200)
- **data** (object) - The GitHub App installation object.
  - **id** (string) - The unique identifier for the GitHub App installation.
  - **type** (string) - The resource type, always "github-app-installations".
  - **attributes** (object) - Contains the details of the installation.
    - **name** (string) - The name of the GitHub organization or user.
    - **installation-id** (integer) - The GitHub installation ID.
    - **icon-url** (string) - The URL of the installation's icon.
    - **installation-type** (string) - The type of installation (e.g., "User", "Organization").
    - **installation-url** (string) - The URL to the installation settings in GitHub.

#### Response Example
```json
{
    "data": {
        "id": "ghain-R4xmKTaxnhLFioUq",
        "type": "github-app-installations",
        "attributes": {
            "name": "octouser",
            "installation-id": 54810170,
            "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
            "installation-type": "User",
            "installation-url": "https://github.com/settings/installations/54810170"
        }
    }
}
```
```

--------------------------------

### Complete Terraform Configuration for Boundary OIDC

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/oidc-auth0

This is a complete example of a `main.tf` file for setting up HashiCorp Boundary with OIDC authentication. It includes the provider configuration, the OIDC auth method resource, and an example OIDC account resource. All 'updateme' placeholders must be replaced with actual values.

```Terraform
terraform {
  required_providers {
    boundary = {
      source  = "hashicorp/boundary"
      version = "1.0.12"
    }
  }
}

provider "boundary" {
  addr                            = "BOUNDARY_ADDR" # updateme
  auth_method_id                  = "ampw_1234567890"    # updateme
  password_auth_method_login_name = "myuser"             # updateme
  password_auth_method_password   = "passpass"           # updateme
}

resource "boundary_auth_method_oidc" "provider" {
  name               = "Auth0"
  description        = "OIDC auth method for Auth0"
  scope_id           = "o_1234567890"                    # updateme
  issuer             = "https://dev-1vdl8c0q.us.auth0.com/"   # updateme
}
```

--------------------------------

### Minimal Terraform Module Structure Example

Source: https://developer.hashicorp.com/terraform/language/v1.13.x/modules/develop/structure

This example demonstrates the minimal recommended file structure for a Terraform module. It includes the essential files for a basic module, such as README.md, main.tf, variables.tf, and outputs.tf.

```tree
$+ tree minimal-module/
.
├── README.md
├── main.tf
├── variables.tf
└── outputs.tf

```

```tree
$+ tree minimal-module/
.
├── README.md
├── main.tf
├── variables.tf
└── outputs.tf

```

--------------------------------

### Sample Response for Listing Module Versions

Source: https://developer.hashicorp.com/terraform/internals/module-registry-protocol

Example JSON response when listing available versions for a Terraform module. The response includes a list of modules, each with an array of available versions.

```json
{
   "modules": [
      {
         "versions": [
            {"version": "1.0.0"},
            {"version": "1.1.0"},
            {"version": "2.0.0"}
         ]
      }
   ]
}
```

--------------------------------

### Implement Terraform Resource Example Widget Read Function (Go)

Source: https://developer.hashicorp.com/terraform/plugin/sdkv2/best-practices/deprecations

Implements the Read function for the 'example_widget' Terraform resource. It retrieves attribute values and sets them on the resource data, prioritizing 'existing_attribute' if present, otherwise using 'new_attribute'.

```go
func resourceExampleWidgetRead(d *schema.ResourceData, meta any) error {
    // ... other logic ...

    if _, ok := d.GetOk("existing_attribute"); ok {
        d.Set("existing_attribute", /* ... */)
    } else {
        d.Set("new_attribute", /* ... */)
    }

    // ... other logic ...
    return nil
}
```

--------------------------------

### Retrieve a Specific GitHub App Installation using cURL

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/github-app-installations

This snippet shows how to fetch details for a particular GitHub App installation using its unique ID via a cURL command. Similar to listing installations, it requires an authorization token and the correct content type. The response provides comprehensive information about the specified installation.

```shell
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installation/ghain-R4xmKTaxnhLFioUq
```

--------------------------------

### Clone Terraform Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/1-0/refresh

Clones the sample repository containing Terraform configuration for the tutorial. This repository includes the necessary files to follow along with the refresh-only mode demonstration.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-refresh
```

--------------------------------

### Show GitHub App Installation

Source: https://developer.hashicorp.com/terraform/enterprise/v202402-2/api-docs/github-app-installations

Retrieves details for a specific GitHub App installation using its HCP Terraform ID.

```APIDOC
## GET /github-app/installation/:gh_app_installation_id

### Description
This endpoint retrieves details for a specific GitHub App installation identified by its HCP Terraform ID.

### Method
GET

### Endpoint
/github-app/installation/:gh_app_installation_id

### Parameters
#### Path Parameters
- **gh_app_installation_id** (string) - Required - The HCP Terraform ID of the GitHub App installation.

### Request Example
```bash
curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installation/ghain-R4xmKTaxnhLFioUq
```

### Response
#### Success Response (200)
- **data** (object) - The GitHub App installation object.
  - **id** (string) - The unique identifier for the HCP Terraform GitHub App installation.
  - **type** (string) - The resource type, always 'github-app-installations'.
  - **attributes** (object) - Contains the details of the GitHub App installation.
    - **name** (string) - The name of the GitHub organization or user the app is installed for.
    - **installation-id** (integer) - The unique ID of the installation in GitHub.
    - **icon-url** (string) - URL to the icon representing the GitHub organization or user.
    - **installation-type** (string) - Type of installation (e.g., 'User', 'Organization').
    - **installation-url** (string) - URL to manage the installation in GitHub settings.

#### Response Example
```json
{
    "data": {
        "id": "ghain-R4xmKTaxnhLFioUq",
        "type": "github-app-installations",
        "attributes": {
            "name": "octouser",
            "installation-id": 54810170,
            "icon-url": "https://avatars.githubusercontent.com/u/29916665?v=4",
            "installation-type": "User",
            "installation-url": "https://github.com/settings/installations/54810170"
        }
    }
}
```
```

--------------------------------

### Clone Example Repository for Vault-backed Dynamic Credentials

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/dynamic-credentials-vault

This command clones the example repository containing Terraform configurations necessary to establish a trust relationship between AWS and HCP Terraform for Vault-backed dynamic credentials.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-vault-backed-dynamic-credentials
```

--------------------------------

### Create Provider Platform and Upload Binary (Terraform Cloud API)

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-3/registry/publish-providers

This snippet illustrates the process of creating a provider platform and uploading the corresponding binary file. It involves obtaining a provider binary upload URL and then using cURL to transfer the platform-specific binary.

```json
{
  "links": {
    "provider-binary-upload": "https://archivist.terraform.io/v1/object/dmF1b45c367djh45nj78"
  }
}
```

```bash
$ curl -T local-example/terraform-provider-random_3.1.3_linux_amd64.zip \
  https://archivist.terraform.io/v1/object/dmF1b45c367djh45nj78
```

```bash
$ curl -T local-example/terraform-provider-random_3.1.3_linux_amd64.zip \
  https://archivist.terraform.io/v1/object/dmF1b45c367djh45nj78
```

--------------------------------

### Clone Terraform Example Repository (Bash)

Source: https://developer.hashicorp.com/terraform/tutorials/policy/drift-and-policy

This command clones a Terraform example repository from GitHub. Replace 'USER' with your GitHub username. This is a prerequisite for following the tutorial's steps.

```bash
git clone https://github.com/USER/learn-terraform-drift-and-policy

```

--------------------------------

### Get Length of List, Map, or String - Terraform

Source: https://developer.hashicorp.com/terraform/language/configuration-0-11/interpolation

The `length` function calculates the number of elements in a list or map, or the number of characters in a string. Examples: `${length(split(",", "a,b,c"))}`, `${length("a,b,c")}`, `${length(map("key", "val"))}`.

```Terraform
length(split(",", "a,b,c"))
```

```Terraform
length("a,b,c")
```

```Terraform
length(map("key", "val"))
```

--------------------------------

### Provision a Compute Instance in GCP using Terraform

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/dynamic-credentials

This Terraform configuration provisions a single compute instance in the 'us-east1' region using the Google Cloud provider. It defines a Debian 11 boot disk and configures metadata startup script to install and start an Apache web server. The machine type and tags are configurable via variables.

```Terraform
provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
  zone    = var.gcp_zone
}

resource "google_compute_instance" "vm_instance" {
  name         = "terraform-instance"
  machine_type = var.machine_type

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = "default"
    access_config {
    }
  }

  metadata_startup_script = <<-EOF
    #!/bin/bash
    sudo yum update -y
    sudo yum install httpd -y
    sudo systemctl enable httpd
    sudo systemctl start httpd
    echo "<html><body><div>Hello, world!</div></body></html>" > /var/www/html/index.html
    EOF

  tags = var.tags
}

```

--------------------------------

### Launch Docker Container and Connect to Cassandra

Source: https://developer.hashicorp.com/terraform/tutorials/aws/aws-cloud-control

Launches the 'amazon/keyspaces-toolkit' Docker container, mounting local data, and passing AWS credentials. It then connects to the Amazon Keyspaces Cassandra database using cqlsh-expansion with SigV4 authentication.

```bash
$ docker run -ti --rm --mount type=bind,src=$(pwd)/data,dst=/data \
         --env-file ./aws_auth_env \
         --env AWS_DEFAULT_REGION="$(terraform output -raw aws_region)" \
         --entrypoint cqlsh-expansion amazon/keyspaces-toolkit \
                      cassandra.$(terraform output -raw aws_region).amazonaws.com \
                      -k $(terraform output -raw keyspace_name) \
                      --ssl --auth-provider "SigV4AuthProvider"
```

--------------------------------

### SAML Authentication Request Example

Source: https://developer.hashicorp.com/terraform/enterprise/v202506-1/saml/idp-configuration

This section shows an example of a SAML AuthnRequest sent by Terraform Enterprise before user sign-on.

```APIDOC
## POST /users/saml/auth

### Description
This endpoint is used to initiate the SAML authentication flow. Terraform Enterprise sends an AuthnRequest to the Identity Provider (IdP) for user sign-on.

### Method
POST

### Endpoint
/users/saml/auth

### Parameters
#### Query Parameters
None

#### Request Body
This is an example of the SAML AuthnRequest payload, which is typically sent as part of a POST request.

### Request Example
```xml
<samlp:AuthnRequest AssertionConsumerServiceURL='https://app.terraform.io/users/saml/auth' Destination='https://example.onelogin.com/trust/saml2/http-post/sso/1' ID='_000eda0a-c0f0-00cf-b0a0-c00b000d000f' IssueInstant='2018-02-28T02:16:25Z' Version='2.0' xmlns:saml='urn:oasis:names:tc:SAML:2.0:assertion' xmlns:samlp='urn:oasis:names:tc:SAML:2.0:protocol'>
  <saml:Issuer>https://app.terraform.io/users/saml/metadata</saml:Issuer>
  <samlp:NameIDPolicy AllowCreate='true' Format='urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress'/>
</samlp:AuthnRequest>
```

### Response
#### Success Response (200)
This endpoint typically redirects the user to the IdP for authentication. A direct success response is not usually observed in this part of the flow.

#### Response Example
(Redirection to Identity Provider)
```

--------------------------------

### Terraform JSON Filter: Indexes

Source: https://developer.hashicorp.com/terraform/enterprise/v202302-1/workspaces/json-filtering

Indexes are used to access elements within JSON arrays or fields with non-alphanumeric keys in JSON objects. Array elements are accessed by their numerical index (starting from 0), while object fields are accessed using their string representation within square brackets. For example, `["foo-bar"]` accesses the field named 'foo-bar'.

```jq-like
// Example: Accessing an array element
.[0]
```

```jq-like
// Example: Accessing an object field with a hyphen
.["foo-bar"]
```

```jq-like
// Example: Combining selectors and indexes
.["foo-bar"][0]
```

--------------------------------

### Apply Terraform Configuration to Create Spotify Playlist

Source: https://developer.hashicorp.com/terraform/tutorials/community-providers/spotify-playlist

This snippet demonstrates how to apply a Terraform configuration to create a new Spotify playlist. It shows the expected output during the apply process, including resource creation and plan confirmation.

```bash
$ terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are
indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # spotify_playlist.playlist will be created
  + resource "spotify_playlist" "playlist" {
      + description = "This playlist was created by Terraform"
      + id          = (known after apply)
      + name        = "Terraform Summer Playlist"
      + public      = true
      + snapshot_id = (known after apply)
      + tracks      = [
          + "2SpEHTbUuebeLkgs9QB7Ue",
          + "4w3tQBXhn5345eUXDGBWZG",
          + "6dnco8haegnJYtylV26cBq",
        ]
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + playlist_url = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:

```

```bash
  Enter a value: yes

spotify_playlist.playlist: Creating...
spotify_playlist.playlist: Creation complete after 1s [id=40bGNifvqzwjO8gHDvhbB3]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

playlist_url = "https://open.spotify.com/playlist/40bGNifvqzwjO8gHDvhbB3"

```

--------------------------------

### Read List Argument Data in Terraform Functions (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.12.x/functions/parameters/list

Demonstrates how to define and read a list of string arguments within a Terraform function. It shows the `Definition` method for parameter setup and the `Run` method for accessing the argument value using `req.Arguments.Get()`. The code handles Go nil for Terraform null and includes a commented-out example for `AllowUnknownValues`.

```go
func (f ExampleFunction) Definition(ctx context.Context, req function.DefinitionRequest, resp *function.DefinitionDefinitionResponse) {
    resp.Definition = function.Definition{
        // ... other Definition fields ...
        Parameters: []function.Parameter{
            function.ListParameter{
                ElementType: types.StringType,
                Name: "list_param",
            },
        },
    }
}

func (f ExampleFunction) Run(ctx context.Context, req function.RunRequest, resp *function.RunResponse) {
    var listArg []*string // Go nil equals Terraform null
    // var listArg types.List // e.g. with AllowUnknownValues

    resp.Error = function.ConcatFuncErrors(resp.Error, req.Arguments.Get(ctx, &listArg))

    // listArg is now populated
    // ... other logic ...
}

```

--------------------------------

### Implement Order Resource Acceptance Test in Go

Source: https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework/providers-plugin-framework-acceptance-testing

This Go code snippet demonstrates how to implement acceptance tests for the `hashicups_order` resource using the Terraform plugin testing framework. It covers create, read, import, and update scenarios, verifying resource attributes and dynamic values. Dependencies include the `testing` package and `github.com/hashicorp/terraform-plugin-testing/helper/resource`.

```go
package provider

import (
    "testing"

    "github.com/hashicorp/terraform-plugin-testing/helper/resource"
)

func TestAccOrderResource(t *testing.T) {
    resource.Test(t, resource.TestCase{
        ProtoV6ProviderFactories: testAccProtoV6ProviderFactories,
        Steps: []resource.TestStep{
            // Create and Read testing
            {
                Config: providerConfig + `
resource "hashicups_order" "test" {
  items = [
    {
      coffee = {
        id = 1
      }
      quantity = 2
    },
  ]
}
`,
                Check: resource.ComposeAggregateTestCheckFunc(
                    // Verify number of items
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.#", "1"),
                    // Verify first order item
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.quantity", "2"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.id", "1"),
                    // Verify first coffee item has Computed attributes filled.
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.description", ""),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.image", "/hashicorp.png"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.name", "HCP Aeropress"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.price", "200"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.teaser", "Automation in a cup"),
                    // Verify dynamic values have any value set in the state.
                    resource.TestCheckResourceAttrSet("hashicups_order.test", "id"),
                    resource.TestCheckResourceAttrSet("hashicups_order.test", "last_updated"),
                ),
            },
            // ImportState testing
            {
                ResourceName:      "hashicups_order.test",
                ImportState:       true,
                ImportStateVerify: true,
                // The last_updated attribute does not exist in the HashiCups
                // API, therefore there is no value for it during import.
                ImportStateVerifyIgnore: []string{"last_updated"},
            },
            // Update and Read testing
            {
                Config: providerConfig + `
resource "hashicups_order" "test" {
  items = [
    {
      coffee = {
        id = 2
      }
      quantity = 2
    },
  ]
}
`,
                Check: resource.ComposeAggregateTestCheckFunc(
                    // Verify first order item updated
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.quantity", "2"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.id", "2"),
                    // Verify first coffee item has Computed attributes updated.
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.description", ""),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.image", "/packer.png"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.name", "Packer Spiced Latte"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.price", "350"),
                    resource.TestCheckResourceAttr("hashicups_order.test", "items.0.coffee.teaser", "Packed with goodness to spice up your images"),
                ),
            },
            // Delete testing automatically occurs in TestCase
        },
    })
}

```

--------------------------------

### Clone Terraform AWS ASG Example Repository

Source: https://developer.hashicorp.com/terraform/tutorials/aws/aws-asg

Clones the example repository containing Terraform configuration for an AWS Auto Scaling group. This is the first step to follow along with the tutorial.

```bash
git clone https://github.com/hashicorp-education/learn-terraform-aws-asg

```

--------------------------------

### Create Stack Component Configuration (VCS-backed)

Source: https://developer.hashicorp.com/terraform/cloud-docs/api-docs/private-registry/stack-component-configurations

This snippet demonstrates how to publish a stack component configuration using a VCS-backed workflow via the Terraform Registry API. It requires specifying the organization name, repository details, and optionally an OAuth token ID or GitHub App installation ID for authentication. The `source-directory` and `tag-prefix` can be used for monorepo setups.

```json
{
  "data": {
    "type": "registry-components",
    "attributes": {
      "name": "my-component",
      "vcs-repo": {
        "identifier": "my-org/my-repo",
        "oauth-token-id": "ot-xxxxxxxxxxxxxxxx",
        "source-directory": "/path/to/component",
        "tag-prefix": "v"
      }
    }
  }
}
```

--------------------------------

### Connect to PostgreSQL Target using Boundary CLI

Source: https://developer.hashicorp.com/terraform/tutorials/hashicorp/target-aware-workers

This snippet shows how to establish a connection to a PostgreSQL target using the `boundary connect` command. It requires the target name, target scope name, username, and the psql CLI tool. The example includes troubleshooting steps for connection errors.

```bash
$ boundary connect postgres -target-name postgres -target-scope-name databases -username postgres -- -l
psql: error: connection to server at "127.0.0.1", port 53971 failed: server closed the connection unexpectedly
    This probably means the server terminated abnormally
    before or while processing the request.

```

```bash
$ boundary connect postgres -target-name postgres -target-scope-name databases -username postgres -- -l
Password for user postgres:
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
(4 rows)

```

--------------------------------

### Terraform endswith Function Examples

Source: https://developer.hashicorp.com/terraform/language/functions/endswith

These examples demonstrate the usage of the `endswith` function in Terraform. The first example shows a case where the string does end with the specified suffix, resulting in `true`. The second example shows a case where the string does not end with the suffix, resulting in `false`.

```terraform
> endswith("hello world", "world")
true

> endswith("hello world", "hello")
false
```

--------------------------------

### Implement Terraform Resource List Method (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/list-resources/list

This Go code snippet demonstrates the implementation of the `List` method for a Terraform resource. It shows how to access configuration data from the `ListRequest`, process it (simulating external API calls), and then iterate through results to create and push `ListResult` objects into a stream. It also includes basic error handling for configuration retrieval and highlights how to set display names, identities, and resource details for each item in the list.

```go
// ThingListResource defines the list implementation.
// Some list.ListResource interface methods are omitted for brevity.
type ThingListResource struct{}

type ThingListResourceModel struct {
    ResourceGroupName types.String `tfsdk:"resource_group_name"`
}

func (r *ThingListResource) ListResourceConfigSchema(_ context.Context, _ list.ListResourceConfigSchemaRequest, resp *list.ListResourceConfigSchemaResponse) {
    resp.Schema = listschema.Schema{
        Attributes: map[string]listschema.Attribute{
            "resource_group_name": listschema.StringAttribute{
                Description: "Name of the resource group to list things in.",
                Required:    true,
            },
        },
    }
}

func (r *ThingListResource) List(ctx context.Context, req list.ListRequest, stream *list.ListResultsStream) {
    var data ThingListResourceModel

    // Read list config data into the model
    diags := req.Config.Get(ctx, &data)....
    if diags.HasError() {
        stream.Results = list.ListResultsStreamDiagnostics(diags)
        return
    }

    // Typically lists will make external calls here using data from the config
    // as input. For brevity, we assume the `things` slice below was returned by an
    // API call here

    // Define the function that will push results into the stream
    stream.Results = func(push func(list.ListResult) bool) {
        for _, thing := range things {
        // Initialize a new result object for each thing
        result := req.NewListResult(ctx)

        // Set the user-friendly name of this thing
        result.DisplayName = thing.Name

        // Set resource identity data on the result
        result.Diagnostics.Append(result.Identity.Set(ctx, thing.ID))

        // Set the resource information on the result
        result.Diagnostics.Append(result.Resource.Set(ctx, thing.Resource))

        // Send the result to the stream.
        if !push(result) {
            return
        }
    }
}


```

--------------------------------

### tf-migrate prepare Command Execution and Output

Source: https://developer.hashicorp.com/terraform/enterprise/v202411-1/migrate/tf-migrate/reference/prepare

Demonstrates the execution of the `tf-migrate prepare` command, which prepares configurations for migrating Terraform state to HCP Terraform. It shows the interactive prompts and successful completion messages, including organization selection and branch creation.

```bash
$ tf-migrate prepare\n✓ Current working directory: /tmp/backend-test/learn-terraform-migrate\n✓ Environment readiness checks completed\n✓ Found 3 HCP Terraform organizations\n┌────────────────────────────┐\n│ Available Orgs             │\n├────────────────────────────┤\n│ my-org-1                   │\n│ my-org-2                   │\n│ my-org-3                   │\n└────────────────────────────┘\nEnter the name of the HCP Terraform organization to migrate to:  my-org-1\n✓ You have selected organization my-org-1 for migration\n✓ Found 1 directories with Terraform files\n┌────────────────────────────────┐\n│   Terraform File Directories   │\n├────────────────────────────────┤\n│ learn-terraform-migrate        │\n└────────────────────────────────┘\nCreate a local branch named hcp-migrate-main from the current branch main: ... ?\n\n\n  Only 'yes or no' will be accepted as input.\n  Type 'yes' to approve the step\n  Type 'no' to to skip\n\n\nEnter a value:  yes\n\n✓ Successfully created branch hcp-migrate-main\nDo you want to open a pull request from hcp-migrate-main ... ?\n\n\n  Only 'yes or no' will be accepted as input.\n  Type 'yes' to approve the step\n  Type 'no' to to skip\n\n\nEnter a value:  yes\n\n✓ Migration config generation completed\n
```

--------------------------------

### Implement Terraform Provider Resources (Single Resource)

Source: https://developer.hashicorp.com/terraform/plugin/framework/providers

This Go code demonstrates how a Terraform provider implements the `Resources` method to define its available resources. It returns a slice of functions, each creating a new instance of a resource type, ensuring data isolation between operations. This example shows a provider with a single resource.

```go
// With the provider.Provider implementation
func (p *ExampleCloudProvider) Resources(_ context.Context) []func() resource.Resource {
    return []func() resource.Resource{
        NewThingResource,
    }
}

// With the resource.Resource implementation
func NewThingResource() resource.Resource {
    return &ThingResource{}
}

type ThingResource struct {}
```

--------------------------------

### Clone Example Terraform Repository (Shell)

Source: https://developer.hashicorp.com/terraform/tutorials/applications/confluent-provider

Clones the example repository containing Terraform configurations for Confluent Cloud resources. This repository provides the necessary files to follow along with the tutorial.

```shell
git clone https://github.com/hashicorp-education/learn-terraform-confluent-provider
```

--------------------------------

### Terraform Provider Resource Implementation (Go)

Source: https://developer.hashicorp.com/terraform/plugin/framework/v1.1.x/providers

This Go code illustrates how a Terraform provider implements the `Resources` method to return a slice of resource creation functions. It shows a basic implementation for a single resource ('ThingResource') and how to group multiple resources using Go slices and packages.

```go
// With the provider.Provider implementation
func (p *ExampleCloudProvider) Resources(_ context.Context) []func() resource.Resource {
    return []func() resource.Resource{
        NewThingResource,
    }
}

// With the resource.Resource implementation
func NewThingResource() resource.Resource {
    return &ThingResource{}
}

type ThingResource struct {}
```

```go
// With the provider.Provider implementation
func (p *ExampleCloudProvider) Resources(_ context.Context) []func() resource.Resource {
    return []func() resource.Resource{
        servicex.Resources...,
        servicey.Resources...
    }
}

// With the servicex implementation
package servicex

var Resources = []func() resource.Resource {
    NewThingResource,
    NewWidgetResource,
}

func NewThingResource() resource.Resource {
    return &
}

type ThingResource {}

func NewWidgetResource() resource.Resource {
    return &WidgetResource{}
}

type WidgetResource {}
```

--------------------------------

### List GitHub App Installations (Bash)

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/api-docs/github-app-installations

Lists all GitHub App installations accessible by the current user. This command requires an API token for authentication and specifies the content type as JSON. Optional query parameters can filter the results by name or installation ID.

```Bash
# List all GitHub App installations
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installations

# List GitHub App installations filtered by name
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installations?filter[name]=octouser

# List GitHub App installations filtered by installation ID
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installations?filter[installation_id]=54810170
```

--------------------------------

### Initialize HCP Terraform Workspace with Azure Provider

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/stacks-migrate

This command initializes the HCP Terraform workspace, downloading necessary provider plugins for Azure. It shows the installation of `azurerm`, `tls`, and `random` providers and confirms successful initialization.

```bash
$ terraform init
Initializing HCP Terraform...
Initializing provider plugins...
- Reusing previous version of hashicorp/azurerm from the dependency lock file
- Reusing previous version of hashicorp/tls from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/azurerm v4.51.0...
- Installed hashicorp/azurerm v4.51.0 (signed by HashiCorp)
- Installing hashicorp/tls v4.1.0...
- Installed hashicorp/tls v4.1.0 (signed by HashiCorp)
- Installing hashicorp/random v3.7.2...
- Installed hashicorp/random v3.7.2 (signed by HashiCorp)

HCP Terraform has been successfully initialized!

You may now begin working with HCP Terraform. Try running "terraform plan" to
see any changes that are required for your infrastructure.

If you ever set or change modules or Terraform Settings, run "terraform init"
again to reinitialize your working directory.

```

--------------------------------

### Install tf-migrate using Homebrew on macOS

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/migrate/tf-migrate

This snippet demonstrates how to install the tf-migrate CLI using the Homebrew package manager on macOS. It first adds the HashiCorp tap to Homebrew and then installs the tf-migrate formula. Ensure Homebrew is installed on your system before running these commands.

```bash
$ brew tap hashicorp/tap
$ brew install hashicorp/tap/tf-migrate
```

--------------------------------

### SAML Authentication Request Example

Source: https://developer.hashicorp.com/terraform/enterprise/v202208-3/user-management/saml/idp-configuration

This section provides an example of an AuthnRequest sent from Terraform Enterprise before single sign-on, and the expected response from an identity provider.

```APIDOC
## POST /users/saml/auth

### Description
This endpoint facilitates single sign-on (SSO) for Terraform Enterprise using SAML. It handles authentication requests initiated by Terraform Enterprise and processes responses from configured identity providers.

### Method
POST

### Endpoint
/users/saml/auth

### Parameters
#### Query Parameters
None

#### Request Body
This endpoint expects a SAML AuthnRequest, typically sent as part of an SSO flow. The exact format is defined by the SAML protocol.

### Request Example
```xml
<samlp:AuthnRequest AssertionConsumerServiceURL='https://app.terraform.io/users/saml/auth' Destination='https://example.onelogin.com/trust/saml2/http-post/sso/1' ID='_000eda0a-c0f0-00cf-b0a0-c00b000d000f' IssueInstant='2018-02-28T02:16:25Z' Version='2.0' xmlns:saml='urn:oasis:names:tc:SAML:2.0:assertion' xmlns:samlp='urn:oasis:names:tc:SAML:2.0:protocol'>
  <saml:Issuer>https://app.terraform.io/users/saml/metadata</saml:Issuer>
  <samlp:NameIDPolicy AllowCreate='true' Format='urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress'/>
</samlp:AuthnRequest>
```

### Response
#### Success Response (200)
Upon successful authentication, the identity provider will typically redirect the user back to Terraform Enterprise with a SAML assertion. The specific response format depends on the IdP and SAML configuration.

#### Response Example
(Response is typically a SAML assertion within an HTML form for auto-submission to the AssertionConsumerServiceURL)
```

--------------------------------

### Runs, Plans, and Applies Updates

Source: https://developer.hashicorp.com/terraform/enterprise/v202409-3/api-docs/changelog

Introduces support for `import` blocks, with new options and properties for Runs, Plans, and Applies.

```APIDOC
## POST /runs/{id}

### Description
Updates a run, including the new `allow-config-generation` option for import blocks.

### Method
POST

### Endpoint
/runs/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the run.

#### Request Body
- **allow_config_generation** (boolean) - Optional - Enables configuration generation for import blocks.

### Response
#### Success Response (200)
- **id** (string) - The ID of the updated run.
- **allow_config_generation** (boolean) - The status of configuration generation.

#### Response Example
```json
{
  "id": "run-abcdef123456",
  "allow_config_generation": true
}
```
```

```APIDOC
## GET /plans/{id}

### Description
Retrieves details of a plan, including new properties related to resource imports and generated configuration.

### Method
GET

### Endpoint
/plans/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the plan.

### Response
#### Success Response (200)
- **id** (string) - The ID of the plan.
- **resource_imports** (array) - A list of resource imports.
- **generated_configuration** (string) - The generated configuration content.
- ... (other plan attributes)

#### Response Example
```json
{
  "id": "plan-abcdef123456",
  "resource_imports": [
    {
      "address": "aws_s3_bucket.example",
      "type": "aws_s3_bucket"
    }
  ],
  "generated_configuration": "resource \"aws_s3_bucket\" \"example\" {\n  bucket = \"my-bucket\"\n}"
}
```
```

```APIDOC
## POST /applies/{id}

### Description
Updates an apply, including the new `resource_imports` property.

### Method
POST

### Endpoint
/applies/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the apply.

#### Request Body
- **resource_imports** (array) - Optional - A list of resource imports associated with the apply.
  - **address** (string) - Required - The address of the resource.
  - **type** (string) - Required - The type of the resource.

### Response
#### Success Response (200)
- **id** (string) - The ID of the updated apply.
- **resource_imports** (array) - The list of resource imports.

#### Response Example
```json
{
  "id": "apply-abcdef123456",
  "resource_imports": [
    {
      "address": "aws_s3_bucket.example",
      "type": "aws_s3_bucket"
    }
  ]
}
```
```

--------------------------------

### Provision an EC2 Instance in AWS using Terraform

Source: https://developer.hashicorp.com/terraform/tutorials/cloud/dynamic-credentials

This Terraform configuration provisions a single EC2 instance in the 'us-east-2' region using the AWS provider. It utilizes a data source to find the latest Amazon Linux 2 AMI and configures user data to install and start an Apache web server. The instance type and tags are configurable via variables.

```Terraform
provider "aws" {
  region = var.aws_region
}

data "aws_ami" "amazon_linux" {
  most_recent = true
  owners    = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.amazon_linux.id
  instance_type = var.instance_type

  user_data = <<-EOF
    #!/bin/bash
    sudo yum update -y
    sudo yum install httpd -y
    sudo systemctl enable httpd
    sudo systemctl start httpd
    echo "<html><body><div>Hello, world!</div></body></html>" > /var/www/html/index.html
    EOF

  tags = var.tags
}

```

--------------------------------

### Apply Terraform Configuration and Output URL

Source: https://developer.hashicorp.com/terraform/tutorials/configuration-language/resource

This snippet demonstrates the command to apply Terraform configurations and the expected output after a successful apply. It shows the creation of resources and provides an example of the `application-url` output, which is used to access the deployed web application.

```bash
$ terraform apply
## ...

Apply complete! Resources: 1 added, 1 changed, 0 destroyed.

Outputs:

application-url = "ec2-18-236-123-132.us-west-2.compute.amazonaws.com/index.php"
domain-name = "ec2-18-236-123-132.us-west-2.compute.amazonaws.com"
```

--------------------------------

### Execute Airgap Installation Script

Source: https://developer.hashicorp.com/terraform/enterprise/1.0.x/deploy/replicated/install/automated/automating-the-installer

This script is used to perform an airgapped installation of Terraform Enterprise. It requires the installer bootstrapper to be present in `/tmp`. Ensure you are in the directory containing the script before execution. The script accepts parameters for airgap mode, proxy settings, and private/public IP addresses.

```shell
cd /tmp
./install.sh \
    airgap \
    no-proxy \
    private-address=1.2.3.4 \
    public-address=5.6.7.8

```

--------------------------------

### Define Resource Schema in SDKv2

Source: https://developer.hashicorp.com/terraform/plugin/framework/migrating/resources

This Go code defines the schema for 'example_resource' in SDKv2. It includes an 'attribute' which is a required string, forces replacement on change, and has a validation function to ensure it's one of 'a' or 'b'.

```go
func exampleResource() *schema.Resource {
    return &schema.Resource{
        CreateContext: createResource,
        DeleteContext: deleteResource,
        ReadContext:   readResource,

        Schema: map[string]*schema.Schema{
            "attribute": {
                Type:             schema.TypeString,
                Required:         true,
                ForceNew:         true,
                ValidateDiagFunc: validation.ToDiagFunc(validation.StringInSlice([]string{'a', 'b'}, false)),
            },
            /* ... */

```

--------------------------------

### Prompt for Azure Storage Buckets (User Input)

Source: https://developer.hashicorp.com/terraform/docs/tools/mcp-server/prompt

This is an example of a user prompt intended to solicit information about setting up storage buckets within the Azure provider using the Terraform MCP server. The prompt is designed to be specific enough to be routed to the MCP server.

```text
I need help setting up storage buckets in the azure provider
```

--------------------------------

### Install Container Tools on RHEL 9

Source: https://developer.hashicorp.com/terraform/enterprise/v202312-1/flexible-deployments/install/podman/requirements

Installs the `container-tools` package on RHEL 9, which includes Podman, Buildah, and Skopeo, simplifying the installation process with a single command.

```bash
dnf install -y container-tools
```

--------------------------------

### Main Application Entry Point in C#

Source: https://developer.hashicorp.com/terraform/cdktf/concepts/variables-and-outputs

The main entry point for the C# CDKTF application. It initializes the CDKTF App, instantiates the Producer and Consumer stacks, and synthesizes the Terraform configuration.

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using System.Linq;
using Constructs;
using HashiCorp.Cdktf;
using random.Provider;
using random.Pet;

namespace Examples
{
    class Main
    {
                public static void Main(string[] args)
                {
                    App app = new App();
                    new Producer(app, "cdktf-producer");
                    new Consumer(app, "cdktf-consumer");
                    app.Synth();
                }
    }

}
```

--------------------------------

### Terraform Apply Execution and Output

Source: https://developer.hashicorp.com/terraform/tutorials/cli/state-cli

Demonstrates the execution of 'terraform apply' command, showing the plan, resource creation progress, and final apply completion with output details. It includes the interactive prompt for applying changes.

```bash
$ terraform apply
data.aws_ami.ubuntu: Reading...
data.aws_ami.ubuntu: Read complete after 0s [id=ami-027a754129abb5386]

Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
##...
Plan: 2 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + aws_region     = "us-east-1"
  + instance_id    = (known after apply)
  + public_ip      = (known after apply)
  + security_group = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_security_group.sg_8080: Creating...
aws_security_group.sg_8080: Creation complete after 3s [id=sg-0adfd0a0ade3eebdc]
aws_instance.example: Creating...
aws_instance.example: Still creating... [10s elapsed]
aws_instance.example: Still creating... [20s elapsed]
aws_instance.example: Still creating... [30s elapsed]
aws_instance.example: Creation complete after 32s [id=i-05a8893f05c6a37be]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

Outputs:

aws_region = "us-east-1"
instance_id = "i-05a8893f05c6a37be"
public_ip = "18.212.104.187"
security_group = "sg-0adfd0a0ade3eebdc"
```

--------------------------------

### Deploy Kubernetes Web App with Terraform CDK (C#)

Source: https://developer.hashicorp.com/terraform/cdktf/v0.12.x/concepts/constructs

This C# code snippet demonstrates setting up a Terraform CDK application, configuring the Kubernetes provider with a local kubeconfig path, and deploying a web application using the KubernetesWebAppDeployment construct. It defines deployment properties such as image, replicas, and environment.

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using System.Linq;
using Constructs;
using HashiCorp.Cdktf;
using kubernetes;
using MyConstructs;
namespace MyCompany.MyApp
{
    class MyApp : TerraformStack
    {
        public MyApp(Construct scope, string name) : base(scope, name)
        {

            new KubernetesProvider(this, "kind", new KubernetesProviderConfig {
                ConfigPath = Path.Join(Environment.CurrentDirectory, "../kubeconfig.yaml")
            });
            new KubernetesWebAppDeployment(this, "deployment", new Dictionary<string, object> {
                { "image", "nginx:latest" },
                { "replicas", 2 },
                { "app", "myapp" },
                { "component", "frontend" },
                { "environment", "dev" }
            });
        }

        public static void Main(string[] args)
        {
            App app = new App();
            new MyApp(app, "demo");
            app.Synth();
            Console.WriteLine("App synth complete");
        }
    }
}
```

--------------------------------

### Show Specific GitHub App Installation (Bash)

Source: https://developer.hashicorp.com/terraform/enterprise/v202303-1/api-docs/github-app-installations

Retrieves details for a specific GitHub App installation using its unique ID. This API call requires authentication with a bearer token and specifies the JSON content type. The `:gh_app_installation_id` placeholder must be replaced with the actual installation ID.

```Bash
# Show a specific GitHub App installation
$ curl \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  https://app.terraform.io/api/v2/github-app/installation/ghain-R4xmKTaxnhLFioUq
```