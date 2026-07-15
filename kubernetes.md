### kubectl run Examples: Basic Pod Creation

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/_print

Demonstrates the basic usage of `kubectl run` to start pods with specified container images. Includes examples for starting a simple nginx pod and a hazelcast pod, with and without exposing specific ports.

```bash
# Start a nginx pod
kubectl run nginx --image=nginx

# Start a hazelcast pod and let the container expose port 5701
kubectl run hazelcast --image=hazelcast/hazelcast --port=5701
```

--------------------------------

### Install CRI-O Runtime

Source: https://kubernetes.io/docs/tutorials/cluster-management/_print

Downloads and installs the CRI-O container runtime using a script. It then enables and starts the CRI-O service, followed by a quick check to confirm the service is active.

```bash
curl https://raw.githubusercontent.com/cri-o/packaging/main/get > crio-install
sudo bash crio-install
sudo systemctl daemon-reload
sudo systemctl enable --now crio.service
sudo systemctl is-active crio.service
```

--------------------------------

### Download Kind Configuration

Source: https://kubernetes.io/docs/tutorials/security/_print

This command downloads the example 'kind' configuration file from the specified URL. It requires 'curl' to be installed.

```bash
curl -L -O https://k8s.io/examples/pods/security/seccomp/kind.yaml

```

--------------------------------

### Kubectl Get Examples: Listing and Filtering Resources

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/_print

These examples demonstrate various ways to use the kubectl get command for listing and filtering Kubernetes resources. They cover basic listing, detailed output, specific resource retrieval, and filtering by different criteria.

```bash
# List all pods in ps output format
kubectl get pods

# List all pods in ps output format with more information (such as node name)
kubectl get pods -o wide

# List a single replication controller with specified NAME in ps output format
kubectl get replicationcontroller web

# List deployments in JSON output format, in the "v1" version of the "apps" API group
kubectl get deployments.v1.apps -o json

# List a single pod in JSON output format
kubectl get -o json pod web-pod-13je7

# List a pod identified by type and name specified in "pod.yaml" in JSON output format
kubectl get -f pod.yaml -o json

# List resources from a directory with kustomization.yaml - e.g. dir/kustomization.yaml
kubectl get -k dir/

# Return only the phase value of the specified pod
kubectl get -o template pod/web-pod-13je7 --template={{.status.phase}}

# List resource information in custom columns
kubectl get pod test-pod -o custom-columns=CONTAINER:.spec.containers[0].name,IMAGE:.spec.containers[0].image

# List all replication controllers and services together in ps output format
kubectl get rc,services

# List one or more resources by their type and names
kubectl get rc/web service/frontend pods/web-pod-13je7

# List the 'status' subresource for a single pod
kubectl get pod web-pod-13je7 --subresource status

# List all deployments in namespace 'backend'
kubectl get deployments.apps --namespace backend

# List all pods existing in all namespaces
kubectl get pods --all-namespaces
```

--------------------------------

### Example Docker Compose File

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

This is an example docker-compose.yml file that defines three services: redis-leader, redis-replica, and web. It specifies container images, ports, environment variables, and labels for Kubernetes.

```yaml
services:

  redis-leader:
    container_name: redis-leader
    image: redis
    ports:
      - "6379"

  redis-replica:
    container_name: redis-replica
    image: redis
    ports:
      - "6379"
    command: redis-server --replicaof redis-leader 6379 --dir /tmp

  web:
    container_name: web
    image: quay.io/kompose/web
    ports:
      - "8080:8080"
    environment:
      - GET_HOSTS_FROM=dns
    labels:
      kompose.service.type: LoadBalancer

```

--------------------------------

### Install Kompose from Source using Go

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

Install Kompose by fetching the latest development changes directly from the master branch using `go get`. This method requires Go to be installed on your system and is suitable for users who want the most recent features or to contribute to the project.

```go
go get -u github.com/kubernetes/kompose
```

--------------------------------

### Get Logs for DRA Example Driver DaemonSet

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

This command retrieves logs from all Pods belonging to the 'dra-example-driver' DaemonSet within the 'dra-tutorial' namespace. It's useful for debugging and understanding how the DRA driver handles resource claim preparation and device allocation.

```bash
kubectl logs -l app.kubernetes.io/name=dra-example-driver -n dra-tutorial
```

--------------------------------

### Install Kubernetes Go Client Library

Source: https://kubernetes.io/docs/tasks/access-application-cluster/_print

This command installs the Kubernetes Go client library. Ensure you replace `<kubernetes-version-number>` with the appropriate version. Detailed installation instructions can be found in the `INSTALL.md` file.

```bash
go get k8s.io/client-go@kubernetes-<kubernetes-version-number>
```

--------------------------------

### Kubectl Apply Examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

Illustrative examples of using the 'kubectl apply' command. These examples demonstrate applying configurations from local files, directories (including kustomization), standard input, wildcard file matching, and using the alpha '--prune' flag for resource management.

```bash
# Apply the configuration in pod.json to a pod
kubectl apply -f ./pod.json

# Apply resources from a directory containing kustomization.yaml - e.g. dir/kustomization.yaml
kubectl apply -k dir/

# Apply the JSON passed into stdin to a pod
cat pod.json | kubectl apply -f -

# Apply the configuration from all files that end with '.json'
kubectl apply -f '*.json'

# Note: --prune is still in Alpha
# Apply the configuration in manifest.yaml that matches label app=nginx and delete all other resources that are not in the file and match label app=nginx
kubectl apply --prune -f manifest.yaml -l app=nginx

# Apply the configuration in manifest.yaml and delete all the other config maps that are not in the file
kubectl apply --prune -f manifest.yaml --all --prune-allowlist=core/v1/ConfigMap
```

--------------------------------

### Create and Install a Simple Kubectl Plugin

Source: https://kubernetes.io/docs/reference/kubectl

This example demonstrates how to create a basic kubectl plugin by writing a script, making it executable, and placing it in a directory within your system's PATH. Plugins extend kubectl's functionality, allowing custom commands.

```bash
# Create a simple plugin script
cat ./kubectl-hello

#!/bin/sh

# this plugin prints the words "hello world"
echo "hello world"

# Make the plugin executable
chmod a+x ./kubectl-hello

# Move it to a location in our PATH
sudo mv ./kubectl-hello /usr/local/bin
sudo chown root:root /usr/local/bin

# Invoke the plugin
kubectl hello
```

--------------------------------

### Kubectl Create Deployment Example

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to create a Kubernetes deployment using the kubectl command-line tool. It shows examples for specifying the image, command, replicas, exposed ports, and multiple containers.

```bash
kubectl create deployment my-dep --image=busybox
kubectl create deployment my-dep --image=busybox -- date
kubectl create deployment my-dep --image=nginx --replicas=3
kubectl create deployment my-dep --image=busybox --port=5701
kubectl create deployment my-dep --image=busybox:latest --image=ubuntu:latest --image=nginx
```

--------------------------------

### Example: Generate All Control Plane Pods (kubeadm)

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init-phase

This example demonstrates how to generate all static Pod manifest files for control plane components, which is functionally equivalent to running `kubeadm init`. It shows the basic command usage.

```bash
kubeadm init phase control-plane all
```

--------------------------------

### Kubectl Get Command Examples

Source: https://kubernetes.io/docs/reference/kubectl

Illustrates common uses of the 'kubectl get' command for listing Kubernetes resources. Examples include listing pods, replication controllers, services, daemon sets, and filtering by node or field selectors.

```bash
# List all pods in plain-text
kubectl get pods

# List pods with extra information (-o wide)
kubectl get pods -o wide

# List a specific replication controller
kubectl get replicationcontroller <rc-name>

# List replication controllers and services together
kubectl get rc,services

# List all daemon sets
kubectl get ds

# List pods on a specific node
kubectl get pods --field-selector=spec.nodeName=server01
```

--------------------------------

### Install and Use JavaScript Kubernetes Client

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Installs the JavaScript client for Kubernetes using npm and provides an example of loading kubeconfig and interacting with the Kubernetes API to list pods in the 'default' namespace.

```bash
npm install @kubernetes/client-node
```

```javascript
const k8s = require('@kubernetes/client-node');

const kc = new k8s.KubeConfig();
kc.loadFromDefault();

const k8sApi = kc.makeApiClient(k8s.CoreV1Api);

k8sApi.listNamespacedPod({ namespace: 'default' }).then((res) => {
    console.log(res);
});

```

--------------------------------

### Kubectl Create PriorityClass Examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

Provides practical examples of using the `kubectl create priorityclass` command. These examples demonstrate how to create priority classes with different configurations, including setting a name, value, description, global default status, and preemption policy.

```bash
# Create a priority class named high-prioritykubectl create priorityclass high-priority --value=1000 --description="high priority"
```

```bash
# Create a priority class named default-priority that is considered as the global default prioritykubectl create priorityclass default-priority --value=1000 --global-default=true --description="default priority"
```

```bash
# Create a priority class named high-priority that cannot preempt pods with lower prioritykubectl create priorityclass high-priority --value=1000 --description="high priority" --preemption-policy="Never"
```

--------------------------------

### Configure Startup and Liveness Probes for Slow Starting Containers

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes

This configuration sets up both a startup probe and a liveness probe for a container. The startup probe allows for a longer initial delay (up to 5 minutes in this example) to accommodate slow application initialization. Once the startup probe succeeds, the liveness probe takes over for ongoing health checks.

```yaml
ports:
- name: liveness-port
  containerPort: 8080

livenessProbe:
  httpGet:
    path: /healthz
    port: liveness-port
  failureThreshold: 1
  periodSeconds: 10

startupProbe:
  httpGet:
    path: /healthz
    port: liveness-port
  failureThreshold: 30
  periodSeconds: 10


```

--------------------------------

### Kubectl Create Rolebinding Examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

Examples demonstrating the usage of the 'kubectl create rolebinding' command. These examples illustrate how to create role bindings for different scenarios, including binding users and groups to cluster roles, and service accounts to roles.

```bash
# Create a role binding for user1, user2, and group1 using the admin cluster role
kubectl create rolebinding admin --clusterrole=admin --user=user1 --user=user2 --group=group1
```

```bash
# Create a role binding for service account monitoring:sa-dev using the admin role
kubectl create rolebinding admin-binding --role=admin --serviceaccount=monitoring:sa-dev
```

--------------------------------

### Watch Pod Changes in a Namespace (HTTP Request)

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

This example demonstrates an HTTP GET request to watch for changes (create, delete, patch, update) to pods in a namespace, starting from a specific `resourceVersion`. The response is a stream of JSON documents representing each change.

```http
GET /api/v1/namespaces/test/pods?watch=1&resourceVersion=10245
---
200 OK
Transfer-Encoding: chunked
Content-Type: application/json

{
  "type": "ADDED",
  "object": {"kind": "Pod", "apiVersion": "v1", "metadata": {"resourceVersion": "10596", ...}, ...}
}
{
  "type": "MODIFIED",
  "object": {"kind": "Pod", "apiVersion": "v1", "metadata": {"resourceVersion": "11020", ...}, ...}
}
...
```

--------------------------------

### List Specific Kubernetes Resources by Type and Name with kubectl get

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to list one or more specific Kubernetes resources by providing their type and names. This example lists a replication controller, a service, and a pod.

```bash
# List one or more resources by their type and names
kubectl get rc/web service/frontend pods/web-pod-13je7
```

--------------------------------

### Wait for Service Creation (Shell)

Source: https://kubernetes.io/docs/concepts/workloads/pods/init-containers

This example demonstrates how to use an init container to wait for a Kubernetes service to be available before the main application starts. It uses a simple shell loop with `nslookup` to check for the service's existence.

```shell
for i in {1..100}; do sleep 1; if nslookup myservice; then exit 0; fi; done; exit 1
```

--------------------------------

### Example: Use Minikube Context

Source: https://kubernetes.io/docs/reference/kubectl/_print

An example demonstrating how to use the 'kubectl config use-context' command to switch to the 'minikube' cluster context.

```bash
# Use the context for the minikube cluster
kubectl config use-context minikube
```

--------------------------------

### Example: Generate Pods with Config File (kubeadm)

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init-phase

This example shows how to generate all static Pod manifest files for control plane components using options read from a configuration file. This is useful for managing complex configurations.

```bash
kubeadm init phase control-plane all --config config.yaml
```

--------------------------------

### Kubernetes Repository Configuration Example (RPM)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This is an example of a Kubernetes repository configuration file for RPM-based systems. It defines the repository name, base URL for packages, and GPG key information. The 'exclude' field lists packages that should not be installed from this repository.

```ini
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.34/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.34/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl

```

--------------------------------

### Example Kubernetes PKI File Paths

Source: https://kubernetes.io/docs/setup/best-practices/certificates

This example provides a comprehensive list of all necessary certificate and key file paths for a Kubernetes cluster where all PKI components are self-generated. This is useful for setting up a custom or manually configured cluster.

```bash
/etc/kubernetes/pki/etcd/ca.key
/etc/kubernetes/pki/etcd/ca.crt
/etc/kubernetes/pki/apiserver-etcd-client.key
/etc/kubernetes/pki/apiserver-etcd-client.crt
/etc/kubernetes/pki/ca.key
/etc/kubernetes/pki/ca.crt
/etc/kubernetes/pki/apiserver.key
/etc/kubernetes/pki/apiserver.crt
/etc/kubernetes/pki/apiserver-kubelet-client.key
/etc/kubernetes/pki/apiserver-kubelet-client.crt
/etc/kubernetes/pki/front-proxy-ca.key
/etc/kubernetes/pki/front-proxy-ca.crt
/etc/kubernetes/pki/front-proxy-client.key
/etc/kubernetes/pki/front-proxy-client.crt
/etc/kubernetes/pki/etcd/server.key
/etc/kubernetes/pki/etcd/server.crt
/etc/kubernetes/pki/etcd/peer.key
/etc/kubernetes/pki/etcd/peer.crt
/etc/kubernetes/pki/etcd/healthcheck-client.key
/etc/kubernetes/pki/etcd/healthcheck-client.crt
/etc/kubernetes/pki/sa.key
/etc/kubernetes/pki/sa.pub

```

--------------------------------

### Example: Kubectl Create Job

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to create a basic Kubernetes job using the 'kubectl create job' command with a specified image.

```bash
# Create a job
kubectl create job my-job --image=busybox
```

--------------------------------

### Start a Minikube Cluster

Source: https://kubernetes.io/docs/tutorials/_print

This command initiates a local Kubernetes cluster using Minikube. Ensure Minikube is installed before running this command. It sets up all necessary components for a local Kubernetes environment.

```bash
minikube start

```

--------------------------------

### Install Kubeadm and Kubelet on Windows

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Downloads and installs kubeadm and kubelet on a Windows machine, preparing it to join a Kubernetes cluster. The `KubernetesVersion` parameter should be adjusted as needed.

```powershell
curl.exe -LO https://raw.githubusercontent.com/kubernetes-sigs/sig-windows-tools/master/hostprocess/PrepareNode.ps1
./PrepareNode.ps1 -KubernetesVersion v1.35.0
```

--------------------------------

### List Multiple Kubernetes Resource Types with kubectl get

Source: https://kubernetes.io/docs/reference/kubectl/_print

Shows how to list multiple types of Kubernetes resources in a single command. This example lists replication controllers and services together.

```bash
# List all replication controllers and services together in ps output format
kubectl get rc,services
```

--------------------------------

### Download and Install kubeadm, kubelet, and Configure Systemd Service

Source: https://kubernetes.io/docs/setup/production-environment/_print

This snippet downloads the latest stable release of `kubeadm` and `kubelet` binaries, makes them executable, and then sets up the `kubelet` systemd service and configuration files by fetching templates from a GitHub repository. It dynamically determines the release version and architecture.

```bash
RELEASE="$(curl -sSL https://dl.k8s.io/release/stable.txt)"
ARCH="amd64"
cd $DOWNLOAD_DIR
sudo curl -L --remote-name-all https://dl.k8s.io/release/${RELEASE}/bin/linux/${ARCH}/{kubeadm,kubelet}
sudo chmod +x {kubeadm,kubelet}

RELEASE_VERSION="v0.16.2"
curl -sSL "https://raw.githubusercontent.com/kubernetes/release/${RELEASE_VERSION}/cmd/krel/templates/latest/kubelet/kubelet.service" | sed "s:/usr/bin:${DOWNLOAD_DIR}:g" | sudo tee /usr/lib/systemd/system/kubelet.service
sudo mkdir -p /usr/lib/systemd/system/kubelet.service.d
curl -sSL "https://raw.githubusercontent.com/kubernetes/release/${RELEASE_VERSION}/cmd/krel/templates/latest/kubeadm/10-kubeadm.conf" | sed "s:/usr/bin:${DOWNLOAD_DIR}:g" | sudo tee /usr/lib/systemd/system/kubelet.service.d/10-kubeadm.conf

# Optionally, enable the kubelet service before running kubeadm:
sudo systemctl enable --now kubelet
```

--------------------------------

### Example: Kubectl Create Job with Command

Source: https://kubernetes.io/docs/reference/kubectl/_print

Illustrates creating a Kubernetes job that executes a specific command and arguments upon creation.

```bash
# Create a job with a command
kubectl create job my-job --image=busybox -- date
```

--------------------------------

### Install and Configure containerd on Windows

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

These PowerShell commands outline the process for downloading, extracting, configuring, and starting containerd on a Windows system. It includes steps for setting the version, copying binaries, generating the configuration file, and registering containerd as a service. It also includes an optional step to exclude containerd from Windows Defender scans.

```powershell
# Set the desired containerd version
$Version="1.4.3"

# Download containerd
curl.exe -L https://github.com/containerd/containerd/releases/download/v$Version/containerd-$Version-windows-amd64.tar.gz -o containerd-windows-amd64.tar.gz
tar.exe xvf .\containerd-windows-amd64.tar.gz

# Extract and configure
Copy-Item -Path ".\bin\" -Destination "$Env:ProgramFiles\containerd" -Recurse -Force
cd $Env:ProgramFiles\containerd\
.\containerd.exe config default | Out-File config.toml -Encoding ascii

# Review the configuration. Depending on setup you may want to adjust:
# - the sandbox_image (Kubernetes pause image)
# - cni bin_dir and conf_dir locations
Get-Content config.toml

# (Optional - but highly recommended) Exclude containerd from Windows Defender Scans
Add-MpPreference -ExclusionProcess "$Env:ProgramFiles\containerd\containerd.exe"

# Start containerd
.\containerd.exe --register-service
Start-Service containerd

```

--------------------------------

### Get LeaseCandidate HTTP Request

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/_print

Example HTTP GET request to retrieve a specific LeaseCandidate by its name and namespace in Kubernetes v1beta1.

```http
GET /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name} HTTP/1.1
Host: api.kubernetes.example.com
Accept: application/json

```

--------------------------------

### Systemd Kubelet Drop-in Configuration Example

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/kubelet-integration

This example shows the content of a typical systemd drop-in configuration file for the Kubelet service, installed by the kubeadm package. It sets environment variables for Kubelet configuration arguments.

```ini
[Service]
Environment="KUBELET_KUBECONFIG_ARGS=--bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf"
Environment="KUBELET_CONFIG_ARGS=--config=/var/lib/kubelet/config.yaml"
EnvironmentFile=-/var/lib/kubelet/kubeadm-flags.env

```

--------------------------------

### Example: Create Pod Disruption Budget (Percentage)

Source: https://kubernetes.io/docs/reference/kubectl/_print

Example of creating a Pod Disruption Budget named 'my-pdb' that targets pods with the label 'app=nginx' and ensures at least 50% of the selected pods remain available.

```bash
kubectl create pdb my-pdb --selector=app=nginx --min-available=50%
```

--------------------------------

### Install kubectl Powershell Completion

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Guides users on installing powershell completion for kubectl. It covers loading completion into the current shell and configuring it to run on startup.

```powershell
# Load the kubectl completion code for powershell into the current shell
kubectl completion powershell | Out-String | Invoke-Expression
# Set kubectl completion code for powershell to run on startup
## Save completion code to a script and execute in the profile
kubectl completion powershell > "$HOME\.kube\completion.ps1"
Add-Content $PROFILE ". '$HOME\.kube\completion.ps1'"
## Execute completion code in the profile
Add-Content $PROFILE "if (Get-Command kubectl -ErrorAction SilentlyContinue) {
kubectl completion powershell | Out-String | Invoke-Expression
}"
## Add completion code directly to the $PROFILE script
kubectl completion powershell >> $PROFILE
```

--------------------------------

### Kubelet Systemd Drop-in Configuration Example

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

This example shows the contents of a typical kubelet systemd drop-in file (`10-kubeadm.conf`). It defines environment variables for kubelet configuration, including paths to bootstrap and main kubeconfig files, and allows for dynamic arguments from an environment file.

```ini
[Service]
Environment="KUBELET_KUBECONFIG_ARGS=--bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf"
Environment="KUBELET_CONFIG_ARGS=--config=/var/lib/kubelet/config.yaml"
# This is a file that "kubeadm init" and "kubeadm join" generate at runtime, populating
# the KUBELET_KUBEADM_ARGS variable dynamically
EnvironmentFile=-/var/lib/kubelet/kubeadm-flags.env
# This is a file that the user can use for overrides of the kubelet args as a last resort. Preferably,
# the user should use the .NodeRegistration.KubeletExtraArgs object in the configuration files instead.

```

--------------------------------

### List Kubernetes Pods with kubectl get

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates basic commands to list pods in different output formats. Shows how to get a simple list, a wide list with more information, and how to specify a single replication controller.

```bash
# List all pods in ps output format
kubectl get pods

# List all pods in ps output format with more information (such as node name)
kubectl get pods -o wide

# List a single replication controller with specified NAME in ps output format
kubectl get replicationcontroller web
```

--------------------------------

### Install OpenAPI Go Packages

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/_print

These go get commands install necessary Go packages from the go-openapi project, which are required for loading and processing OpenAPI specifications.

```shell
go get -u github.com/go-openapi/loads
go get -u github.com/go-openapi/spec

```

--------------------------------

### Start Minikube with Increased Resources

Source: https://kubernetes.io/docs/tutorials/_print

This command starts a Minikube instance with increased memory and CPU resources. It is recommended for tutorials that require more resources than Minikube's default configuration to avoid errors.

```bash
minikube start --memory 5120 --cpus=4
```

--------------------------------

### Kubernetes SubjectAccessReview Example

Source: https://kubernetes.io/docs/concepts/security/controlling-access

An example of a SubjectAccessReview request in Kubernetes. This demonstrates how to check if a user is authorized to perform a specific action on a resource. This specific example checks if 'bob' can 'get' pods in the 'projectCaribou' namespace.

```json
{
  "apiVersion": "authorization.k8s.io/v1beta1",
  "kind": "SubjectAccessReview",
  "spec": {
    "resourceAttributes": {
      "namespace": "projectCaribou",
      "verb": "get",
      "group": "unicorn.example.org",
      "resource": "pods"
    }
  }
}

```

--------------------------------

### ip-masq-agent Configuration Example (JSON)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

An example configuration file for the ip-masq-agent using JSON syntax. It shows how to define non-masquerade CIDR ranges, control masquerading of link-local traffic, and set the interval for configuration reloads.

```json
{
  "nonMasqueradeCIDRs": [
    "10.0.0.0/8",
    "172.16.0.0/12",
    "192.168.0.0/16",
    "169.254.0.0/16"
  ],
  "masqLinkLocal": false,
  "resyncInterval": "60s"
}

```

--------------------------------

### Kubernetes CronJob API Request (HTTP GET)

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/cron-job-v1

Example of an HTTP GET request to retrieve a specific CronJob resource from a Kubernetes cluster.

```http
GET /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}
```

--------------------------------

### ip-masq-agent Configuration Example (YAML)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

An example configuration file for the ip-masq-agent using YAML syntax. It demonstrates how to specify non-masquerade CIDR ranges, whether to masquerade link-local traffic, and the resync interval for configuration reloads.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: ip-masq-agent
data:
  config:
    "nonMasqueradeCIDRs":
      - "10.0.0.0/8"
      - "172.16.0.0/12"
      - "192.168.0.0/16"
      - "169.254.0.0/16"
    "masqLinkLocal": false
    "resyncInterval": "60s"

```

--------------------------------

### Example: List All Contexts

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example demonstrates how to list all available contexts defined in the kubeconfig file using the 'kubectl config get-contexts' command.

```bash
kubectl config get-contexts
```

--------------------------------

### Kubernetes Namespace API - Get Request Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

This snippet demonstrates how to make an HTTP GET request to retrieve a specific Kubernetes namespace by its name. It includes path and query parameters.

```http
GET /api/v1/namespaces/{name}?pretty=true HTTP/1.1
Host: kubernetes.default.svc
```

--------------------------------

### Kubernetes API Request: Get IngressClass (Shell)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Example of how to retrieve a specific IngressClass resource using the Kubernetes API via a GET request. This command targets the IngressClass by its name.

```shell
curl -X GET \
  http://localhost:8080/apis/networking.k8s.io/v1/ingressclasses/{name} \
  -H 'Accept: application/json'
```

--------------------------------

### Get Detailed kubectl Client Version

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Retrieves a detailed, YAML-formatted output of the installed kubectl client version. This provides more comprehensive information than the basic version check.

```bash
kubectl version --client --output=yaml
```

--------------------------------

### Download Example Pod Manifest

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Download the example Pod manifest file from the provided URL. This file can then be modified with your private image details and used to create the Pod.

```bash
curl -L -o my-private-reg-pod.yaml https://k8s.io/examples/pods/private-reg-pod.yaml
```

--------------------------------

### Kubernetes Apiserver Validation Error Example

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods

An example of an error message from the Kubernetes apiserver when a pod description contains an unknown field, such as a misspelling of 'command'.

```text
I0805 10:43:25.129850   46757 schema.go:126] unknown field: commnd
I0805 10:43:25.129973   46757 schema.go:129] this may be a false alarm, see https://github.com/kubernetes/kubernetes/issues/6842
pods/mypod

```

--------------------------------

### Delay Application Start (Shell)

Source: https://kubernetes.io/docs/concepts/workloads/pods/_print

A simple init container example that introduces a delay before the main application container starts. This is achieved using the 'sleep' command for a specified duration.

```shell
sleep 60
```

--------------------------------

### Resource Rules Example (Kubernetes Admission)

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/mutating-admission-policy-binding-v1alpha1

Illustrates the structure of `resourceRules` for defining which operations on which resources an admission policy should match. It includes examples for specifying API groups, versions, operations, and resources.

```yaml
resourceRules: |
  - apiGroups: ["apps"]
    apiVersions: ["v1"]
    operations: ["UPDATE"]
    resources: ["deployments", "deployments/scale"]
    scope: "Namespaced"
```

```yaml
resourceRules: |
  - apiGroups: ["*"]
    apiVersions: ["*"]
    operations: ["*"]
    resources: ["*"]
    scope: "*"
```

--------------------------------

### Install kubectl using Snap

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

This command installs kubectl as a snap application, which is a universal package format for Linux. The `--classic` flag is required for kubectl as it needs broader system access. After installation, `kubectl version --client` verifies the installation.

```bash
snap install kubectl --classic
kubectl version --client
```

--------------------------------

### List Pods in a Namespace (HTTP Request)

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

This example shows an HTTP GET request to list all pods in a specific namespace. The response includes a `resourceVersion` which can be used to initiate a watch.

```http
GET /api/v1/namespaces/test/pods
---
200 OK
Content-Type: application/json

{
  "kind": "PodList",
  "apiVersion": "v1",
  "metadata": {"resourceVersion":"10245"},
  "items": [...] 
}
```

--------------------------------

### Delay Application Start (Shell)

Source: https://kubernetes.io/docs/concepts/workloads/pods/init-containers

A straightforward example of an init container used to introduce a delay before the main application container begins execution. This can be useful for various synchronization or readiness checks.

```shell
sleep 60
```

--------------------------------

### Hugo Headless Page Bundle Example

Source: https://kubernetes.io/docs/contribute/_print

This example demonstrates a Hugo 'headless' Page Bundle, indicated by `headless: true` in its front matter. Such bundles do not get their own URL and are intended for use within other pages.

```filetree
en/includes
├── default-storage-class-prereqs.md
├── index.md
├── partner-script.js
├── partner-style.css
├── task-tutorial-prereqs.md
├── user-guide-content-moved.md
└── user-guide-migration-notice.md

```

--------------------------------

### Kubectl Rollout Status Example

Source: https://kubernetes.io/docs/reference/kubectl/_print

Provides an example of how to use the 'kubectl rollout status' command to watch the rollout status of a deployment named 'nginx'.

```bash
# Watch the rollout status of a deployment
kubectl rollout status deployment/nginx
```

--------------------------------

### List Service Output Example (kubectl)

Source: https://kubernetes.io/docs/tasks/network/_print

Example output from `kubectl get svc` for a dual-stack service, showing only the primary IPv4 cluster IP in the `CLUSTER-IP` column.

```text
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
my-service   ClusterIP   10.0.216.242   <none>        80/TCP    5s

```

--------------------------------

### Start a basic Nginx pod using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts a simple pod running the nginx image. It's a fundamental way to deploy a containerized application.

```bash
kubectl run nginx --image=nginx
```

--------------------------------

### Kubectl API Resources Examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

Illustrative examples of using the 'kubectl api-resources' command with different flags to filter and display API resources. These examples demonstrate common use cases such as showing wide output, sorting, filtering by namespace, and filtering by API group.

```bash
# Print the supported API resourceskubectl api-resources

```

```bash
# Print the supported API resources with more information
kubectl api-resources -o wide

```

```bash
# Print the supported API resources sorted by a column
kubectl api-resources --sort-by=name

```

```bash
# Print the supported namespaced resources
kubectl api-resources --namespaced=true

```

```bash
# Print the supported non-namespaced resources
kubectl api-resources --namespaced=false

```

```bash
# Print the supported API resources with a specific APIGroup
kubectl api-resources --api-group=rbac.authorization.k8s.io

```

--------------------------------

### Kubectl Attach Command Examples

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

Demonstrates various ways to use the 'kubectl attach' command to get output from pods and containers, including interactive terminal mode and targeting specific containers or replica sets.

```bash
kubectl attach mypod

```

```bash
kubectl attach mypod -c ruby-container

```

```bash
kubectl attach mypod -c ruby-container -i -t

```

```bash
kubectl attach rs/nginx

```

--------------------------------

### Create Kubernetes Role with SubResource Specification

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This example shows how to create a role that includes permissions for subresources. The role 'foo' can perform 'get', 'list', and 'watch' operations on both 'pods' and their 'status' subresource.

```bash
kubectl create role foo --verb=get,list,watch --resource=pods,pods/status
```

--------------------------------

### Example: Create Pod Disruption Budget (Absolute)

Source: https://kubernetes.io/docs/reference/kubectl/_print

Example of creating a Pod Disruption Budget named 'my-pdb' that targets pods with the label 'app=rails' and ensures at least 1 pod remains available.

```bash
kubectl create poddisruptionbudget my-pdb --selector=app=rails --min-available=1
```

--------------------------------

### Kubectl Kustomize Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Examples demonstrating how to use the `kubectl kustomize` command to build KRM resources from different sources.

```bash
# Build the current working directorykubectl kustomize

# Build some shared configuration directorykubectl kustomize /home/config/production

# Build from github
kubectl kustomize https://github.com/kubernetes-sigs/kustomize.git/examples/helloWorld?ref=v1.0.6
```

--------------------------------

### Enable Kubelet Service

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Enables and starts the `kubelet` service. This is an optional step that can be performed before running `kubeadm` to ensure the Kubelet is running and ready to manage pods.

```shell
sudo systemctl enable --now kubelet
```

--------------------------------

### Create and Debug a Pod with Sysadmin Profile

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod

This snippet demonstrates how to create a sample pod, then debug it using an ephemeral container with the 'sysadmin' profile for elevated privileges. It also shows how to verify the applied capabilities and clean up the pod.

```bash
kubectl run myapp --image=busybox:1.28 --restart=Never -- sleep 1d
kubectl debug -it myapp --image=busybox:1.28 --target=myapp --profile=sysadmin
/ # grep Cap /proc/$$/status
kubectl get pod myapp -o jsonpath='{.spec.ephemeralContainers[0].securityContext}'
kubectl delete pod myapp
```

--------------------------------

### ValidatingAdmissionPolicy Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example demonstrates a ValidatingAdmissionPolicy that enforces image naming conventions based on namespace labels. It checks if container images contain 'example.com' and ensures they start with the environment label defined in the namespace.

```APIDOC
## ValidatingAdmissionPolicy: image-matches-namespace-environment.policy.example.com

### Description
This policy validates that container images within Deployments adhere to a naming convention based on the namespace's environment label. It allows for an 'exempt' label to bypass validation.

### Method
N/A (This is a Kubernetes resource definition, not a direct API endpoint call)

### Endpoint
N/A

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
This section describes the structure of the `ValidatingAdmissionPolicy` resource.

- **apiVersion** (string) - Required - Specifies the Kubernetes API version.
- **kind** (string) - Required - Must be 'ValidatingAdmissionPolicy'.
- **metadata** (object) - Required - Contains metadata for the policy.
  - **name** (string) - Required - The name of the policy.
- **spec** (object) - Required - The specification for the admission policy.
  - **failurePolicy** (string) - Required - Defines the behavior on failure ('Fail' or 'Ignore').
  - **matchConstraints** (object) - Required - Defines the resources the policy applies to.
    - **resourceRules** (array) - Required - A list of resource rules.
      - **apiGroups** (array of strings) - Required - API groups to match.
      - **apiVersions** (array of strings) - Required - API versions to match.
      - **operations** (array of strings) - Required - Operations to match (e.g., 'CREATE', 'UPDATE').
      - **resources** (array of strings) - Required - Resources to match (e.g., 'deployments').
  - **variables** (array) - Optional - Defines variables used in expressions.
    - **name** (string) - Required - The name of the variable.
    - **expression** (string) - Required - The CEL expression to evaluate the variable.
  - **validations** (array) - Required - The validation rules.
    - **expression** (string) - Required - The CEL expression for the validation.
    - **messageExpression** (string) - Optional - An expression to generate a custom error message.

### Request Example
```json
{
  "apiVersion": "admissionregistration.k8s.io/v1",
  "kind": "ValidatingAdmissionPolicy",
  "metadata": {
    "name": "image-matches-namespace-environment.policy.example.com"
  },
  "spec": {
    "failurePolicy": "Fail",
    "matchConstraints": {
      "resourceRules": [
        {
          "apiGroups": ["apps"],
          "apiVersions": ["v1"],
          "operations": ["CREATE", "UPDATE"],
          "resources": ["deployments"]
        }
      ]
    },
    "variables": [
      {
        "name": "environment",
        "expression": "'environment' in namespaceObject.metadata.labels ? namespaceObject.metadata.labels['environment'] : 'prod'"
      },
      {
        "name": "exempt",
        "expression": "'exempt' in object.metadata.labels && object.metadata.labels['exempt'] == 'true'"
      },
      {
        "name": "containers",
        "expression": "object.spec.template.spec.containers"
      },
      {
        "name": "containersToCheck",
        "expression": "variables.containers.filter(c, c.image.contains('example.com/'))"
      }
    ],
    "validations": [
      {
        "expression": "variables.exempt || variables.containersToCheck.all(c, c.image.startsWith(variables.environment + '.'))",
        "messageExpression": "'only ' + variables.environment + ' images are allowed in namespace ' + namespaceObject.metadata.name"
      }
    ]
  }
}
```

### Response
N/A (This is a resource definition, not an API call that returns a response in the traditional sense. Admission control decisions are made by the Kubernetes API server.)

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### List LeaseCandidates HTTP Request

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/_print

Example HTTP GET request to list all LeaseCandidates within a specific namespace in Kubernetes v1beta1.

```http
GET /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates HTTP/1.1
Host: api.kubernetes.example.com
Accept: application/json

```

--------------------------------

### Kubectl Create RoleBinding Examples

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

These examples demonstrate how to create RoleBindings to grant roles within a specific namespace. RoleBindings link a role (or cluster role) to users, groups, or service accounts within a defined scope.

```bash
kubectl create rolebinding bob-admin-binding --clusterrole=admin --user=bob --namespace=acme
```

```bash
kubectl create rolebinding myapp-view-binding --clusterrole=view --serviceaccount=acme:myapp --namespace=acme
```

```bash
kubectl create rolebinding myappnamespace-myapp-view-binding --clusterrole=view --serviceaccount=myappnamespace:myapp --namespace=acme
```

```bash
kubectl create rolebinding my-sa-view \
  --clusterrole=view \
  --serviceaccount=my-namespace:my-sa \
  --namespace=my-namespace
```

```bash
kubectl create rolebinding default-view \
  --clusterrole=view \
  --serviceaccount=my-namespace:default \
  --namespace=my-namespace
```

--------------------------------

### Kubernetes RBAC RoleBinding GET API Request

Source: https://kubernetes.io/docs/reference/kubernetes-api/authorization-resources/role-binding-v1

Example HTTP GET request to retrieve a specific RoleBinding by name and namespace. This operation is used to read the details of a single RoleBinding resource.

```http
GET /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name}
```

--------------------------------

### Kubernetes Versioning in Documentation

Source: https://kubernetes.io/docs/contribute/_print

Illustrates how to specify Kubernetes versioning for examples using front matter in Markdown files. It also shows how to avoid version-specific comments within code examples.

```yaml
---
title: <your tutorial title here>
min-kubernetes-server-version: v1.8
---

```

```yaml
apiVersion: v1
kind: Pod
...
```

--------------------------------

### Start Minikube with Increased Resources

Source: https://kubernetes.io/docs/tutorials/stateful-application/cassandra

This command starts the Minikube environment with increased memory and CPU resources, which are necessary to avoid resource allocation errors during the Cassandra deployment tutorial.

```bash
minikube start --memory 5120 --cpus=4

```

--------------------------------

### Kubectl Apply: Creating Resources from Files and URLs

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to create Kubernetes resources using `kubectl apply` from various sources including local YAML/JSON files, multiple files, directories, and URLs. This is the recommended method for managing applications in production.

```bash
kubectl apply -f ./my-manifest.yaml                 # create resource(s)
kubectl apply -f ./my1.yaml -f ./my2.yaml           # create from multiple files
kubectl apply -f ./dir                              # create resource(s) in all manifest files in dir
kubectl apply -f https://example.com/manifest.yaml  # create resource(s) from url (Note: this is an example domain and does not contain a valid manifest)
kubectl create deployment nginx --image=nginx       # start a single instance of nginx
kubectl create job hello --image=busybox:1.28 -- echo "Hello World"
kubectl create cronjob hello --image=busybox:1.28   --schedule="*/1 * * * *" -- echo "Hello World"
kubectl explain pods                           # get the documentation for pod manifests
```

--------------------------------

### Get product_uuid using sysfs

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

This command reads the system's product UUID from the sysfs filesystem. It's essential for ensuring each node in a Kubernetes cluster has a unique identifier, preventing installation failures.

```shell
sudo cat /sys/class/dmi/id/product_uuid

```

--------------------------------

### Install kubectl Convert Plugin for Windows

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows

Provides steps to download, validate, and install the kubectl convert plugin on Windows. It includes commands for downloading the binary and checksum, validating the binary using Command Prompt and PowerShell, and cleaning up installation files.

```powershell
curl.exe -LO "https://dl.k8s.io/release/v1.35.0/bin/windows/amd64/kubectl-convert.exe"
```

```powershell
curl.exe -LO "https://dl.k8s.io/v1.35.0/bin/windows/amd64/kubectl-convert.exe.sha256"
```

```powershell
CertUtil -hashfile kubectl-convert.exe SHA256
type kubectl-convert.exe.sha256
```

```powershell
$($(CertUtil -hashfile .\kubectl-convert.exe SHA256)[1] -replace " ", "") -eq $(type .\kubectl-convert.exe.sha256)
```

```powershell
del kubectl-convert.exe
del kubectl-convert.exe.sha256
```

--------------------------------

### Kubernetes ControllerRevision API - Get Operation (kubectl)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Example kubectl command to retrieve a specific ControllerRevision by its name and namespace.

```bash
kubectl get controllerrevision <name> -n <namespace>
```

--------------------------------

### Make Kubelet Executable and Copy to Bin

Source: https://kubernetes.io/docs/tutorials/_print

These commands make the downloaded Kubelet binary executable and then copy it to the system's binary directory, making it available system-wide.

```bash
chmod +x kubelet
sudo cp kubelet /usr/bin/

```

--------------------------------

### Get Shell to a Specific Container in a Multi-Container Pod

Source: https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container

When a Pod contains multiple containers, this command uses the `--container` (or `-c`) flag to specify which container to execute commands within. This example shows how to get a shell to the 'main-app' container in a Pod named 'my-pod'.

```bash
kubectl exec -i -t my-pod --container main-app -- /bin/bash

```

--------------------------------

### Initialize Kubeadm with Configuration

Source: https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/_print

Initializes a Kubernetes cluster using a specified configuration file, which can include Kubelet settings like the cgroup driver.

```bash
kubeadm init --config kubeadm-config.yaml
```

--------------------------------

### API Response Compression Verification

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

This example demonstrates how to verify if API response compression is enabled and working by sending a GET request with the 'Accept-Encoding' header and checking the 'content-encoding' response header.

```APIDOC
## GET /api/v1/pods

### Description
This endpoint retrieves a list of pods. When API response compression is enabled, the response can be compressed using gzip if the client requests it via the 'Accept-Encoding' header.

### Method
GET

### Endpoint
/api/v1/pods

### Query Parameters
* **Accept-Encoding** (string) - Required - Specifies the compression algorithms the client supports. Use 'gzip' to request compressed responses.

### Response
#### Success Response (200)
- **content-encoding** (string) - Indicates the compression method used for the response. If compression is active, this will typically be 'gzip'.

### Request Example
```http
GET /api/v1/pods HTTP/1.1
Host: <your-api-server-host>
Accept-Encoding: gzip
```

### Response Example
```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Encoding: gzip

[... compressed JSON response body ...]
```
```

--------------------------------

### Parameter Resource Example (ReplicaLimit)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example shows a custom resource definition for a parameter, `ReplicaLimit`. This resource holds the actual configuration values, such as `maxReplicas`, that are referenced by the ValidatingAdmissionPolicy.

```APIDOC
## POST /apis/rules.example.com/v1/replicallimits

### Description
Creates a custom parameter resource (e.g., ReplicaLimit) that holds configuration values for a ValidatingAdmissionPolicy.

### Method
POST

### Endpoint
/apis/rules.example.com/v1/replicallimits

### Parameters
#### Request Body
- **apiVersion** (string) - Required - Specifies the API version for the parameter resource (e.g., 'rules.example.com/v1').
- **kind** (string) - Required - Specifies the resource kind (e.g., 'ReplicaLimit').
- **metadata** (object) - Required - Contains metadata for the parameter resource, including its name.
  - **name** (string) - Required - The name of the parameter resource.
  - **namespace** (string) - Optional - The namespace of the parameter resource.
- **maxReplicas** (integer) - Required - The maximum number of replicas allowed, as defined by the policy.

### Request Example
```yaml
apiVersion: rules.example.com/v1
kind: ReplicaLimit
metadata:
  name: "replica-limit-test.example.com"
  namespace: "default"
maxReplicas: 3
```

### Response
#### Success Response (200 or 201)
- **metadata** (object) - Metadata of the created parameter resource.
- **maxReplicas** (integer) - The configured maximum replicas.

#### Response Example
```json
{
  "apiVersion": "rules.example.com/v1",
  "kind": "ReplicaLimit",
  "metadata": {
    "name": "replica-limit-test.example.com",
    "namespace": "default",
    "creationTimestamp": "2023-10-27T10:10:00Z"
  },
  "maxReplicas": 3
}
```
```

--------------------------------

### Kubeadm InitConfiguration Example

Source: https://kubernetes.io/docs/reference/config-api/_print

Defines runtime settings for `kubeadm init`, including bootstrap tokens, node registration details, and API server endpoint configuration. This is essential for initializing a Kubernetes node.

```yaml
apiVersion: kubeadm.k8s.io/v1beta3
kind: InitConfiguration
bootstrapTokens:
  - token: "9a08jv.c0izixklcxtmnze7"
    description: "kubeadm bootstrap token"
    ttl: "24h"
  - token: "783bde.3f89s0fje9f38fhf"
    description: "another bootstrap token"
    usages:
      - authentication
      - signing
    groups:
      - system:bootstrappers:kubeadm:default-node-token
nodeRegistration:
  name: "ec2-10-100-0-1"
  criSocket: "/var/run/dockershim.sock"
  taints:
    - key: "kubeadmNode"
      value: "someValue"
      effect: "NoSchedule"
  kubeletExtraArgs:
    v: 4
  ignorePreflightErrors:
    - IsPrivilegedUser
  imagePullPolicy: "IfNotPresent"
localAPIEndpoint:
  advertiseAddress: "10.100.0.1"
  bindPort: 6443
certificateKey: "e6a2eb8581237ab72a4f494f30285ec12a9694d750b9785706a83bfcbbbd2204"
skipPhases:
  - addon/kube-proxy

```

--------------------------------

### Programmatic Access with Go Client Library

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Instructions on how to install and use the official Go client library (`client-go`) for programmatic access to the Kubernetes API.

```APIDOC
## Programmatic Access with Go Client Library

### Description
This section details how to use the official Go client library (`k8s.io/client-go`) to programmatically interact with the Kubernetes API. It covers installation and provides a general guideline for application development.

### Method
N/A (Programmatic)

### Endpoint
N/A (Client library abstracts API endpoints)

### Parameters
N/A

### Request Example
```bash
# Get the client-go library for a specific Kubernetes version
go get k8s.io/client-go@kubernetes-<kubernetes-version-number>

# Example of writing an application using client-go:
# (Refer to client-go documentation for specific code examples)
```

### Response
N/A (Application-specific)

### Notes
- Replace `<kubernetes-version-number>` with the desired Kubernetes version.
- Refer to the `client-go` releases page (https://github.com/kubernetes/client-go/releases) to find supported versions.
- The Go client library handles authentication based on the configuration found in `~/.kube/config` or environment variables.
```

--------------------------------

### Enable and Start Kubelet Service

Source: https://kubernetes.io/docs/tutorials/_print

These commands reload the systemd daemon to recognize the new service file and then enable and start the Kubelet service. This ensures Kubelet starts automatically on boot.

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now kubelet.service

```

--------------------------------

### Set Up Local Workspace and GOPATH

Source: https://kubernetes.io/docs/contribute/_print

Creates a directory for your local workspace and sets the GOPATH environment variable. This is a prerequisite for cloning and managing Go projects.

```shell
mkdir -p $HOME/<workspace>

export GOPATH=$HOME/<workspace>

```

--------------------------------

### Install kubeadm and kubelet Binaries and Configure Kubelet Service

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

Installs the kubeadm and kubelet binaries by downloading them for the latest stable release and specified architecture. It also configures the kubelet systemd service and its associated configuration file by fetching templates and adjusting paths.

```bash
RELEASE="$(curl -sSL https://dl.k8s.io/release/stable.txt)"
ARCH="amd64"
cd $DOWNLOAD_DIR
sudo curl -L --remote-name-all https://dl.k8s.io/release/${RELEASE}/bin/linux/${ARCH}/{kubeadm,kubelet}
sudo chmod +x {kubeadm,kubelet}

RELEASE_VERSION="v0.16.2"
curl -sSL "https://raw.githubusercontent.com/kubernetes/release/${RELEASE_VERSION}/cmd/krel/templates/latest/kubelet/kubelet.service" | sed "s:/usr/bin:${DOWNLOAD_DIR}:g" | sudo tee /usr/lib/systemd/system/kubelet.service
sudo mkdir -p /usr/lib/systemd/system/kubelet.service.d
curl -sSL "https://raw.githubusercontent.com/kubernetes/release/${RELEASE_VERSION}/cmd/krel/templates/latest/kubeadm/10-kubeadm.conf" | sed "s:/usr/bin:${DOWNLOAD_DIR}:g" | sudo tee /usr/lib/systemd/system/kubelet.service.d/10-kubeadm.conf
```

--------------------------------

### Kubeadm Init Success Output and Cluster Setup

Source: https://kubernetes.io/docs/setup/_print

This snippet shows the expected output after a successful `kubeadm init` command, including instructions for setting up kubectl for regular users and the command to join new nodes to the cluster. It highlights the importance of the join command's token and hash.

```bash
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a Pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  /docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash> 

```

--------------------------------

### Requesting Table Format for Pods (HTTP)

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

This example demonstrates how to request a list of pods in the Table format using an HTTP GET request. It specifies the desired content type in the Accept header.

```http
GET /api/v1/pods
Accept: application/json;as=Table;g=meta.k8s.io;v=v1
---
200 OK
Content-Type: application/json

{
    "kind": "Table",
    "apiVersion": "meta.k8s.io/v1",
    ...
    "columnDefinitions": [
        ...
    ]
}
```

--------------------------------

### GET /flagz (Plain Text)

Source: https://kubernetes.io/docs/reference/instrumentation/zpages

Retrieves the command-line arguments used to start a component in a plain text format. This format is intended for debugging and has no compatibility guarantees.

```APIDOC
## GET /flagz (Plain Text)

### Description
Retrieves the command-line arguments used to start a component in a plain text format. This format is intended for debugging and has no compatibility guarantees.

### Method
GET

### Endpoint
/flagz

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **Output** (string) - Plain text output of component flags.

#### Response Example
```
kube-apiserver flags
Warning: This endpoint is not meant to be machine parseable, has no formatting compatibility guarantees and is for debugging purposes only.

advertise-address=192.168.8.2
contention-profiling=false
enable-priority-and-fairness=true
profiling=true
authorization-mode=[Node,RBAC]
authorization-webhook-cache-authorized-ttl=5m0s
authorization-webhook-cache-unauthorized-ttl=30s
authorization-webhook-version=v1beta1
default-watch-cache-size=100
```
```

--------------------------------

### Kubernetes ControllerRevision API - Get Operation (HTTP)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Example HTTP request to retrieve a specific ControllerRevision by its name and namespace. Requires authentication.

```http
GET /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name} HTTP/1.1
Host: your-kubernetes-api-host
Authorization: Bearer <your-token>
```

--------------------------------

### Get IngressClass HTTP Request (Example)

Source: https://kubernetes.io/docs/reference/kubernetes-api/service-resources/ingress-class-v1

Shows how to retrieve a specific IngressClass resource using an HTTP GET request. It requires the name of the IngressClass in the path and supports an optional 'pretty' query parameter for formatted output.

```http
GET /apis/networking.k8s.io/v1/ingressclasses/{name}
Host: localhost
```

--------------------------------

### Example Kubelet Systemd Service Unit Configuration

Source: https://kubernetes.io/docs/reference/node/systemd-watchdog

This is a comprehensive example of a kubelet systemd service unit file. It includes the `[Unit]`, `[Service]`, and `[Install]` sections. Notably, it configures the `WatchdogSec` to `30s` for a 30-second watchdog timeout and sets `Restart=on-failure` to ensure automatic restarts. `StartLimitInterval=0` and `RestartSec=10` are also included for restart behavior.

```systemd unit file
[Unit]
Description=kubelet: The Kubernetes Node Agent
Documentation=https://kubernetes.io/docs/home/
Wants=network-online.target
After=network-online.target

[Service]
ExecStart=/usr/bin/kubelet
# Configures the watchdog timeout
WatchdogSec=30s
Restart=on-failure
StartLimitInterval=0
RestartSec=10

[Install]
WantedBy=multi-user.target

```

--------------------------------

### Install Java Kubernetes client

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Instructions for cloning and building the Java Kubernetes client library using Maven. This is a prerequisite for using the Java client to interact with the Kubernetes API.

```shell
# Clone java library
git clone --recursive https://github.com/kubernetes-client/java

# Installing project artifacts, POM etc:
cd java
mvn install

```

--------------------------------

### Create DRA Tutorial Namespace

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

Creates a dedicated namespace named 'dra-tutorial' for the DRA driver installation and related resources. This helps in organizing and simplifying cleanup of tutorial-specific components in the cluster.

```bash
kubectl create namespace dra-tutorial
```

--------------------------------

### Install Kubelet, Kubeadm, and Kubectl

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

Installs the core Kubernetes components: kubelet, kubeadm, and kubectl. It provides variations for systems using DNF and DNF5 package managers, ensuring the Kubernetes repository is not excluded during installation.

```bash
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
```

```bash
sudo yum install -y kubelet kubeadm kubectl --setopt=disable_excludes=kubernetes
```

--------------------------------

### Kubernetes Job Status Output Example

Source: https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion

This is an example of the `kubectl get -o yaml job <job-name>` output for a Job configured with `backoffLimitPerIndex`. It shows the `completedIndexes`, `failedIndexes`, and `conditions` fields, including the `FailureTarget` and `Failed` types, indicating the state of the indexed Job.

```yaml
  status:
    completedIndexes: 1,3,5,7,9
    failedIndexes: 0,2,4,6,8
    succeeded: 5          # 1 succeeded pod for each of 5 succeeded indexes
    failed: 10            # 2 failed pods (1 retry) for each of 5 failed indexes
    conditions:
    - message: Job has failed indexes
      reason: FailedIndexes
      status: "True"
      type: FailureTarget
    - message: Job has failed indexes
      reason: FailedIndexes
      status: "True"
      type: Failed

```

--------------------------------

### Create a Pod for Copying and Debugging Example

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod

This command creates a pod named `myapp` using the `busybox` image and runs a command to keep it alive for 1 day. This pod serves as the source for creating a debuggable copy.

```bash
kubectl run myapp --image=busybox:1.28 --restart=Never -- sleep 1d

```

--------------------------------

### GET /flagz

Source: https://kubernetes.io/docs/reference/instrumentation/_print

Retrieves the command-line flags used to start a Kubernetes component. Supports both plain text and structured JSON responses.

```APIDOC
## GET /flagz

### Description
Retrieves the command-line flags used to start a Kubernetes component. Supports both plain text and structured JSON responses.

### Method
GET

### Endpoint
/flagz

### Parameters

#### Headers
- **Accept** (string) - Optional - Specifies the desired response format. For structured JSON, use `application/json;v=v1alpha1;g=config.k8s.io;as=Flagz`.

#### Query Parameters
- **g** (string) - Required for structured response - API group for the structured response.
- **v** (string) - Required for structured response - API version for the structured response.
- **as** (string) - Required for structured response - API kind for the structured response.

### Request Example (Plain Text)
```
GET /flagz
```

### Request Example (Structured JSON)
```
GET /flagz?g=config.k8s.io&v=v1alpha1&as=Flagz
Accept: application/json;v=v1alpha1;g=config.k8s.io;as=Flagz
```

### Response
#### Success Response (200)
- **kind** (string) - The type of the resource (for structured response).
- **apiVersion** (string) - The version of the object (for structured response).
- **metadata** (object) - Standard object's metadata (for structured response).
- **flags** (object) - Contains the command-line flags and their values (for structured response).

#### Response Example (Structured JSON)
```json
{
  "kind": "Flagz",
  "apiVersion": "config.k8s.io/v1alpha1",
  "metadata": {
    "name": "kube-apiserver"
  },
  "flags": {
    "advertise-address": "192.168.8.4",
    "allow-privileged": "true",
    "anonymous-auth": "true",
    "authorization-mode": "[Node,RBAC]",
    "enable-priority-and-fairness": "true",
    "profiling": "true",
    "default-watch-cache-size": "100"
  }
}
```

#### Response Example (Plain Text)
```
kube-apiserver flags
Warning: This endpoint is not meant to be machine parseable, has no formatting compatibility guarantees and is for debugging purposes only.

advertise-address=192.168.8.2
contention-profiling=false
enable-priority-and-fairness=true
profiling=true
authorization-mode=[Node,RBAC]
authorization-webhook-cache-authorized-ttl=5m0s
authorization-webhook-cache-unauthorized-ttl=30s
authorization-webhook-version=v1beta1
default-watch-cache-size=100
```

#### Error Response (406 Not Acceptable)
Returned if `application/json` is requested without specifying all required parameters (`g`, `v`, and `as`).
```

--------------------------------

### Kubernetes Service Output Example (kubectl)

Source: https://kubernetes.io/docs/tasks/network/validate-dual-stack

This is an example output from the `kubectl get svc` command, illustrating a dual-stack Service. It shows the Service name, type, assigned ClusterIP addresses (including an IPv6 address), External IP addresses (including an IPv6 address), and the port configuration.

```text
NAME         TYPE           CLUSTER-IP            EXTERNAL-IP        PORT(S)        AGE
my-service   LoadBalancer   2001:db8:fd00::7ebc   2603:1030:805::5   80:30790/TCP   35s

```

--------------------------------

### Install curl and Fetch localhost (bash)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Installs the 'curl' package within a Debian-based Linux environment and then uses 'curl' to make a GET request to 'localhost'. This is typically run inside a container to verify if the web server is serving content.

```bash
apt-get update
apt-get install curl
curl localhost

```

--------------------------------

### Kubernetes Namespace API - List Request Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

This snippet shows an HTTP GET request to list all Kubernetes namespaces. It can be used to observe the current state of namespaces within the cluster.

```http
GET /api/v1/namespaces?pretty=true HTTP/1.1
Host: kubernetes.default.svc
```

--------------------------------

### Configure Containerd on Linux

Source: https://kubernetes.io/docs/tasks/administer-cluster/migrating-from-dockershim/change-runtime-containerd

Installs and configures containerd on a Linux system. This involves creating a configuration directory, generating a default configuration file, and restarting the containerd service. Follow the official containerd installation guide for specific prerequisites.

```bash
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
sudo systemctl restart containerd

```

--------------------------------

### Start an Nginx pod with custom arguments using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts an Nginx pod and passes custom arguments to its default command. The '--' separator indicates the start of arguments for the container's entrypoint.

```bash
kubectl run nginx --image=nginx -- <arg1> <arg2> ... <argN>
```

--------------------------------

### kubectl proxy Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_proxy/_print

Illustrates various use cases for the kubectl proxy command. These examples demonstrate how to proxy the entire Kubernetes API, serve static files alongside the API, and customize API prefixes for different access levels.

```bash
# To proxy all of the Kubernetes API and nothing else
kubectl proxy --api-prefix=/

```

```bash
# To proxy only part of the Kubernetes API and also some static files
# You can get pods info with 'curl localhost:8001/api/v1/pods'
kubectl proxy --www=/my/files --www-prefix=/static/ --api-prefix=/api/

```

```bash
# To proxy the entire Kubernetes API at a different root
# You can get pods info with 'curl localhost:8001/custom/api/v1/pods'
kubectl proxy --api-prefix=/custom/

```

```bash
# Run a proxy to the Kubernetes API server on port 8011, serving static content from ./local/www/
kubectl proxy --port=8011 --www=./local/www/

```

```bash
# Run a proxy to the Kubernetes API server on an arbitrary local port
# The chosen port for the server will be output to stdout
kubectl proxy --port=0

```

```bash
# Run a proxy to the Kubernetes API server, changing the API prefix to k8s-api
# This makes e.g. the pods API available at localhost:8001/k8s-api/v1/pods/
kubectl proxy --api-prefix=/k8s-api
```

--------------------------------

### Kubectl 'kind: List' Output Example

Source: https://kubernetes.io/docs/reference/using-api/_print

This example shows the output format when using `kubectl get services -A -o yaml`. It uses a client-side 'kind: List' to represent a collection that might contain items of different kinds or from multiple API calls. This format is an internal implementation detail for tools and should be avoided in automation.

```yaml
apiVersion: v1
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
items:
- apiVersion: v1
  kind: Service
  metadata:
    creationTimestamp: "2021-06-03T14:54:12Z"
    labels:
      component: apiserver
      provider: kubernetes
    name: kubernetes
    namespace: default
...
- apiVersion: v1
  kind: Service
  metadata:
    annotations:
      prometheus.io/port: "9153"
      prometheus.io/scrape: "true"
    creationTimestamp: "2021-06-03T14:54:14Z"
    labels:
      k8s-app: kube-dns
      kubernetes.io/cluster-service: "true"
      kubernetes.io/name: CoreDNS
    name: kube-dns
    namespace: kube-system

...
```

--------------------------------

### Watch Bookmarks

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

This endpoint demonstrates how to use the BOOKMARK event to mark that all changes up to a given resourceVersion have been sent. It includes an example of a GET request with watch and allowWatchBookmarks parameters.

```APIDOC
## GET /api/v1/namespaces/{namespace}/{resource}?watch=1&resourceVersion={version}&allowWatchBookmarks=true

### Description
Retrieves watch events for a specified resource, including BOOKMARK events to indicate that all changes up to a certain resourceVersion have been sent.

### Method
GET

### Endpoint
`/api/v1/namespaces/{namespace}/{resource}?watch=1&resourceVersion={version}&allowWatchBookmarks=true`

### Parameters
#### Query Parameters
- **watch** (boolean) - Required - Set to `true` to enable watch.
- **resourceVersion** (string) - Required - The resource version to start watching from.
- **allowWatchBookmarks** (boolean) - Required - Set to `true` to enable watch bookmarks.

### Request Example
```json
GET /api/v1/namespaces/test/pods?watch=1&resourceVersion=10245&allowWatchBookmarks=true
```

### Response
#### Success Response (200)
- **type** (string) - The type of the watch event (e.g., ADDED, BOOKMARK).
- **object** (object) - The object associated with the event. For BOOKMARK events, this contains only `.metadata.resourceVersion`.

#### Response Example
```json
{
  "type": "ADDED",
  "object": {"kind": "Pod", "apiVersion": "v1", "metadata": {"resourceVersion": "10596", ...}, ...}
}
{
  "type": "BOOKMARK",
  "object": {"kind": "Pod", "apiVersion": "v1", "metadata": {"resourceVersion": "12746"} }
}
```
```

--------------------------------

### Kubernetes API Request: List IngressClasses (Shell)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Example of how to list all IngressClass resources in the cluster using the Kubernetes API via a GET request. This command supports various query parameters for filtering and watching.

```shell
curl -X GET \
  http://localhost:8080/apis/networking.k8s.io/v1/ingressclasses?allowWatchBookmarks=true&continue=string&fieldSelector=string&labelSelector=string&limit=0&pretty=string&resourceVersion=string&resourceVersionMatch=string&sendInitialEvents=true&timeoutSeconds=0&watch=true \
  -H 'Accept: application/json'
```

--------------------------------

### Get Service EndpointSlices

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods

Retrieve EndpointSlice resources associated with a service to verify that endpoints are being created and that they match the expected number of pods.

```bash
kubectl get endpointslices -l kubernetes.io/service-name=${SERVICE_NAME}
```

--------------------------------

### GET /flagz (Structured JSON)

Source: https://kubernetes.io/docs/reference/instrumentation/zpages

Retrieves the command-line arguments used to start a component in a structured JSON format. Requires specific `Accept` header for versioned response.

```APIDOC
## GET /flagz (Structured JSON)

### Description
Retrieves the command-line arguments used to start a component in a structured JSON format. Requires specific `Accept` header for versioned response.

### Method
GET

### Endpoint
/flagz

### Parameters
#### Headers
- **Accept** (string) - Required - Specifies the desired response format. Example: `application/json;v=v1alpha1;g=config.k8s.io;as=Flagz`

### Request Example
```
GET /flagz HTTP/1.1
Host: <your-api-server-host>
Accept: application/json;v=v1alpha1;g=config.k8s.io;as=Flagz
```

### Response
#### Success Response (200)
- **kind** (string) - The type of the resource, "Flagz".
- **apiVersion** (string) - The version of the API, e.g., "config.k8s.io/v1alpha1".
- **metadata** (object) - Standard object's metadata.
  - **name** (string) - The name of the component (e.g., "kube-apiserver").
- **flags** (object) - Contains the command-line flags and their values.
  - **flagName** (string) - The value of the flag.

#### Response Example
```json
{
  "kind": "Flagz",
  "apiVersion": "config.k8s.io/v1alpha1",
  "metadata": {
    "name": "kube-apiserver"
  },
  "flags": {
    "advertise-address": "192.168.8.4",
    "allow-privileged": "true",
    "anonymous-auth": "true",
    "authorization-mode": "[Node,RBAC]",
    "enable-priority-and-fairness": "true",
    "profiling": "true",
    "default-watch-cache-size": "100"
  }
}
```

#### Error Response (406 Not Acceptable)
Returned if the `Accept` header is missing required parameters (`g`, `v`, and `as`).
```

--------------------------------

### Example DNS Name to IP Address Mapping for Control Plane Endpoint

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm

This example demonstrates how to map a custom DNS name to the IP address of a control-plane node. This mapping is crucial when using the `--control-plane-endpoint` argument with `kubeadm init` to facilitate future high availability setups or load balancer integration.

```text
192.168.0.102 cluster-endpoint

```

--------------------------------

### Get DRA Resources (DeviceClasses, ResourceSlices, ResourceClaims, ResourceClaimTemplates)

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

Retrieves lists of DRA-related resources from the Kubernetes cluster. These commands are used to inspect the initial state of DRA components before and after driver installation. They help confirm if any DRA drivers have advertised resources.

```bash
kubectl get deviceclasses
kubectl get resourceslices
kubectl get resourceclaims -A
kubectl get resourceclaimtemplates -A
```

--------------------------------

### Install kubectl to System Directory

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

Installs the downloaded kubectl binary to the system's local bin directory, making it available system-wide. Requires root privileges.

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

--------------------------------

### Install kubectl on Debian/Ubuntu using apt

Source: https://kubernetes.io/docs/tasks/tools/_print

Installs kubectl on Debian-based systems. It first installs necessary packages, downloads the Kubernetes signing key, adds the Kubernetes apt repository, and finally updates the package index and installs kubectl.

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
# If the folder /etc/apt/keyrings does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.35/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.35/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly
sudo apt-get update
sudo apt-get install -y kubectl
```

--------------------------------

### Apply Baseline Pod in Example Namespace

Source: https://kubernetes.io/docs/tutorials/security/_print

Applies a baseline Pod to the 'example' namespace to verify Pod Security Standard enforcement. The output will include warnings if the Pod violates the configured PSS.

```bash
kubectl apply -n example -f https://k8s.io/examples/security/example-baseline-pod.yaml

```

--------------------------------

### Download and Install Kubeadm and Kubelet Binaries

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

Downloads the latest stable release of kubeadm and kubelet binaries for the specified architecture and installs them into the defined DOWNLOAD_DIR. It also sets execute permissions and configures systemd service files.

```bash
RELEASE="$(curl -sSL https://dl.k8s.io/release/stable.txt)"
ARCH="amd64"
cd $DOWNLOAD_DIR
sudo curl -L --remote-name-all https://dl.k8s.io/release/${RELEASE}/bin/linux/${ARCH}/{kubeadm,kubelet}
sudo chmod +x {kubeadm,kubelet}
```

```bash
RELEASE_VERSION="v0.16.2"
curl -sSL "https://raw.githubusercontent.com/kubernetes/release/${RELEASE_VERSION}/cmd/krel/templates/latest/kubelet/kubelet.service" | sed "s:/usr/bin:${DOWNLOAD_DIR}:g" | sudo tee /usr/lib/systemd/system/kubelet.service
sudo mkdir -p /usr/lib/systemd/system/kubelet.service.d
curl -sSL "https://raw.githubusercontent.com/kubernetes/release/${RELEASE_VERSION}/cmd/krel/templates/latest/kubeadm/10-kubeadm.conf" | sed "s:/usr/bin:${DOWNLOAD_DIR}:g" | sudo tee /usr/lib/systemd/system/kubelet.service.d/10-kubeadm.conf
```

--------------------------------

### Start a Hazelcast pod with labels using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts a Hazelcast pod and applies two labels: 'app=hazelcast' and 'env=prod'. Labels are key-value pairs used for organizing and selecting Kubernetes objects.

```bash
kubectl run hazelcast --image=hazelcast/hazelcast --labels="app=hazelcast,env=prod"
```

--------------------------------

### kubectl describe examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_describe

This snippet provides practical examples of using the kubectl describe command for various scenarios, including describing nodes, pods, resources from a file, all resources of a type, and resources filtered by labels.

```bash
# Describe a node
kubectl describe nodes kubernetes-node-emt8.c.myproject.internal
```

```bash
# Describe a pod
kubectl describe pods/nginx
```

```bash
# Describe a pod identified by type and name in "pod.json"
kubectl describe -f pod.json
```

```bash
# Describe all pods
kubectl describe pods
```

```bash
# Describe pods by label name=myLabel
kubectl describe pods -l name=myLabel
```

```bash
# Describe all pods managed by the 'frontend' replication controller
# (rc-created pods get the name of the rc as a prefix in the pod name)
kubectl describe pods frontend
```

--------------------------------

### Disable KubeletPodResourcesGet Feature Gate

Source: https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins

Command to start kubelet services with the KubeletPodResourcesGet feature gate disabled. This is used to turn off the Get endpoint functionality.

```bash
--feature-gates=KubeletPodResourcesGet=false

```

--------------------------------

### Start an Nginx pod with a custom command and arguments using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts an Nginx pod, explicitly defines a custom command, and provides arguments for that command. The '--command' flag enables the specification of a custom entrypoint.

```bash
kubectl run nginx --image=nginx --command -- <cmd> <arg1> ... <argN>
```

--------------------------------

### Kubernetes Kubelet Credential Provider Configuration Example

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

An example configuration file for the kubelet's image credential provider. This file specifies the list of credential provider helper plugins that the kubelet will invoke for container images. Multiple providers can match a single image, and their results are combined.

```yaml
apiVersion: kubelet.config.k8s.io/v1
kind: CredentialProviderConfig
# providers is a list of credential provider helper plugins that will be enabled by the kubelet.
# Multiple providers may match against a single image, in which case credentials
# from all providers will be returned to the kubelet. If multiple providers are called
# for a single image, the results are combined. If providers return overlapping
```

--------------------------------

### Example Pod Manifest (BestEffort QoS)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This is a basic Pod manifest example. It defines a single container with an nginx image. Since no resource requests or limits are specified, this Pod will run in the 'BestEffort' QoS class.

```yaml
spec:
  containers:
  - name: nginx
    image: nginx

```

--------------------------------

### Verify Admission Controller Loading (kubectl logs)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp

This example shows log output from the Kubernetes API server at startup, listing the loaded mutating and validating admission controllers. It is used to verify that the PodSecurity admission controller is loaded and that PodSecurityPolicy is no longer present.

```bash
I0218 00:59:44.903329      13 plugins.go:158] Loaded 16 mutating admission controller(s) successfully in the following order: NamespaceLifecycle,LimitRanger,ServiceAccount,NodeRestriction,TaintNodesByCondition,Priority,DefaultTolerationSeconds,ExtendedResourceToleration,PersistentVolumeLabel,DefaultStorageClass,StorageObjectInUseProtection,RuntimeClass,DefaultIngressClass,MutatingAdmissionWebhook.
I0218 00:59:44.903350      13 plugins.go:161] Loaded 14 validating admission controller(s) successfully in the following order: LimitRanger,ServiceAccount,PodSecurity,Priority,PersistentVolumeClaimResize,RuntimeClass,CertificateApproval,CertificateSigning,CertificateSubjectRestriction,DenyServiceExternalIPs,ValidatingAdmissionWebhook,ResourceQuota.
```

--------------------------------

### Kuberc: Define Aliases for Kubectl Commands

Source: https://kubernetes.io/docs/reference/kubectl/_print

The `.kuberc` file allows defining custom aliases for kubectl commands. This example creates an alias 'getn' for 'kubectl get' with a default JSON output format.

```yaml
apiVersion: kubectl.config.k8s.io/v1beta1
kind: Preference
aliases:
- name: getn
  command: get
  options:
   - name: output
     default: json

```

--------------------------------

### JSON Resource Encoding Examples

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

Provides examples of how to list resources and create resources using JSON encoding with the Kubernetes API.

```APIDOC
### JSON resource encoding

The Kubernetes API defaults to using JSON for encoding HTTP message bodies.

For example:
  1. List all of the pods on a cluster, without specifying a preferred format
```
GET /api/v1/pods

```
```
200 OK
Content-Type: application/json

… JSON encoded collection of Pods (PodList object)

```

  2. Create a pod by sending JSON to the server, requesting a JSON response.
```
POST /api/v1/namespaces/test/pods
Content-Type: application/json
Accept: application/json
… JSON encoded Pod object

```
```
200 OK
Content-Type: application/json

{
  "kind": "Pod",
  "apiVersion": "v1",
  …
}

```

You can also request table and metadata-only representations of this encoding.
```

--------------------------------

### Kubernetes Pods List Example

Source: https://kubernetes.io/docs/tasks/debug/debug-application/_print

An example output of listing Kubernetes Pods. This output shows Pod names, readiness status, running status, restart counts, and age. High restart counts may indicate Pod issues.

```text
NAME                        READY     STATUS    RESTARTS   AGE
hostnames-632524106-bbpiw   1/1       Running   0          1h
hostnames-632524106-ly40y   1/1       Running   0          1h
hostnames-632524106-tlaok   1/1       Running   0          1h

```

--------------------------------

### Example iptables Rules for a Kubernetes Service

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

This is an example output of `iptables-save | grep hostnames`. It illustrates the iptables rules configured by kube-proxy for a 'hostnames' Service. The rules demonstrate the translation of Service ClusterIPs and ports to specific Pod IPs and ports, including load balancing logic via `statistic --mode random`.

```shell
-A KUBE-SEP-57KPRZ3JQVENLNBR -s 10.244.3.6/32 -m comment --comment "default/hostnames:" -j MARK --set-xmark 0x00004000/0x00004000
-A KUBE-SEP-57KPRZ3JQVENLNBR -p tcp -m comment --comment "default/hostnames:" -m tcp -j DNAT --to-destination 10.244.3.6:9376
-A KUBE-SEP-WNBA2IHDGP2BOBGZ -s 10.244.1.7/32 -m comment --comment "default/hostnames:" -j MARK --set-xmark 0x00004000/0x00004000
-A KUBE-SEP-WNBA2IHDGP2BOBGZ -p tcp -m comment --comment "default/hostnames:" -m tcp -j DNAT --to-destination 10.244.1.7:9376
-A KUBE-SEP-X3P2623AGDH6CDF3 -s 10.244.2.3/32 -m comment --comment "default/hostnames:" -j MARK --set-xmark 0x00004000/0x00004000
-A KUBE-SEP-X3P2623AGDH6CDF3 -p tcp -m comment --comment "default/hostnames:" -m tcp -j DNAT --to-destination 10.244.2.3:9376
-A KUBE-SERVICES -d 10.0.1.175/32 -p tcp -m comment --comment "default/hostnames: cluster IP" -m tcp --dport 80 -j KUBE-SVC-NWV5X2332I4OT4T3
-A KUBE-SVC-NWV5X2332I4OT4T3 -m comment --comment "default/hostnames:" -m statistic --mode random --probability 0.33332999982 -j KUBE-SEP-WNBA2IHDGP2BOBGZ
-A KUBE-SVC-NWV5X2332I4OT4T3 -m comment --comment "default/hostnames:" -m statistic --mode random --probability 0.50000000000 -j KUBE-SEP-X3P2623AGDH6CDF3
-A KUBE-SVC-NWV5X2332I4OT4T3 -m comment --comment "default/hostnames:" -j KUBE-SEP-57KPRZ3JQVENLNBR
```

--------------------------------

### Install kubeadm and kubelet Binaries

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Installs the kubeadm and kubelet binaries for the specified release and architecture. It downloads the binaries to the configured download directory and makes them executable. This step is crucial for bootstrapping and managing Kubernetes clusters.

```shell
RELEASE="$(curl -sSL https://dl.k8s.io/release/stable.txt)"
ARCH="amd64"
cd $DOWNLOAD_DIR
sudo curl -L --remote-name-all https://dl.k8s.io/release/${RELEASE}/bin/linux/${ARCH}/{kubeadm,kubelet}
sudo chmod +x {kubeadm,kubelet}
```

--------------------------------

### Install kubectl using Package Managers (Windows)

Source: https://kubernetes.io/docs/tasks/tools/_print

This section provides commands to install kubectl on Windows using popular package managers: Chocolatey, Scoop, and winget. Each command installs the Kubernetes CLI tool.

```shell
choco install kubernetes-cli
```

```shell
scoop install kubectl
```

```shell
winget install -e --id Kubernetes.kubectl
```

--------------------------------

### List Kubernetes Resources with Custom Columns using kubectl get

Source: https://kubernetes.io/docs/reference/kubectl/_print

Explains how to list Kubernetes resources with custom columns, allowing you to display specific fields in a tabular format. This example shows listing container name and image for a pod.

```bash
# List resource information in custom columns
kubectl get pod test-pod -o custom-columns=CONTAINER:.spec.containers[0].name,IMAGE:.spec.containers[0].image
```

--------------------------------

### Create a Sample Application Pod (kubectl)

Source: https://kubernetes.io/docs/tasks/debug/_print

This command creates a simple pod named `myapp` running a `busybox` container that executes `sleep 1d`. This pod serves as a target for demonstrating how to create a debug copy with modified configurations.

```bash
kubectl run myapp --image=busybox:1.28 --restart=Never -- sleep 1d
```

--------------------------------

### Example Kubernetes Deployment Output after Scaling

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This output shows the result of `kubectl get deployment capacity-reservation` after scaling. It confirms that the deployment has reached its desired replica count (5/5) and that all replicas are up-to-date and available, indicating successful scaling.

```text
NAME                   READY   UP-TO-DATE   AVAILABLE   AGE
capacity-reservation   5/5     5            5           2m

```

--------------------------------

### Create Deployment with kubectl

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

Creates a Kubernetes Deployment named 'hostnames' using the 'registry.k8s.io/serve_hostname' image. This is a common starting point for setting up applications to test service connectivity.

```bash
kubectl create deployment hostnames --image=registry.k8s.io/serve_hostname

```

--------------------------------

### Kubectl Create ClusterRoleBinding Examples

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

These examples show how to create ClusterRoleBindings to grant roles across the entire cluster. ClusterRoleBindings are used for permissions that apply globally, regardless of namespace.

```bash
kubectl create clusterrolebinding root-cluster-admin-binding --clusterrole=cluster-admin --user=root
```

```bash
kubectl create clusterrolebinding kube-proxy-binding --clusterrole=system:node-proxier --user=system:kube-proxy
```

```bash
kubectl create clusterrolebinding myapp-view-binding --clusterrole=view --serviceaccount=acme:myapp
```

--------------------------------

### Kubectl Events Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Provides practical examples of using the `kubectl events` command. These examples demonstrate listing events in the default namespace, all namespaces, watching for events related to a specific resource, and filtering events by type.

```bash
# List recent events in the default namespace
kubectl events

# List recent events in all namespaces
kubectl events --all-namespaces

# List recent events for the specified pod, then wait for more events and list them as they arrive
kubectl events --for pod/web-pod-13je7 --watch

# List recent events in YAML format
kubectl events -oyaml

# List recent only events of type 'Warning' or 'Normal'
kubectl events --types=Warning,Normal
```

--------------------------------

### Example Pod Status Output

Source: https://kubernetes.io/docs/tasks/run-application/_print

This is an example output showing the status of MySQL Pods after they have been successfully created and are running. It indicates the number of ready containers and the age of each Pod.

```text
NAME      READY     STATUS    RESTARTS   AGE
mysql-0   2/2       Running   0          2m
mysql-1   2/2       Running   0          1m
mysql-2   2/2       Running   0          1m
```

--------------------------------

### Kubernetes DeviceClass API Operations

Source: https://kubernetes.io/docs/reference/kubernetes-api/extend-resources/device-class-v1

Provides examples of HTTP requests for common DeviceClass operations in Kubernetes, including GET, POST, PUT, PATCH, and DELETE.

```http
GET /apis/resource.k8s.io/v1/deviceclasses/{name}

```

```http
GET /apis/resource.k8s.io/v1/deviceclasses

```

```http
POST /apis/resource.k8s.io/v1/deviceclasses

```

```http
PUT /apis/resource.k8s.io/v1/deviceclasses/{name}

```

```http
PATCH /apis/resource.k8s.io/v1/deviceclasses/{name}

```

```http
DELETE /apis/resource.k8s.io/v1/deviceclasses/{name}

```

--------------------------------

### Create ConfigMap from Directory with Sample Files

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap

This example demonstrates creating a ConfigMap from multiple files within a directory. It first creates a local directory and then downloads sample configuration files (`game.properties` and `ui.properties`) into it using `wget`. These files will then be used to populate the ConfigMap.

```bash
mkdir -p configure-pod-container/configmap/

# Download the sample files into `configure-pod-container/configmap/` directory
wget https://kubernetes.io/examples/configmap/game.properties -O configure-pod-container/configmap/game.properties
wget https://kubernetes.io/examples/configmap/ui.properties -O configure-pod-container/configmap/ui.properties
```

--------------------------------

### Create API Object from Configuration File (kubectl)

Source: https://kubernetes.io/docs/contribute/style/_print

Shows the `kubectl` command to create an API object from a configuration file. The configuration file should be placed in one of the `<LANG>/examples` subdirectories. This command is used to demonstrate the creation process.

```Bash
kubectl create -f https://k8s.io/examples/pods/storage/gce-volume.yaml
```

--------------------------------

### Kubernetes Pod Spec Examples for QoS Classes

Source: https://kubernetes.io/docs/concepts/policy/node-resource-managers

These examples demonstrate Kubernetes pod specifications and how they map to different Quality of Service (QoS) classes based on resource requests and limits for CPU and memory.

```yaml
spec:
  containers:
  - name: nginx
    image: nginx

```

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      limits:
        memory: "200Mi"
      requests:
        memory: "100Mi"

```

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      limits:
        memory: "200Mi"
        cpu: "2"
      requests:
        memory: "100Mi"
        cpu: "1"

```

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      limits:
        memory: "200Mi"
        cpu: "2"
      requests:
        memory: "200Mi"
        cpu: "2"

```

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      limits:
        memory: "200Mi"
        cpu: "1.5"
      requests:
        memory: "200Mi"
        cpu: "1.5"

```

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      limits:
        memory: "200Mi"
        cpu: "2"

```

--------------------------------

### Avoid Version Comments in Examples

Source: https://kubernetes.io/docs/contribute/style/_print

This example illustrates a common pitfall to avoid when writing Kubernetes configuration examples. It shows an incorrect use of comments to denote alternative versions, which can lead to confusion. The correct approach is to ensure examples are version-specific and do not include comments about other versions.

```yaml
apiVersion: v1 # earlier versions use...
kind: Pod
...
```

--------------------------------

### Verify DRA Driver DaemonSet Pods

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

This command retrieves all Pods belonging to the DRA example driver DaemonSet within the 'dra-tutorial' namespace. It helps confirm that the driver is running on all relevant nodes.

```bash
kubectl get pod -l app.kubernetes.io/name=dra-example-driver -n dra-tutorial
```

--------------------------------

### Example Pod Description Output (Kubernetes)

Source: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers

This is an example output from `kubectl describe pod`. It showcases key fields like 'Limits' for CPU and memory, 'State' including 'Last State' with 'Reason: OOMKilled', and 'Restart Count', which are vital for troubleshooting resource starvation.

```yaml
Name:                           simmemleak-hra99
Namespace:                      default
Image(s):                       saadali/simmemleak
Node:                           kubernetes-node-tf0f/10.240.216.66
Labels:                         name=simmemleak
Status:                         Running
Reason:
Message:
IP:                             10.244.2.75
Containers:
  simmemleak:
    Image:  saadali/simmemleak:latest
    Limits:
      cpu:          100m
      memory:       50Mi
    State:          Running
      Started:      Tue, 07 Jul 2019 12:54:41 -0700
    Last State:     Terminated
      Reason:       OOMKilled
      Exit Code:    137
      Started:      Fri, 07 Jul 2019 12:54:30 -0700
      Finished:     Fri, 07 Jul 2019 12:54:33 -0700
    Ready:          False
    Restart Count:  5
Conditions:
  Type      Status
  Ready     False
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  42s   default-scheduler  Successfully assigned simmemleak-hra99 to kubernetes-node-tf0f
  Normal  Pulled     41s   kubelet            Container image "saadali/simmemleak:latest" already present on machine
  Normal  Created    41s   kubelet            Created container simmemleak
  Normal  Started    41s   kubelet            Started container simmemleak
  Normal  Killing    32s   kubelet            Killing container with id ead3fb35-5cf5-44ed-9ae1-488115be66c6: Need to kill Pod
```

--------------------------------

### Kubectl Create Job Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/_print

Examples demonstrating how to use the 'kubectl create job' command. These include creating a simple job with an image, creating a job with a specific command, and creating a job from an existing cron job.

```bash
# Create a job
kubectl create job my-job --image=busybox

```

```bash
# Create a job with a command
kubectl create job my-job --image=busybox -- date

```

```bash
# Create a job from a cron job named "a-cronjob"
kubectl create job test-job --from=cronjob/a-cronjob

```

--------------------------------

### Kubeadm InitConfiguration Example (YAML)

Source: https://kubernetes.io/docs/reference/config-api/_print

Defines runtime settings for `kubeadm init`, including bootstrap tokens, node registration details, and API endpoint configuration. This is used for settings specific to the node where kubeadm is executed.

```yaml
apiVersion: kubeadm.k8s.io/v1beta4
kind: InitConfiguration
bootstrapTokens:
  - token: "9a08jv.c0izixklcxtmnze7"
    description: "kubeadm bootstrap token"
    ttl: "24h"
  - token: "783bde.3f89s0fje9f38fhf"
    description: "another bootstrap token"
    usages:
  - authentication
  - signing
    groups:
  - system:bootstrappers:kubeadm:default-node-token

nodeRegistration:
  name: "ec2-10-100-0-1"
  criSocket: "unix:///var/run/containerd/containerd.sock"
  taints:
    - key: "kubeadmNode"
      value: "someValue"
      effect: "NoSchedule"
  kubeletExtraArgs:
    - name: v
      value: "5"
  ignorePreflightErrors:
    - IsPrivilegedUser
  imagePullPolicy: "IfNotPresent"
  imagePullSerial: true

localAPIEndpoint:
  advertiseAddress: "10.100.0.1"
  bindPort: 6443
certificateKey: "e6a2eb8581237ab72a4f494f30285ec12a9694d750b9785706a83bfcbbbd2204"
skipPhases:
  - preflight
timeouts:
  controlPlaneComponentHealthCheck: "60s"
  kubenetesAPICall: "40s"

```

--------------------------------

### Versioning Kubernetes Examples in Documentation Front Matter

Source: https://kubernetes.io/docs/contribute/style/style-guide

Specify the minimum Kubernetes server version for code and configuration examples using the `min-kubernetes-server-version` field in the page's front matter. This ensures examples are relevant to the intended audience and version.

```yaml
---
title: <your tutorial title here>
min-kubernetes-server-version: v1.8
---
```

--------------------------------

### Get OS version using systeminfo

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

This command retrieves system information, including the OS version, on Windows systems. It's used to check compatibility with Kubernetes requirements.

```powershell
systeminfo

```

--------------------------------

### Extract Specific Pod Information with kubectl get Templates

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to extract specific fields from Kubernetes resources using the template output format. This example shows retrieving only the 'phase' value of a pod's status.

```bash
# Return only the phase value of the specified pod
kubectl get -o template pod/web-pod-13je7 --template={{.status.phase}}
```

--------------------------------

### Kubernetes PriorityClass API Operations (Go)

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/priority-class-v1

Example Go code demonstrating how to interact with the Kubernetes PriorityClass API. This snippet shows how to create a client and perform operations like getting, listing, creating, updating, patching, and deleting PriorityClasses.

```go
package main

import (
	"context"
	"fmt"
	"log"

	metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
	schedulingv1 "k8s.io/api/scheduling/v1"
	k8sclient "k8s.io/client-go/kubernetes"
	"k8s.io/client-go/tools/clientcmd"
)

func main() {
	// Load Kubernetes configuration
	config, err := clientcmd.BuildConfigFromFlags("", "~/.kube/config")
	if err != nil {
		log.Fatalf("Error building kubeconfig: %s", err.Error())
	}

	// Create a Kubernetes clientset
	clientset, err := k8sclient.NewForConfig(config)
	if err != nil {
		log.Fatalf("Error creating Kubernetes client: %s", err.Error())
	}

	ctx := context.Background()
	priorityClassClient := clientset.SchedulingV1().PriorityClasses()

	// Example: Create a PriorityClass
	newPriorityClass := &schedulingv1.PriorityClass{
		ObjectMeta: metav1.ObjectMeta{
			Name: "example-priority",
		},
		Value:          100,
		GlobalDefault:  false,
		PreemptionPolicy: schedulingv1.PreemptLowerPriority.Pointer(),
		Description:    "An example priority class.",
	}

	createdPC, err := priorityClassClient.Create(ctx, newPriorityClass, metav1.CreateOptions{})
	if err != nil {
		log.Printf("Error creating PriorityClass: %v", err)
	} else {
		fmt.Printf("Created PriorityClass: %s\n", createdPC.Name)
	}

	// Example: List PriorityClasses
	pcs, err := priorityClassClient.List(ctx, metav1.ListOptions{})
	if err != nil {
		log.Fatalf("Error listing PriorityClasses: %s", err.Error())
	}

	fmt.Println("Existing PriorityClasses:")
	for _, pc := range pcs.Items {
		fmt.Printf("- %s (Value: %d)\n", pc.Name, pc.Value)
	}

	// Example: Get a specific PriorityClass
	nameToGet := "example-priority"
	getPC, err := priorityClassClient.Get(ctx, nameToGet, metav1.GetOptions{})
	if err != nil {
		log.Printf("Error getting PriorityClass %s: %v", nameToGet, err)
	} else {
		fmt.Printf("Got PriorityClass: %s\n", getPC.Name)
	}

	// Example: Delete a PriorityClass
	nameToDelete := "example-priority"
	err = priorityClassClient.Delete(ctx, nameToDelete, metav1.DeleteOptions{})
	if err != nil {
		log.Printf("Error deleting PriorityClass %s: %v", nameToDelete, err)
	} else {
		fmt.Printf("Deleted PriorityClass: %s\n", nameToDelete)
	}
}

```

--------------------------------

### Set up Local Workspace and GOPATH

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/kubectl

This snippet demonstrates how to create a local workspace directory and set the GOPATH environment variable, which is crucial for Go development and managing dependencies.

```bash
mkdir -p $HOME/<workspace>

export GOPATH=$HOME/<workspace>
```

--------------------------------

### Kubernetes RBAC RoleBinding LIST API Request (Cluster-wide)

Source: https://kubernetes.io/docs/reference/kubernetes-api/authorization-resources/role-binding-v1

Example HTTP GET request to list all RoleBindings across all namespaces. This operation is useful for cluster-wide administration and auditing.

```http
GET /apis/rbac.authorization.k8s.io/v1/rolebindings
```

--------------------------------

### Clone Kubernetes Repository (Go)

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/_print

This snippet demonstrates how to clone the Kubernetes repository using the `go get` command. It assumes Go and Git are installed and configured. The command fetches the repository into the specified GOPATH directory.

```bash
mkdir $GOPATH/src
cd $GOPATH/src
go get github.com/kubernetes/kubernetes

```

--------------------------------

### ZooKeeper Server Start Command Configuration (Shell)

Source: https://kubernetes.io/docs/tutorials/stateful-application/_print

Demonstrates the command used to start ZooKeeper servers with various configuration parameters passed as command-line arguments. This includes settings for server count, data directories, ports, election timeouts, and logging levels. This method ensures direct control over the ZooKeeper ensemble's operational parameters.

```shell
start-zookeeper \
  --servers=3 \
  --data_dir=/var/lib/zookeeper/data \
  --data_log_dir=/var/lib/zookeeper/data/log \
  --conf_dir=/opt/zookeeper/conf \
  --client_port=2181 \
  --election_port=3888 \
  --server_port=2888 \
  --tick_time=2000 \
  --init_limit=10 \
  --sync_limit=5 \
  --heap=512M \
  --max_client_cnxns=60 \
  --snap_retain_count=3 \
  --purge_interval=12 \
  --max_session_timeout=40000 \
  --min_session_timeout=4000 \
  --log_level=INFO
```

--------------------------------

### Kubernetes Service YAML Output (SingleStack)

Source: https://kubernetes.io/docs/concepts/services-networking/dual-stack

This is an example output of `kubectl get svc my-service -o yaml` for a Service that has been configured with `SingleStack` ipFamilyPolicy. It shows the assigned `clusterIP`, `clusterIPs`, `ipFamilies`, and `ipFamilyPolicy`.

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/name: MyApp
  name: my-service
spec:
  clusterIP: 10.0.197.123
  clusterIPs:
  - 10.0.197.123
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app.kubernetes.io/name: MyApp
  type: ClusterIP
status:
  loadBalancer: {}

```

--------------------------------

### List Pods using Python Kubernetes client

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Shows how to use the Python Kubernetes client library to load kubeconfig and list pods across all namespaces. Installation requires `pip install kubernetes`.

```python
from kubernetes import client, config

config.load_kube_config()

v1=client.CoreV1Api()
print("Listing pods with their IPs:")
ret = v1.list_pod_for_all_namespaces(watch=False)
for i in ret.items:
    print("%s\t%s\t%s" % (i.status.pod_ip, i.metadata.namespace, i.metadata.name))

```

--------------------------------

### kubectl label Examples: Applying to Multiple Resources

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_label/_print

Shows how to apply labels to all resources within a namespace using the --all flag, and how to target a resource defined in a JSON file using the -f flag. These examples highlight bulk operations and file-based resource targeting.

```bash
# Update all pods in the namespace
kubectl label pods --all status=unhealthy

# Update a pod identified by the type and name in "pod.json"
kubectl label -f pod.json status=unhealthy
```

--------------------------------

### Kubectl Top Node Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Examples demonstrating how to use the 'kubectl top node' command. This includes showing metrics for all nodes and for a specific named node.

```bash
# Show metrics for all nodeskubectl top node

# Show metrics for a given node
kubectl top node NODE_NAME
```

--------------------------------

### Set up Go workspace and GOPATH

Source: https://kubernetes.io/docs/contribute/_print

Creates a local workspace directory and exports the GOPATH environment variable to point to this new workspace. This is a foundational step for managing Go projects.

```bash
mkdir -p $HOME/<workspace>

export GOPATH=$HOME/<workspace>
```

--------------------------------

### Get ResourceClaim Objects

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

This command lists all ResourceClaim objects within the 'dra-tutorial' namespace. It provides a summary of their current states, such as 'allocated' or 'reserved', indicating the resource allocation status.

```bash
kubectl get resourceclaims -n dra-tutorial
```

--------------------------------

### kubectl Command Syntax Example

Source: https://kubernetes.io/docs/reference/kubectl

Demonstrates the basic syntax for running kubectl commands, including the command, resource type, name, and optional flags. This is fundamental for interacting with the Kubernetes API.

```bash
kubectl [command] [TYPE] [NAME] [flags]
```

--------------------------------

### Get Pods by Label with kubectl

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

Retrieves a list of Pods that match a specific label selector. This is fundamental for verifying the status and existence of application instances within the cluster.

```bash
kubectl get pods -l app=hostnames

```

--------------------------------

### kubectl run Examples: Interactive and Custom Commands

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/_print

Provides examples for running pods in an interactive mode, controlling restart behavior, and executing custom commands with specific arguments within the container.

```bash
# Start a busybox pod and keep it in the foreground, don't restart it if it exits
kubectl run -i -t busybox --image=busybox --restart=Never

# Start the nginx pod using the default command, but use custom arguments (arg1 .. argN) for that command
kubectl run nginx --image=nginx -- <arg1> <arg2> ... <argN>

# Start the nginx pod using a different command and custom arguments
kubectl run nginx --image=nginx --command -- <cmd> <arg1> ... <argN>
```

--------------------------------

### Kubelet Configuration File Example

Source: https://kubernetes.io/docs/tasks/administer-cluster/kubelet-config-file

An example of a Kubelet configuration file in YAML format. This file defines parameters such as the address, port, serialization of image pulls, and eviction thresholds. Ensure the kubelet has read permissions on this file.

```yaml
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
address: "192.168.0.8"
port: 20250
serializeImagePulls: false
evictionHard:
    memory.available:  "100Mi"
    nodefs.available:  "10%"
    nodefs.inodesFree: "5%"
    imagefs.available: "15%"
    imagefs.inodesFree: "5%"

```

--------------------------------

### Install Website Dependencies with npm

Source: https://kubernetes.io/docs/contribute/new-content/preview-locally

Installs project dependencies using npm ci, which is recommended for ensuring a clean and reproducible environment. This command should be run after installing Hugo and Node.js as specified in netlify.toml.

```bash
npm ci

```

--------------------------------

### Expose Kubernetes Resources as Services (kubectl)

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to use the `kubectl expose` command to create Kubernetes Services for various resources like replication controllers, pods, and deployments. It covers exposing different ports, protocols, and naming conventions for the services.

```bash
# Create a service for a replicated nginx, which serves on port 80 and connects to the containers on port 8000
kubectl expose rc nginx --port=80 --target-port=8000

# Create a service for a replication controller identified by type and name specified in "nginx-controller.yaml", which serves on port 80 and connects to the containers on port 8000
kubectl expose -f nginx-controller.yaml --port=80 --target-port=8000

# Create a service for a pod valid-pod, which serves on port 444 with the name "frontend"
kubectl expose pod valid-pod --port=444 --name=frontend

# Create a second service based on the above service, exposing the container port 8443 as port 443 with the name "nginx-https"
kubectl expose service nginx --port=443 --target-port=8443 --name=nginx-https

# Create a service for a replicated streaming application on port 4100 balancing UDP traffic and named 'video-stream'.
kubectl expose rc streamer --port=4100 --protocol=UDP --name=video-stream

# Create a service for a replicated nginx using replica set, which serves on port 80 and connects to the containers on port 8000
kubectl expose rs nginx --port=80 --target-port=8000

# Create a service for an nginx deployment, which serves on port 80 and connects to the containers on port 8000
kubectl expose deployment nginx --port=80 --target-port=8000
```

--------------------------------

### Pull Example DRA Driver Image

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

Pulls the 'dra-example-driver' Docker image to a cluster node. This step verifies that the nodes can access the driver image, simulating a real-world scenario where nodes need to download and run the driver.

```bash
docker pull registry.k8s.io/dra-example-driver/dra-example-driver:v0.2.0
```

--------------------------------

### Allow GET/POST to non-resource endpoint '/healthz' (Kubernetes YAML)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example shows a Kubernetes Role rule for accessing non-resource endpoints. It allows 'get' and 'post' requests to the '/healthz' endpoint and its subpaths. This requires a ClusterRole.

```yaml
rules:
- nonResourceURLs: ["/healthz", "/healthz/*"]
  verbs: ["get", "post"]
```

--------------------------------

### Kubernetes Command-Line Operations with Labels

Source: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels

Provides examples of using `kubectl` to interact with Kubernetes resources based on labels. This includes applying a YAML file, getting pods with specific label columns, selecting pods based on multiple label criteria, and updating labels on existing pods.

```bash
kubectl apply -f examples/guestbook/all-in-one/guestbook-all-in-one.yamlkubectl get pods -Lapp -Ltier -Lrole
```

```bash
kubectl get pods -lapp=guestbook,role=replica
```

```bash
kubectl label pods -l app=nginx tier=fe
```

```bash
kubectl get pods -l app=nginx -L tier
```

--------------------------------

### Kubernetes RawExtension Usage Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Demonstrates the usage of runtime.RawExtension for handling arbitrary data, typically used for driver-specific configuration parameters in Kubernetes. It shows how to embed and unpack data.

```go
// Internal package:
type MyAPIObjectInternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin runtime.Object `json:"myPlugin"`
}
type PluginAInternal struct {
	AOption string `json:"aOption"`
}

// External package:
type MyAPIObjectExternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin runtime.RawExtension `json:"myPlugin"`
}
type PluginAExternal struct {
	AOption string `json:"aOption"`
}

// On the wire, the JSON will look something like this:
// {
//   "kind": "MyAPIObject",
//   "apiVersion": "v1",
//   "myPlugin": {
//     "kind": "PluginA",
//     "aOption": "foo"
//   }
// }
// Decode first uses json or yaml to unmarshal the serialized data into your external MyAPIObject.
// That causes the raw JSON to be stored, but not unpacked.
// The next step is to copy (using pkg/conversion) into the internal struct.
// The runtime package's DefaultScheme has conversion functions installed which will unpack the JSON stored in RawExtension,
// turning it into the correct object type, and storing it in the Object.
// (TODO: In the case where the object is of an unknown type, a runtime.Unknown object will be created and stored.)
```

--------------------------------

### Expose Deployment as a NodePort Service (kubectl)

Source: https://kubernetes.io/docs/tasks/access-application-cluster/_print

Creates a Kubernetes Service of type NodePort named 'example-service' to expose the 'hello-world' Deployment. NodePort services make the application accessible on a static port on each Node's IP address.

```bash
kubectl expose deployment hello-world --type=NodePort --name=example-service

```

--------------------------------

### List IngressClasses HTTP Request (Example)

Source: https://kubernetes.io/docs/reference/kubernetes-api/service-resources/ingress-class-v1

Illustrates how to list all IngressClass resources in the cluster using an HTTP GET request. It supports various query parameters for filtering, pagination, and watching resources.

```http
GET /apis/networking.k8s.io/v1/ingressclasses
Host: localhost
```

--------------------------------

### Kubernetes API Request for Pod Logs

Source: https://kubernetes.io/docs/reference/access-authn-authz/rbac

Example of a GET request to retrieve logs for a specific Pod in Kubernetes. This demonstrates the structure of API calls involving resources and subresources.

```http
GET /api/v1/namespaces/{namespace}/pods/{name}/log

```

--------------------------------

### Get Pod Status

Source: https://kubernetes.io/docs/tutorials/security/seccomp

This command retrieves the status of a specified Kubernetes Pod. It's used to verify that the 'default-pod' has started successfully with the RuntimeDefault seccomp profile.

```bash
kubectl get pod default-pod
```

--------------------------------

### Container Commands Examples

Source: https://kubernetes.io/docs/tasks/debug/_print

Examples of commands that can be run inside a Kubernetes container after obtaining a shell. These include listing directory contents, inspecting system files, and installing/running diagnostic tools like tcpdump and lsof.

```bash
# Run this inside the container
ls /
cat /proc/mounts
cat /proc/1/maps
apt-get update
apt-get install -y tcpdump
tcpdump
apt-get install -y lsof
lsof
apt-get install -y procps
ps aux
ps aux | grep nginx
```

--------------------------------

### Configure Swap to Enable on Boot

Source: https://kubernetes.io/docs/tutorials/cluster-management/_print

Methods to ensure swap is active after a system reboot. This includes adding an entry to `/etc/fstab` for traditional swap files or using systemd units for more advanced control, potentially delaying kubelet startup.

```bash
# Example /etc/fstab entry:
/swapfile swap swap defaults 0 0
```

--------------------------------

### Example: Create ConfigMap from a Folder using kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_configmap

This example demonstrates creating a ConfigMap named 'my-config' by referencing all files within the 'path/to/bar' directory. Each file's basename will be used as a key in the ConfigMap.

```bash
kubectl create configmap my-config --from-file=path/to/bar
```

--------------------------------

### Install kubectl using Homebrew

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

This command installs kubectl using the Homebrew package manager, commonly used on macOS and Linux. After installation, `kubectl version --client` verifies the installation. This method is suitable for users who prefer Homebrew for managing their software.

```bash
brew install kubectl
kubectl version --client
```

--------------------------------

### Kubectl Autoscale Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_autoscale/_print

Provides practical examples of using the kubectl autoscale command for different scenarios. These examples demonstrate how to set minimum and maximum pod counts, target CPU utilization, and target memory for various Kubernetes resource types.

```bash
# Auto scale a deployment "foo", with the number of pods between 2 and 10, no target CPU utilization specified so a default autoscaling policy will be used
kubectl autoscale deployment foo --min=2 --max=10
```

```bash
# Auto scale a replication controller "foo", with the number of pods between 1 and 5, target CPU utilization at 80%
kubectl autoscale rc foo --max=5 --cpu=80%
```

```bash
# Auto scale a deployment "bar", with the number of pods between 3 and 6, target average CPU of 500m and memory of 200Mi
kubectl autoscale deployment bar --min=3 --max=6 --cpu=500m --memory=200Mi
```

```bash
# Auto scale a deployment "bar", with the number of pods between 2 and 8, target CPU utilization 60% and memory utilization 70%
kubectl autoscale deployment bar --min=3 --max=6 --cpu=60% --memory=70%
```

--------------------------------

### Example: Describe a Specific Context

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example shows how to retrieve detailed information about a specific context by providing its name to the 'kubectl config get-contexts' command.

```bash
kubectl config get-contexts my-context
```

--------------------------------

### Kubernetes RBAC ClusterRole and RoleBinding Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/rbac

This example demonstrates a Kubernetes ClusterRole and RoleBinding configuration. The ClusterRole 'role-grantor' allows creating role bindings and binding specific ClusterRoles ('admin', 'edit', 'view'). The RoleBinding 'role-grantor-binding' grants these permissions to 'user-1' within the 'user-1-namespace'. This setup enables 'user-1' to assign predefined roles to other users in their namespace.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: role-grantor
rules:
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["rolebindings"]
  verbs: ["create"]
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["clusterroles"]
  verbs: ["bind"]
  # omit resourceNames to allow binding any ClusterRole
  resourceNames: ["admin","edit","view"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: role-grantor-binding
  namespace: user-1-namespace
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: role-grantor
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: user-1

```

--------------------------------

### Kubernetes kubectl wait command examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

This snippet demonstrates various use cases for the `kubectl wait` command. It shows how to wait for pods to be ready, for specific conditions like `false` or `Running` phase, and for services to have ingress. It also covers waiting for resource creation or deletion with timeouts.

```bash
  # Wait for the pod "busybox1" to contain the status condition of type "Ready"
  kubectl wait --for=condition=Ready pod/busybox1
  
  # The default value of status condition is true; you can wait for other targets after an equal delimiter (compared after Unicode simple case folding, which is a more general form of case-insensitivity)
  kubectl wait --for=condition=Ready=false pod/busybox1
  
  # Wait for the pod "busybox1" to contain the status phase to be "Running"
  kubectl wait --for=jsonpath='{.status.phase}'=Running pod/busybox1
  
  # Wait for pod "busybox1" to be Ready
  kubectl wait --for='jsonpath={.status.conditions[?(@.type=="Ready")].status}=True' pod/busybox1
  
  # Wait for the service "loadbalancer" to have ingress
  kubectl wait --for=jsonpath='{.status.loadBalancer.ingress}' service/loadbalancer
  
  # Wait for the secret "busybox1" to be created, with a timeout of 30s
  kubectl create secret generic busybox1
  kubectl wait --for=create secret/busybox1 --timeout=30s
  
  # Wait for the pod "busybox1" to be deleted, with a timeout of 60s, after having issued the "delete" command
  kubectl delete pod/busybox1
  kubectl wait --for=delete pod/busybox1 --timeout=60s
```

--------------------------------

### Configure Kubelet to Tolerate Swap Memory

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

Allows the kubelet to start even if swap memory is detected on a node. This is achieved by setting `failSwapOn: false` in the kubelet configuration or as a command-line argument. Workloads do not get swap access by default and require `swapBehavior` to be set.

```yaml
failSwapOn: false

```

--------------------------------

### Kubectl Set Image Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Illustrative examples of using the 'kubectl set image' command. These examples demonstrate updating specific containers in a deployment, updating images for multiple resource types, updating all containers in a daemonset, and performing a dry run with local output.

```bash
# Set a deployment's nginx container image to 'nginx:1.9.1', and its busybox container image to 'busybox'
kubectl set image deployment/nginx busybox=busybox nginx=nginx:1.9.1

# Update all deployments' and rc's nginx container's image to 'nginx:1.9.1'
kubectl set image deployments,rc nginx=nginx:1.9.1 --all

# Update image of all containers of daemonset abc to 'nginx:1.9.1'
kubectl set image daemonset abc *=nginx:1.9.1

# Print result (in yaml format) of updating nginx container image from local file, without hitting the server
kubectl set image -f path/to/file.yaml nginx=nginx:1.9.1 --local -o yaml
```

--------------------------------

### Kubectl Describe Command Examples

Source: https://kubernetes.io/docs/reference/kubectl

Shows examples of the 'kubectl describe' command for displaying detailed information about Kubernetes resources. This includes describing nodes, pods, and pods managed by a replication controller.

```bash
# Describe a node
kubectl describe nodes <node-name>

# Describe a pod
kubectl describe pods/<pod-name>

# Describe pods managed by a replication controller
kubectl describe pods --selector=replicationcontroller=<rc-name>
```

--------------------------------

### Get MAC address using ip link

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

This command displays network interface information, including MAC addresses. Unique MAC addresses are crucial for Kubernetes to identify nodes correctly.

```shell
ip link

```

--------------------------------

### Pull DRA Example Driver Image

Source: https://kubernetes.io/docs/tutorials/cluster-management/_print

Pulls the 'dra-example-driver:v0.2.0' Docker image from the 'registry.k8s.io' repository. This step confirms that your cluster nodes have access to the necessary driver image, which is a prerequisite for installation. This command is typically run from within one of the cluster's nodes.

```bash
docker pull registry.k8s.io/dra-example-driver/dra-example-driver:v0.2.0

```

--------------------------------

### Install Missing System Executables for kubeadm

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

Addresses warnings during `kubeadm init` indicating that `ebtables` or `ethtool` are not found. Provides installation commands for Debian/Ubuntu and CentOS/Fedora systems.

```shell
apt install ebtables ethtool
```

```shell
yum install ebtables ethtool
```

--------------------------------

### Get kernel version using uname

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

This command retrieves the kernel version of a Linux system. It's used to ensure compatibility with Kubernetes requirements, as kubeadm relies on specific kernel features.

```shell
uname -r

```

--------------------------------

### Install Kubernetes Python Client Library

Source: https://kubernetes.io/docs/tasks/access-application-cluster/_print

This command installs the Kubernetes Python client library using pip. For alternative installation methods and more options, refer to the Python Client Library documentation.

```bash
pip install kubernetes
```

--------------------------------

### Kubectl Set Selector Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

These examples demonstrate practical use cases for the 'kubectl set selector' command. The first example shows how to set a selector on a Service object before creating it, using a dry-run and piping the output. The second example illustrates setting a label (which often implies selector functionality) on a Deployment before creating it.

```bash
# Set the labels and selector before creating a deployment/service pair
kubectl create service clusterip my-svc --clusterip="None" -o yaml --dry-run=client | kubectl set selector --local -f - 'environment=qa' -o yaml | kubectl create -f -
```

```bash
kubectl create deployment my-dep --image=nginx -o yaml --dry-run=client | kubectl label --local -f - environment=qa -o yaml | kubectl create -f -
```

--------------------------------

### Verify kubectl Convert Plugin Installation

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows

A command to verify if the kubectl convert plugin has been successfully installed by checking its help output. If no error is displayed, the installation is considered successful.

```bash
kubectl convert --help
```

--------------------------------

### Serve Kubernetes Website Locally with Make

Source: https://kubernetes.io/docs/contribute/new-content/_print

This command initiates a local server for the Kubernetes website using the 'make container-serve' target. It's designed to build and serve the site within a Docker container, allowing for local previewing of changes. Ensure Docker is installed and running.

```bash
make container-serve
```

--------------------------------

### Using Hugo Figure Shortcode for Diagrams

Source: https://kubernetes.io/docs/contribute/style/diagram-guide

This example shows how to use the Hugo `figure` shortcode to embed a diagram, likely generated by Mermaid. This method integrates diagrams into Hugo-generated websites.

```html
{{< figure src="/path/to/your/diagram.svg" alt="Diagram Caption" >}}
```

--------------------------------

### Serve Kubernetes Website Locally with Local Hugo

Source: https://kubernetes.io/docs/contribute/new-content/preview-locally

Starts the Hugo server locally using the 'make serve' command within the website repository directory. This method requires Hugo (Extended edition) and Node.js to be installed locally. It serves the site at http://localhost:1313.

```bash
cd <path_to_your_repo>/website
make serve

```

--------------------------------

### Get ZooKeeper Logging Configuration (Kubernetes)

Source: https://kubernetes.io/docs/tutorials/_print

Retrieves the current Log4j logging configuration file from a ZooKeeper pod running in Kubernetes. This command is useful for understanding the existing logging setup before making changes.

```bash
kubectl exec zk-0 cat /usr/etc/zookeeper/log4j.properties
```

--------------------------------

### Test Kubectl Plugin with Arguments and Flags

Source: https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins

This example shows how to invoke a previously installed kubectl plugin with additional arguments and flags. Kubectl will correctly identify the plugin and pass all subsequent arguments and flags to the plugin executable. This demonstrates the plugin mechanism's ability to handle complex command-line invocations.

```bash
# test that calling your plugin via a "kubectl" command works
# even when additional arguments and flags are passed to your
# plugin executable by the user.
kubectl foo bar baz arg1 --meaningless-flag=true

```

--------------------------------

### Define Pod Restart Policy with Kompose

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

Translates the 'restart' policy from docker-compose to Kubernetes Pod 'restartPolicy'. This determines how pods are managed upon termination. For example, 'on-failure' in docker-compose results in 'OnFailure' restartPolicy for the Pod.

```yaml
version: '2'

services:
  pival:
    image: perl
    command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
    restart: "on-failure"
```

--------------------------------

### Bash Completion for kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_completion

Provides instructions and code examples for enabling bash autocompletion for kubectl. This includes installation on macOS using homebrew and on Linux, as well as sourcing the completion script into the current shell or .bash_profile.

```bash
# Installing bash completion on macOS using homebrew
## If running Bash 3.2 included with macOS
brew install bash-completion
## or, if running Bash 4.1+
brew install bash-completion@2
## If kubectl is installed via homebrew, this should start working immediately
## If you've installed via other means, you may need add the completion to your completion directory
kubectl completion bash > $(brew --prefix)/etc/bash_completion.d/kubectl


# Installing bash completion on Linux
## If bash-completion is not installed on Linux, install the 'bash-completion' package
## via your distribution's package manager.
## Load the kubectl completion code for bash into the current shell
source <(kubectl completion bash)
## Write bash completion code to a file and source it from .bash_profile
kubectl completion bash > ~/.kube/completion.bash.inc
printf "
# kubectl shell completion
source '$HOME/.kube/completion.bash.inc'
" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

--------------------------------

### Example: Create ExternalName Service

Source: https://kubernetes.io/docs/reference/kubectl/_print

This example demonstrates how to create an ExternalName service named 'my-ns' that references the external DNS name 'bar.com'. This is a practical application of the `kubectl create service externalname` command.

```bash
kubectl create service externalname my-ns --external-name bar.com
```

--------------------------------

### Install kubectl on openSUSE/SLES using zypper

Source: https://kubernetes.io/docs/tasks/tools/_print

Installs kubectl on SUSE-based systems using zypper. It adds the Kubernetes zypper repository configuration, updates zypper, and then installs kubectl. Requires manual confirmation for the GPG key.

```bash
# This overwrites any existing configuration in /etc/zypp/repos.d/kubernetes.repo
cat <<EOF | sudo tee /etc/zypp/repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/repodata/repomd.xml.key
EOF
sudo zypper update
sudo zypper install -y kubectl
```

--------------------------------

### Kubernetes RawExtension Usage Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Demonstrates the usage of RawExtension in Kubernetes for handling arbitrary data, particularly for driver-specific configurations. It shows how to define internal and external API objects and how data is serialized and deserialized.

```go
package main

import (
	"encoding/json"
	"fmt"
	"k8s.io/apimachinery/pkg/runtime"
	"k8s.io/apimachinery/pkg/runtime/schema"
)

// Internal package example
type MyAPIObjectInternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin runtime.Object `json:"myPlugin"`
}

type PluginAInternal struct {
	AOption string `json:"aOption"`
}

// External package example
type MyAPIObjectExternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin runtime.RawExtension `json:"myPlugin"`
}

type PluginAExternal struct {
	AOption string `json:"aOption"`
}

func main() {
	// Example JSON payload as it would appear on the wire
	jsonPayload := `{
		"kind":"MyAPIObject",
		"apiVersion":"v1",
		"myPlugin": {
			"kind":"PluginA",
			"aOption":"foo"
		}
	}`

	// Simulate decoding into the external type
	var externalObject MyAPIObjectExternal
	err := json.Unmarshal([]byte(jsonPayload), &externalObject)
	if err != nil {
		fmt.Printf("Error unmarshalling external object: %v\n", err)
		return
	}

	fmt.Printf("External Object MyPlugin Kind: %s\n", externalObject.MyPlugin.Kind)

	// Simulate conversion to internal type (simplified)
	// In a real scenario, this would involve a runtime.Scheme and converters.
	// For demonstration, we'll manually create a scheme and register types.

scheme := runtime.NewScheme()
schema.GroupVersionKindToSchema(schema.GroupVersionKind{Group: "", Version: "v1", Kind: "MyAPIObject"})
schema.GroupVersionKindToSchema(schema.GroupVersionKind{Group: "", Version: "v1", Kind: "PluginA"})

	s// Create a new internal object
	internalObject := &MyAPIObjectInternal{}

	// Manually decode the RawExtension into the correct internal type
	// This is a simplified representation of what pkg/conversion would do.
	pluginA := &PluginAInternal{}
	err = json.Unmarshal(externalObject.MyPlugin.Raw, pluginA)
	if err != nil {
		fmt.Printf("Error unmarshalling plugin A: %v\n", err)
		return
	}

	internalObject.MyPlugin = pluginA

	fmt.Printf("Internal Object MyPlugin AOption: %s\n", pluginA.AOption)

	// Example of creating an unknown object if the kind is not registered
	unknownPayload := `{
		"kind":"UnknownPlugin",
		"data":"some data"
	}`

	var unknownRawExtension runtime.RawExtension
	err = json.Unmarshal([]byte(unknownPayload), &unknownRawExtension)
	if err != nil {
		fmt.Printf("Error unmarshalling unknown payload: %v\n", err)
		return
	}

	// In a real scenario, if UnknownPlugin is not registered, it would be stored as runtime.Unknown
	// For this example, we'll just show it's stored as RawExtension
	fmt.Printf("Unknown Plugin Raw Data: %s\n", string(unknownRawExtension.Raw))
}

```

--------------------------------

### Validation Actions Example (YAML)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

Demonstrates how to configure multiple validation actions within a ValidatingAdmissionPolicyBinding. This example specifies both 'Warn' and 'Audit' actions to inform clients and log validation failures.

```yaml
validationActions: [Warn, Audit]
```

--------------------------------

### Kubernetes Authorization Configuration Example (YAML)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

An example YAML configuration file for Kubernetes authorization, demonstrating how to define authorization chains with multiple webhooks and parameters. This configuration allows for fine-grained control, including explicit deny rules and pre-filtering with CEL. Note: This is an example and should not be used as-is.

```yaml
---
#
# DO NOT USE THE CONFIG AS IS. THIS IS AN EXAMPLE.

```

--------------------------------

### ZooKeeper Server Startup Command Configuration (Shell)

Source: https://kubernetes.io/docs/tutorials/_print

Demonstrates the shell command used to start ZooKeeper servers within a Kubernetes container. It shows how ZooKeeper's operational parameters, such as server count, data directories, ports, and various tuning settings, are passed as command-line arguments. This ensures consistent configuration for leader election and Zab protocol.

```shell
start-zookeeper \
--servers=3 \
--data_dir=/var/lib/zookeeper/data \
--data_log_dir=/var/lib/zookeeper/data/log \
--conf_dir=/opt/zookeeper/conf \
--client_port=2181 \
--election_port=3888 \
--server_port=2888 \
--tick_time=2000 \
--init_limit=10 \
--sync_limit=5 \
--heap=512M \
--max_client_cnxns=60 \
--snap_retain_count=3 \
--purge_interval=12 \
--max_session_timeout=40000 \
--min_session_timeout=4000 \
--log_level=INFO
```

--------------------------------

### Update Zypper and Install kubectl

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

These commands first update the zypper package manager and confirm the new repository addition, then install the kubectl client. The update step ensures that the package manager is aware of the newly added Kubernetes repository. The zypper install command requires user interaction to accept the GPG key.

```bash
sudo zypper update
sudo zypper install -y kubectl
```

--------------------------------

### Get Documentation for Resource and its Fields

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_explain/_print

Retrieves the documentation for a specified Kubernetes resource and its associated fields. This is a basic usage of the explain command.

```bash
kubectl explain pods
```

--------------------------------

### Kubectl Label Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Illustrative examples demonstrating the usage of the `kubectl label` command for various common tasks. These examples cover adding labels, overwriting existing ones, updating all resources, and using file-based resource identification.

```bash
# Update pod 'foo' with the label 'unhealthy' and the value 'true'
kubectl label pods foo unhealthy=true

# Update pod 'foo' with the label 'status' and the value 'unhealthy', overwriting any existing value
kubectl label --overwrite pods foo status=unhealthy

# Update all pods in the namespace
kubectl label pods --all status=unhealthy

# Update a pod identified by the type and name in "pod.json"
kubectl label -f pod.json status=unhealthy

# Update pod 'foo' only if the resource is unchanged from version 1
kubectl label pods foo status=unhealthy --resource-version=1

# Update pod 'foo' by removing a label named 'bar' if it exists
# Does not require the --overwrite flag
kubectl label pods foo bar-
```

--------------------------------

### Download CRI-O Installer Script (Bash)

Source: https://kubernetes.io/docs/tutorials/cluster-management/kubelet-standalone

Downloads the static binary bundle installation script for the CRI-O container runtime from its GitHub repository. This script simplifies the installation process across different Linux distributions.

```bash
curl https://raw.githubusercontent.com/cri-o/packaging/main/get > crio-install

```

--------------------------------

### Kubelet Flags for Node Self-Registration (Bash)

Source: https://kubernetes.io/docs/concepts/nodes/node

This example shows common command-line flags used when starting a kubelet to enable self-registration with the Kubernetes API server. These flags configure authentication, cloud provider interaction, node IP, and labels.

```bash
# Example kubelet startup options for self-registration:
# --kubeconfig: Path to credentials for API server authentication.
# --cloud-provider: Specifies how to interact with a cloud provider for metadata.
# --register-node: Enables automatic registration with the API server (default is true).
# --register-with-taints: List of taints to apply during registration (e.g., "key=value:effect").
# --node-ip: Optional IP addresses for the node (e.g., "192.168.1.100").
# --node-labels: Labels to add to the node upon registration (e.g., "disktype=ssd,region=us-west-1").
# --node-status-update-frequency: How often the kubelet reports node status (e.g., "10s").
```

--------------------------------

### EndpointSlice with Topology Hints (Kubernetes)

Source: https://kubernetes.io/docs/concepts/services-networking/topology-aware-routing

This example shows an EndpointSlice resource in Kubernetes populated with topology hints. The 'hints.forZones' field indicates the preferred zone for an endpoint, guiding kube-proxy for topology-aware routing.

```yaml
apiVersion: discovery.k8s.io/v1
kind: EndpointSlice
metadata:
  name: example-hints
  labels:
    kubernetes.io/service-name: example-svc
addressType: IPv4
ports:
  - name: http
    protocol: TCP
    port: 80
endpoints:
  - addresses:
      - "10.1.2.3"
    conditions:
      ready: true
    hostname: pod-1
    zone: zone-a
    hints:
      forZones:
        - name: "zone-a"
```

--------------------------------

### Kubernetes Documentation Filename and Path Formatting

Source: https://kubernetes.io/docs/contribute/_print

Demonstrates the correct way to format filenames, directories, and paths in Kubernetes documentation using code style. This ensures clarity and distinguishes these elements from regular text.

```markdown
Open the `envars.yaml` file.
```

```markdown
Go to the `/docs/tutorials` directory.
```

```markdown
Open the `/_data/concepts.yaml` file.
```

--------------------------------

### Install Missing System Binaries (Ubuntu/Debian)

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

Installs the 'ebtables' and 'ethtool' packages on Ubuntu or Debian-based systems. These packages are often required by kubeadm for network configuration and pre-flight checks during installation.

```bash
apt install ebtables ethtool
```

--------------------------------

### Install kubectl Bash Completion on Linux

Source: https://kubernetes.io/docs/reference/kubectl/_print

Provides instructions for installing bash completion for kubectl on Linux. It covers installing the bash-completion package and configuring shell profiles.

```bash
# Installing bash completion on Linux
## If bash-completion is not installed on Linux, install the 'bash-completion' package
## via your distribution's package manager.
## Load the kubectl completion code for bash into the current shell
source <(kubectl completion bash)
## Write bash completion code to a file and source it from .bash_profile
kubectl completion bash > ~/.kube/completion.bash.inc
printf "
# kubectl shell completion
source '$HOME/.kube/completion.bash.inc'
" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

--------------------------------

### Start Kubelet with Configuration File

Source: https://kubernetes.io/docs/tasks/administer-cluster/kubelet-config-file

Command to start the Kubelet process using a configuration file. The `--config` flag points to the path of the Kubelet configuration file. Command-line flags targeting the same values as the config file will override them.

```bash
kubelet --config=/path/to/your/kubelet-config.yaml
```

--------------------------------

### Test kubectl Client Version

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Tests the installed kubectl client version. This command verifies that kubectl is installed and accessible, and shows the client version.

```bash
kubectl version --client
```

--------------------------------

### Kubernetes RBAC RoleBinding LIST API Request (Namespaced)

Source: https://kubernetes.io/docs/reference/kubernetes-api/authorization-resources/role-binding-v1

Example HTTP GET request to list all RoleBindings within a specific namespace. This operation supports various query parameters for filtering and watching resources.

```http
GET /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings
```

--------------------------------

### Kubernetes Impersonation Headers Examples

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

Examples demonstrating the format of impersonation headers used in Kubernetes requests. These headers allow a client to request that the server act as a specific user, group, or with additional attributes.

```text
Impersonate-User: jane.doe@example.com
Impersonate-Group: developers
Impersonate-Group: admins

```

```text
Impersonate-User: jane.doe@example.com
Impersonate-Uid: 06f6ce97-e2c5-4ab8-7ba5-7654dd08d52b
Impersonate-Extra-dn: cn=jane,ou=engineers,dc=example,dc=com
Impersonate-Extra-acme.com%2Fproject: some-project
Impersonate-Extra-scopes: view
Impersonate-Extra-scopes: development

```

--------------------------------

### JWT Authentication with Username Prefixing Failure

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example illustrates a JWT authentication scenario where the username is prefixed with 'system:', causing a validation rule to fail. The `AuthenticationConfiguration` includes a `userValidationRules` that prevents usernames starting with 'system:', resulting in an authentication failure.

```yaml
apiVersion: apiserver.config.k8s.io/v1
kind: AuthenticationConfiguration
jwt:
- issuer:
    url: https://example.com
    audiences:
    - my-app
  claimValidationRules:
  - expression: 'claims.hd == "example.com"'
    message: the hd claim must be set to example.com
  claimMappings:
    username:
      expression: '"system:" + claims.username'
    groups:
      expression: 'claims.roles.split(",")'
    uid:
      expression: 'claims.sub'
    extra:
    - key: 'example.com/tenant'
      valueExpression: 'claims.tenant'
  userValidationRules:
  - expression: "!user.username.startsWith('system:')" # the username will be system:foo and expression will evaluate to false, so validation will fail.
    message: 'username cannot used reserved system: prefix'
```

```json
{
    "username": "system:foo",
    "uid": "auth",
    "groups": [
        "user",
        "admin"
    ],
    "extra": {
        "example.com/tenant": ["72f988bf-86f1-41af-91ab-2d7cd011db4a"]
    }
}
```

--------------------------------

### Install kubectl using apt (Debian/Ubuntu)

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

Installs kubectl on Debian-based systems using the apt package manager. This involves adding the Kubernetes repository and GPG key.

```bash
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
# If the folder `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.35/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.35/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly
sudo apt-get update
sudo apt-get install -y kubectl
```

--------------------------------

### Kubernetes CLI: Get Ingress State

Source: https://kubernetes.io/docs/concepts/services-networking/ingress

Command to retrieve the current state and configuration of a Kubernetes Ingress resource. This helps in verifying the Ingress setup and observing its status, including assigned IP addresses and age.

```bash
kubectl get ingress test-ingress

```

--------------------------------

### Kubectl Create Ingress Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_ingress

Illustrates various scenarios for creating ingress resources, including single and multiple rules, TLS secrets, annotations, default backends, and different path types.

```bash
# Create a single ingress called 'simple' that directs requests to foo.com/bar to svc
# svc1:8080 with a TLS secret "my-cert"kubectl create ingress simple --rule="foo.com/bar=svc1:8080,tls=my-cert"

# Create a catch all ingress of "/path" pointing to service svc:port and Ingress Class as "otheringress"
kubectl create ingress catch-all --class=otheringress --rule="/path=svc:port"

# Create an ingress with two annotations: ingress.annotation1 and ingress.annotations2
kubectl create ingress annotated --class=default --rule="foo.com/bar=svc:port" \
--annotation ingress.annotation1=foo \
--annotation ingress.annotation2=bla

# Create an ingress with the same host and multiple paths
kubectl create ingress multipath --class=default \
--rule="foo.com/=svc:port" \
--rule="foo.com/admin/=svcadmin:portadmin"

# Create an ingress with multiple hosts and the pathType as Prefix
kubectl create ingress ingress1 --class=default \
--rule="foo.com/path*=svc:8080" \
--rule="bar.com/admin*=svc2:http"

# Create an ingress with TLS enabled using the default ingress certificate and different path types
kubectl create ingress ingtls --class=default \
--rule="foo.com/=svc:https,tls" \
--rule="foo.com/path/subpath*=othersvc:8080"

# Create an ingress with TLS enabled using a specific secret and pathType as Prefix
kubectl create ingress ingsecret --class=default \
--rule="foo.com/*=svc:8080,tls=secret1"

# Create an ingress with a default backend
kubectl create ingress ingdefault --class=default \
--default-backend=defaultsvc:http \
--rule="foo.com/*=svc:8080,tls=secret1"
```

--------------------------------

### Get MAC address using ifconfig

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

This command, an alternative to 'ip link', also displays network interface details and MAC addresses. It's used to verify that each node in the Kubernetes cluster has a unique MAC address.

```shell
ifconfig -a

```

--------------------------------

### Install kubectl to User Directory (No Root)

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

Installs kubectl to the user's local bin directory when root access is not available. Requires adding the directory to the PATH environment variable.

```bash
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
# and then append (or prepend) ~/.local/bin to $PATH
```

--------------------------------

### Run Interactive Busybox Pod with kubectl

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

Starts an interactive busybox Pod for debugging purposes. This Pod is temporary and will be removed upon exit. It's useful for running commands directly within a cluster environment.

```bash
kubectl run -it --rm --restart=Never busybox --image=gcr.io/google-containers/busybox sh

```

--------------------------------

### Kubernetes Client-Go Watcher Implementation (Go)

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

Illustrates how to implement the list-then-watch logic using the `Reflector` from the Go client library. This is a common pattern for efficiently tracking resource changes.

```go
package main

import (
	"fmt"
	"k8s.io/client-go/tools/cache"
)

func main() {
	// Example usage of cache.Reflector (details omitted for brevity)
	fmt.Println("Using cache.Reflector for list-then-watch pattern.")
	// reflector := cache.NewReflector(...)
	// go reflector.Run(stopCh)
	// ... process events ...
}
```

--------------------------------

### View kube-proxy Process Information

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

This output shows an example of the `ps auxw | grep kube-proxy` command's result. It details the user, PID, CPU/memory usage, command path, and arguments of the running `kube-proxy` process, aiding in its identification and status check.

```shell
root  4194  0.4  0.1 101864 17696 ?    Sl Jul04  25:43 /usr/local/bin/kube-proxy --master=https://kubernetes-master --kubeconfig=/var/lib/kube-proxy/kubeconfig --v=2
```

--------------------------------

### Example: Create ConfigMap with Specific Keys from Files using kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_configmap

This example shows how to create a ConfigMap named 'my-config' where specific keys ('key1', 'key2') are explicitly assigned to the content of different files ('/path/to/bar/file1.txt', '/path/to/bar/file2.txt'). This allows overriding the default behavior of using filenames as keys.

```bash
kubectl create configmap my-config --from-file=key1=/path/to/bar/file1.txt --from-file=key2=/path/to/bar/file2.txt
```

--------------------------------

### Add Diagram Referral Text (Kubernetes Docs)

Source: https://kubernetes.io/docs/contribute/_print

This snippet provides an example of a diagram referral. It's used within the documentation text to guide readers to a specific diagram. The 'Figure NUMBER' in the referral must match the caption of the corresponding diagram.

```text
Figure 10 depicts the components of the Kubernetes architecture.
The control plane ...

```

--------------------------------

### kubectl scale examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/_print

Demonstrates various ways to use the kubectl scale command, including scaling by replica set name, using a YAML file, setting preconditions, scaling multiple resources, and scaling stateful sets.

```bash
# Scale a replica set named 'foo' to 3
kubectl scale --replicas=3 rs/foo

# Scale a resource identified by type and name specified in "foo.yaml" to 3
kubectl scale --replicas=3 -f foo.yaml

# If the deployment named mysql's current size is 2, scale mysql to 3
kubectl scale --current-replicas=2 --replicas=3 deployment/mysql

# Scale multiple replication controllers
kubectl scale --replicas=5 rc/example1 rc/example2 rc/example3

# Scale stateful set named 'web' to 3
kubectl scale --replicas=3 statefulset/web
```

--------------------------------

### Kubeadm ClusterConfiguration Example

Source: https://kubernetes.io/docs/reference/config-api/_print

Configures cluster-wide settings for `kubeadm init`, including networking, etcd, and control plane component configurations. This ensures consistent cluster behavior.

```yaml
apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
etcd:
  # one of local or external
  local:
    imageRepository: "registry.k8s.io"
    imageTag: "3.2.24"
    dataDir: "/var/lib/etcd"
    extraArgs:
      listen-client-urls: "http://10.100.0.1:2379"
    serverCertSANs:
      -  "ec2-10-100-0-1.compute-1.amazonaws.com"
    peerCertSANs:
      - "10.100.0.1"
  # external:
    # endpoints:
    # - "10.100.0.1:2379"
    # - "10.100.0.2:2379"
    # caFile: "/etcd/kubernetes/pki/etcd/etcd-ca.crt"
    # certFile: "/etc/kubernetes/pki/etcd/etcd.crt"
    # keyFile: "/etc/kubernetes/pki/etcd/etcd.key"
networking:
  serviceSubnet: "10.96.0.0/16"
  podSubnet: "10.244.0.0/24"
  dnsDomain: "cluster.local"
kubernetesVersion: "v1.21.0"
controlPlaneEndpoint: "10.100.0.1:6443"
apiServer:
  extraArgs:
    authorization-mode: "Node,RBAC"
  extraVolumes:
    - name: "some-volume"
      hostPath: "/etc/some-path"
      mountPath: "/etc/some-pod-path"
      readOnly: false
      pathType: File
  certSANs:
    - "10.100.1.1"
    - "ec2-10-100-0-1.compute-1.amazonaws.com"
  timeoutForControlPlane: 4m0s
controllerManager:
  extraArgs:
    "node-cidr-mask-size": "20"
  extraVolumes:
    - name: "some-volume"

```

--------------------------------

### Impersonate Node to Get/List Pods (Kubernetes YAML)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example shows how to grant a ServiceAccount permission to impersonate a specific node to perform actions like getting and listing pods on that node. It involves creating ClusterRoles for impersonation and pod access, and then binding them to the ServiceAccount.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: impersonate-node-sa
rules:
- apiGroups: ["authentication.k8s.io"]
  resources: ["nodes"]
  resourceNames: ["mynode"]
  verbs: ["impersonate:arbitrary-node"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: impersonate-list-pods
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs:
      - "impersonate-on:arbitrary-node:list"
      - "impersonate-on:arbitrary-node:get"
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: impersonate-node-sa
  namespace: default
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: impersonate-node-sa
subjects:
- kind: ServiceAccount
  name: node-impersonator
  namespace: default
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: impersonate-list-pods
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: impersonate-list-pods
subjects:
  - kind: ServiceAccount
    name: node-impersonator
    namespace: default

```

--------------------------------

### Using jq for Regex Matching with Kubernetes Pods

Source: https://kubernetes.io/docs/reference/kubectl/jsonpath

Demonstrates how to achieve regular expression matching for Kubernetes pod names when `kubectl`'s JSONPath does not support it directly. It shows an example of a non-working JSONPath command and provides a working alternative using `kubectl` to get JSON output piped to `jq` for filtering.

```bash
# kubectl does not support regular expressions for JSONpath output
# The following command does not work
kubectl get pods -o jsonpath='{.items[?(@.metadata.name=~/^test$/)].metadata.name}'
```

```bash
# The following command achieves the desired result
kubectl get pods -o json | jq -r '.items[] | select(.metadata.name | test("test-")).metadata.name'
```

--------------------------------

### Kubectl Create Service Account Example

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/_print

This example demonstrates how to create a new service account using the kubectl command-line tool. It specifies the name of the service account to be created.

```bash
kubectl create serviceaccount my-service-account
```

--------------------------------

### Example: Create ConfigMap from Environment File using kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_configmap

This example demonstrates creating a ConfigMap named 'my-config' by reading key-value pairs from one or more environment files. Each line in the specified '.env' files in the format 'KEY=VALUE' will be added to the ConfigMap.

```bash
kubectl create configmap my-config --from-env-file=path/to/foo.env --from-env-file=path/to/bar.env
```

--------------------------------

### Allow reading pods in core API Group (Kubernetes YAML)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example shows a Kubernetes Role rule that grants permissions to 'get', 'list', and 'watch' pod resources within the core API group. It is typically used for read-only access to pods.

```yaml
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

--------------------------------

### kubectl Resource Type Specification Examples

Source: https://kubernetes.io/docs/reference/kubectl

Illustrates how to specify resource types in kubectl commands, showing that singular, plural, and abbreviated forms are accepted. This flexibility aids in command efficiency.

```bash
kubectl get pod pod1
kubectl get pods pod1
kubectl get po pod1
```

--------------------------------

### Example: Delete Kubectl Context

Source: https://kubernetes.io/docs/reference/kubectl/_print

An example demonstrating how to delete a Kubernetes context named 'minikube' using the kubectl command-line tool.

```bash
# Delete the context for the minikube cluster
kubectl config delete-context minikube
```

--------------------------------

### Create Resource Quota with Scopes

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This example shows how to create a resource quota with a specific scope, such as 'BestEffort'. It uses the `kubectl create quota` command with both the `--hard` and `--scopes` flags.

```bash
kubectl create quota best-effort --hard=pods=100 --scopes=BestEffort
```

--------------------------------

### ValidatingWebhookConfiguration Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

Example of a ValidatingWebhookConfiguration specifying the admissionReviewVersions it accepts.

```APIDOC
## POST /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations

### Description
Creates a ValidatingWebhookConfiguration resource.

### Method
POST

### Endpoint
/apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations

### Parameters
#### Request Body
- **apiVersion** (string) - Required - Specifies the API version for the ValidatingWebhookConfiguration.
- **kind** (string) - Required - Must be 'ValidatingWebhookConfiguration'.
- **webhooks** (array) - Required - A list of webhook configurations.
  - **name** (string) - Required - The name of the webhook.
  - **admissionReviewVersions** (array of strings) - Required - The versions of AdmissionReview objects the webhook accepts (e.g., ["v1", "v1beta1"]).

### Request Example
```json
{
  "apiVersion": "admissionregistration.k8s.io/v1",
  "kind": "ValidatingWebhookConfiguration",
  "webhooks": [
    {
      "name": "my-webhook.example.com",
      "admissionReviewVersions": ["v1", "v1beta1"]
    }
  ]
}
```

### Response
#### Success Response (201 Created)
- **metadata** (object) - Contains metadata about the created ValidatingWebhookConfiguration.
- **webhooks** (array) - The list of webhook configurations.

#### Response Example
```json
{
  "apiVersion": "admissionregistration.k8s.io/v1",
  "kind": "ValidatingWebhookConfiguration",
  "metadata": {
    "name": "my-webhook.example.com",
    "creationTimestamp": "2023-10-27T10:00:00Z"
  },
  "webhooks": [
    {
      "name": "my-webhook.example.com",
      "admissionReviewVersions": ["v1", "v1beta1"]
    }
  ]
}
```
```

--------------------------------

### Kubectl Port Forwarding Examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates various ways to use `kubectl port-forward` to forward local ports to ports within Kubernetes pods, services, or deployments. It shows how to specify local and remote ports, target services by name, and listen on different network interfaces.

```bash
# Listen on ports 5000 and 6000 locally, forwarding data to/from ports 5000 and 6000 in the pod
kubectl port-forward pod/mypod 5000 6000

# Listen on ports 5000 and 6000 locally, forwarding data to/from ports 5000 and 6000 in a pod selected by the deployment
kubectl port-forward deployment/mydeployment 5000 6000

# Listen on port 8443 locally, forwarding to the targetPort of the service's port named "https" in a pod selected by the service
kubectl port-forward service/myservice 8443:https

# Listen on port 8888 locally, forwarding to 5000 in the pod
kubectl port-forward pod/mypod 8888:5000

# Listen on port 8888 on all addresses, forwarding to 5000 in the pod
kubectl port-forward --address 0.0.0.0 pod/mypod 8888:5000

# Listen on port 8888 on localhost and selected IP, forwarding to 5000 in the pod
kubectl port-forward --address localhost,10.19.21.23 pod/mypod 8888:5000

# Listen on a random port locally, forwarding to 5000 in the pod
kubectl port-forward pod/mypod :5000
```

--------------------------------

### Enable Pod Events in CRI-O

Source: https://kubernetes.io/docs/tasks/administer-cluster/switch-to-evented-pleg

These examples show how to enable pod event generation in CRI-O, a requirement for Evented PLEG. This can be done by starting the daemon with a flag or by using a drop-in configuration file.

```bash
# Start CRI-O with the flag
--enable-pod-events=true
```

```ini
[crio.runtime]
enable_pod_events: true
```

--------------------------------

### Namespace Selector Example (Kubernetes Admission)

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/mutating-admission-policy-binding-v1alpha1

Demonstrates how to use `namespaceSelector` to define rules for applying admission control policies based on namespace labels. It shows examples for excluding specific 'runlevel' values and including specific 'environment' values.

```yaml
namespaceSelector: |
  {
    "matchExpressions": [
      {
        "key": "runlevel",
        "operator": "NotIn",
        "values": [ "0", "1" ]
      }
    ]
  }
```

```yaml
namespaceSelector: |
  {
    "matchExpressions": [
      {
        "key": "environment",
        "operator": "In",
        "values": [ "prod", "staging" ]
      }
    ]
  }
```

--------------------------------

### Kubernetes kubectl Commands for Label Selection

Source: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels

Provides examples of using `kubectl` commands with label selectors for listing Pods. It shows how to apply both equality-based and set-based selectors, including examples for OR logic and negative matching.

```bash
kubectl get pods -l environment=production,tier=frontend
```

```bash
kubectl get pods -l 'environment in (production),tier in (frontend)'
```

```bash
kubectl get pods -l 'environment in (production, qa)'
```

```bash
kubectl get pods -l 'environment,environment notin (frontend)'
```

--------------------------------

### Install kubectl binary on Windows (curl)

Source: https://kubernetes.io/docs/tasks/tools/_print

Installs the kubectl binary on Windows using curl. This command downloads a specific version of kubectl for Windows amd64 architecture.

```shell
curl.exe -LO "https://dl.k8s.io/release/v1.35.0/bin/windows/amd64/kubectl.exe"
```

--------------------------------

### Execute Multiple Single Commands in a Container

Source: https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container

These examples demonstrate executing various commands like `ps aux`, `ls /`, and `cat /proc/1/mounts` directly within the 'shell-demo' container using `kubectl exec`. This allows for non-interactive inspection of the container's state.

```bash
kubectl exec shell-demo -- ps aux
kubectl exec shell-demo -- ls /
kubectl exec shell-demo -- cat /proc/1/mounts

```

--------------------------------

### Automate Credential Preparation with Kubeadm Phases (External CA Mode)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Demonstrates automating the preparation of component credentials when using an external Certificate Authority (CA) with kubeadm. This involves copying CA files, creating a temporary configuration, and running `kubeadm init phase` commands.

```bash
# Copy external CA files to /etc/kubernetes/pki
# Create config.yaml with relevant cluster information
# Execute kubeadm init phase commands:kubeadm init phase kubeconfig all --config config.yaml
kubeadm init phase certs all --config config.yaml
# Inspect generated files, delete ca.key and super-admin.conf
# On join nodes, delete /etc/kubernetes/kubelet.conf
```

--------------------------------

### Install Kube-Proxy Addon to Kubernetes Cluster

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init-phase

Installs the kube-proxy addon components by interacting with the API server. Similar to CoreDNS installation, this command supports flags for customizing the deployment, including image repository, kubeconfig path, Kubernetes version, and service CIDR.

```bash
kubeadm init phase addon kube-proxy [flags]
```

--------------------------------

### Serve Kubernetes Website Locally with Make (Alternative)

Source: https://kubernetes.io/docs/contribute/new-content/_print

This command serves the Kubernetes website locally using Hugo. It navigates to the website directory within the repository and starts the Hugo development server. This is an alternative to 'make container-serve' if you prefer not to use Docker for local serving.

```bash
cd <path_to_your_repo>/website
make serve
```

--------------------------------

### Define an Optional Secret in a Pod (YAML)

Source: https://kubernetes.io/docs/concepts/configuration/_print

This example demonstrates how to define a Pod that references an optional Secret. If the specified Secret ('mysecret') does not exist, Kubernetes will ignore it and the Pod will still start. This is useful for configurations where a Secret is not strictly required for the Pod's operation.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mypod
    image: redis
    volumeMounts:
    - name: foo
      mountPath: "/etc/foo"
      readOnly: true
  volumes:
  - name: foo
    secret:
      secretName: mysecret
      optional: true
```

--------------------------------

### List Kubernetes Resources from Directory with kustomization using kubectl get

Source: https://kubernetes.io/docs/reference/kubectl/_print

Shows how to list Kubernetes resources defined in a directory using kustomization. This is useful for managing complex configurations with overlays and patches.

```bash
# List resources from a directory with kustomization.yaml - e.g. dir/kustomization.yaml
kubectl get -k dir/
```

--------------------------------

### Kubectl Alpha Kuberc Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Examples demonstrating the usage of the 'kubectl alpha kuberc' command for various customization tasks, including viewing configurations, setting default command flags, and creating command aliases.

```bash
# View the current kuberc configuration
kubectl alpha kuberc view
```

```bash
# Set a default value for a command flag
kubectl alpha kuberc set --section defaults --command get --option output=wide
```

```bash
# Create an alias for a command
kubectl alpha kuberc set --section aliases --name getn --command get --prependarg nodes --option output=wide
```

--------------------------------

### Get Pod IPs with kubectl and Go Template

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

Fetches the IP addresses of Pods matching a label selector using `kubectl` and a Go template. This output is crucial for directly testing network connectivity to individual Pods.

```bash
kubectl get pods -l app=hostnames \
    -o go-template='{{range .items}}{{.status.podIP}}{{"\n"}}{{end}}'

```

--------------------------------

### Create and Manage Kubernetes Deployments and Pods

Source: https://kubernetes.io/docs/tutorials/cluster-management/namespaces-walkthrough

Demonstrates applying a deployment manifest and then retrieving information about the created deployments and pods. It also shows switching contexts and creating resources in a different namespace.

```bash
kubectl apply -f https://k8s.io/examples/admin/snowflake-deployment.yaml

kubectl get deployment

kubectl get pods -l app=snowflake

kubectl config use-context prod

kubectl create deployment cattle --image=registry.k8s.io/serve_hostname --replicas=5

kubectl get deployment

kubectl get pods -l app=cattle

```

--------------------------------

### Define Kubectl Alias with Prepend Arguments

Source: https://kubernetes.io/docs/reference/kubectl/kuberc

This example extends the previous alias definition by introducing 'prependArgs'. This allows specifying arguments that will be inserted immediately after the kubectl command and its subcommand. In this case, 'namespace' is prepended, resulting in commands like 'kubectl get namespace test-ns --output json'.

```yaml
apiVersion: kubectl.config.k8s.io/v1beta1
kind: Preference
alias:
  - name: getn
    command: get
    options:
      - name: output
        default: json
    prependArgs:
      - namespace
```

--------------------------------

### Correct Reserved Memory Configuration with Static Policy (YAML)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This YAML configuration demonstrates a correct setup for reserved memory when using the `Static` Memory Manager policy. It includes `kubeReserved`, `systemReserved`, and `reservedMemory` settings, ensuring that the total reserved memory accounts for the default `evictionHard` threshold. This configuration is necessary for the Memory Manager to start correctly.

```yaml
# this snippet relies on the default value of evictionHard
memoryManagerPolicy: StatickubeReserved: { cpu: "4", memory: "4Gi" }
systemReserved: { cpu: "1", memory: "1Gi" }
reservedMemory:
  - numaNode: 0
    limits:
      memory: "3Gi"
  - numaNode: 1
    limits:
      memory: "2148Mi" # 3GiB minus 100MiB
```

--------------------------------

### i18n TOML File Example

Source: https://kubernetes.io/docs/contribute/style/_print

Provides examples of `i18n` TOML files showing how heading strings are translated. The `[whatsnext_heading]` key maps to the `other` field, which contains the localized text for the 'What's next' heading.

```TOML
[whatsnext_heading]
other = "What's next"
```

```TOML
[whatsnext_heading]
other = "다음 내용"
```

--------------------------------

### Install Missing System Binaries (CentOS/Fedora)

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

Installs the 'ebtables' and 'ethtool' packages on CentOS or Fedora-based systems. These packages are often required by kubeadm for network configuration and pre-flight checks during installation.

```bash
yum install ebtables ethtool
```

--------------------------------

### Install kubectl using Yum

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

This command installs the kubectl client using the yum package manager. It requires the Kubernetes yum repository to be configured beforehand. The `-y` flag automatically confirms any prompts during the installation process.

```bash
sudo yum install -y kubectl
```

--------------------------------

### Get Node Name Using Downward API (Kubernetes YAML)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This snippet shows how to inject the node name into a pod's environment using the Downward API. This is often used by agents or controllers running on a node to identify their own node, for example, when configuring impersonation.

```yaml
env:
- name: MY_NODE_NAME
  valueFrom:
    fieldRef:
      fieldPath: spec.nodeName

```

--------------------------------

### kubectl run Examples: Environment Variables and Labels

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/_print

Illustrates how to set environment variables and labels for a pod during its creation using `kubectl run`. This allows for dynamic configuration and easier identification of pods.

```bash
# Start a hazelcast pod and set environment variables "DNS_DOMAIN=cluster" and "POD_NAMESPACE=default" in the container
kubectl run hazelcast --image=hazelcast/hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"

# Start a hazelcast pod and set labels "app=hazelcast" and "env=prod" in the container
kubectl run hazelcast --image=hazelcast/hazelcast --labels="app=hazelcast,env=prod"
```

--------------------------------

### Get Specific ResourceClaim Details in YAML

Source: https://kubernetes.io/docs/tutorials/cluster-management/install-use-dra

This command fetches the detailed YAML representation of a specific ResourceClaim named 'some-gpu'. The output includes the 'status' stanza, which contains information about the allocated device and the Pod it is reserved for.

```bash
kubectl get resourceclaim some-gpu -n dra-tutorial -o yaml
```

--------------------------------

### Create ClusterIP Service with Dry-Run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This example demonstrates creating a ClusterIP service with the `--dry-run` flag set to 'server'. This flag allows you to preview the Kubernetes object that would be created without actually persisting it to the cluster. The output format can be controlled using the `-o` or `--output` flag.

```bash
kubectl create service clusterip my-cs --tcp=5678:8080 --dry-run=server -o yaml
```

--------------------------------

### Configure Mutating Webhook with URL

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example shows how to configure a mutating webhook to call a specific URL. It expects the TLS certificate to be verified using system trust roots and does not specify a custom CA bundle. The `url` field must start with 'https://'.

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: MutatingWebhookConfiguration
webhooks:
- name: my-webhook.example.com
  clientConfig:
    url: "https://my-webhook.example.com:9443/my-webhook-path"
```

--------------------------------

### Create Kubernetes Configuration File

Source: https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters

Manually create a new Kubernetes configuration file. This example demonstrates defining a new context within a basic Config structure.

```yaml
apiVersion: v1
kind: Config
preferences: {}

contexts:
- context:
    cluster: development
    namespace: ramp
    user: developer
  name: dev-ramp-up
```

--------------------------------

### Inspect Kubernetes Service Configuration

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

This command retrieves the detailed configuration of a Kubernetes Service in JSON format. It's used to verify `spec.ports`, `targetPort`, `protocol`, and `selector` fields against the Pod definitions to ensure correct Service setup.

```bash
kubectl get service hostnames -o json

```

--------------------------------

### Kubeadm Join Phase Kubelet Start

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-join-phase

This phase is responsible for writing kubelet settings, generating necessary certificates, and restarting the kubelet service. It ensures the kubelet is correctly configured and running on the node.

```bash
kubeadm join phase kubelet-start
```

--------------------------------

### Kubernetes Probe Event Example

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes

An example of Kubernetes events generated by a kubelet during readiness probe failures, specifically showing a 'ProbeWarning' for excessive redirects.

```text
Events:
  Type     Reason        Age                     From               Message
  ----     ------        ----                    ----               -------
  Normal   Scheduled     29m                     default-scheduler  Successfully assigned default/httpbin-7b8bc9cb85-bjzwn to daocloud
  Normal   Pulling       29m                     kubelet            Pulling image "docker.io/kennethreitz/httpbin"
  Normal   Pulled        24m                     kubelet            Successfully pulled image "docker.io/kennethreitz/httpbin" in 5m12.402735213s
  Normal   Created       24m                     kubelet            Created container httpbin
  Normal   Started       24m                     kubelet            Started container httpbin
 Warning  ProbeWarning  4m11s (x1197 over 24m)  kubelet            Readiness probe warning: Probe terminated redirects

```

--------------------------------

### Install kubectl on Fedora/CentOS/RHEL using yum

Source: https://kubernetes.io/docs/tasks/tools/_print

Installs kubectl on RPM-based systems using yum. It adds the Kubernetes yum repository configuration and then installs kubectl.

```bash
# This overwrites any existing configuration in /etc/yum.repos.d/kubernetes.repo
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/repodata/repomd.xml.key
EOF
sudo yum install -y kubectl
```

--------------------------------

### CEL Apply Configuration Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/mutating-admission-policy-v1beta1

This example demonstrates how to create an apply configuration using CEL to set a single field within an object's spec.

```APIDOC
## Apply Configuration with CEL

### Description
Use CEL expressions to define apply configurations for Kubernetes resources. This allows for declarative setting of object fields.

### Method
Not Applicable (This describes a configuration language, not an API endpoint)

### Endpoint
Not Applicable

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None (This is a CEL expression)

### Request Example
```cel
Object{
  spec: Object.spec{
    serviceAccountName: "example"
  }
}
```

### Response
#### Success Response (200)
None (This is a configuration definition)

#### Response Example
None
```

--------------------------------

### Install Go Packages for OpenAPI Spec Handling

Source: https://kubernetes.io/docs/contribute/_print

Installs required Go packages for handling OpenAPI specifications. These packages are used by the reference-docs generation tool.

```go
go get -u github.com/go-openapi/loads
go get -u github.com/go-openapi/spec

```

--------------------------------

### Example: Delete Minikube User

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_config/_print

An example demonstrating how to delete the 'minikube' user from the kubeconfig file using the kubectl command.

```bash
# Delete the minikube user
kubectl config delete-user minikube
```

--------------------------------

### Deploy and Manage Kubernetes Job (kubectl)

Source: https://kubernetes.io/docs/concepts/workloads/_print

These commands demonstrate how to deploy a Kubernetes Job from a YAML configuration file, check its status, and retrieve detailed information about it. The `kubectl apply` command initiates the Job, `kubectl describe job` provides a comprehensive overview, and `kubectl get job -o yaml` shows the Job's full specification in YAML format.

```bash
# Apply the Job configuration
kubectl apply -f https://kubernetes.io/examples/controllers/job.yaml

# Check the status of the Job
kubectl describe job pi

# Get the Job's full specification in YAML format
kubectl get job pi -o yaml

```

--------------------------------

### Impersonate Node to Get/List Pods (Kubernetes RBAC)

Source: https://kubernetes.io/docs/reference/access-authn-authz/user-impersonation

This example illustrates how to configure RBAC for a service account to impersonate a specific node. This allows the service account to perform actions like getting and listing pods as if it were the node itself. It utilizes ClusterRoles and ClusterRoleBindings.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: impersonate-node-sa
rules:
- apiGroups: ["authentication.k8s.io"]
  resources: ["nodes"]
  resourceNames: ["mynode"]
  verbs: ["impersonate:arbitrary-node"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: impersonate-list-pods
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs:
      - "impersonate-on:arbitrary-node:list"
      - "impersonate-on:arbitrary-node:get"
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: impersonate-node-sa
  namespace: default
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: impersonate-node-sa
subjects:
- kind: ServiceAccount
  name: node-impersonator
  namespace: default
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: impersonate-list-pods
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: impersonate-list-pods
subjects:
  - kind: ServiceAccount
    name: node-impersonator
    namespace: default
```

--------------------------------

### Creating Custom Resources (Shirts)

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/_print

This example shows how to create instances of the 'Shirt' custom resource, defining their specific color and size.

```APIDOC
## Create Shirt Custom Resources

### Description
Creates multiple 'Shirt' custom resources with different color and size specifications.

### Method
`kubectl apply`

### Endpoint
`customresourcedefinition/shirt-resources.yaml`

### Request Body
```yaml
---
apiVersion: stable.example.com/v1
kind: Shirt
metadata:
  name: example1
spec:
  color: blue
  size: S
---
apiVersion: stable.example.com/v1
kind: Shirt
metadata:
  name: example2
spec:
  color: blue
  size: M
---
apiVersion: stable.example.com/v1
kind: Shirt
metadata:
  name: example3
spec:
  color: green
  size: M
```

### Response Example
(Output of `kubectl apply` command, typically indicating success or failure of resource creation.)
```

--------------------------------

### Clone Kubernetes Repository using Go

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/contribute-upstream

This snippet demonstrates how to clone the upstream Kubernetes repository using the `go get` command. It assumes Go and Git are installed and GOPATH is set. The output is the cloned repository located within the GOPATH.

```bash
mkdir $GOPATH/src
cd $GOPAPTH/src
go get github.com/kubernetes/kubernetes
```

--------------------------------

### Example DNS Name to IP Mapping for Control Plane Endpoint

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

An example illustrating how a DNS name can be mapped to an IP address for the `--control-plane-endpoint` argument in `kubeadm init`. This is useful for setting up a stable endpoint for the control plane, especially in high-availability scenarios.

```text
192.168.0.102 cluster-endpoint
```

--------------------------------

### Example: Create Global Default Priority Class

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example shows how to create a PriorityClass that is designated as the global default. This class will be used for pods that do not explicitly specify a priority.

```bash
# Create a priority class named default-priority that is considered as the global default prioritykubectl create priorityclass default-priority --value=1000 --global-default=true --description="default priority"
```

--------------------------------

### Kubectl Top Pod Command Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_top/_print

Demonstrates how to use the 'kubectl top pod' command to display resource usage for pods. It covers showing metrics for all pods, pods in a specific namespace, pods with labels, and individual pods with their containers.

```bash
# Show metrics for all pods in the default namespacekubectl top pod

# Show metrics for all pods in the given namespacekubectl top pod --namespace=NAMESPACE

# Show metrics for a given pod and its containerskubectl top pod POD_NAME --containers

# Show metrics for the pods defined by label name=myLabelkubectl top pod -l name=myLabel
```

--------------------------------

### Kubernetes Headless Service YAML Output (SingleStack)

Source: https://kubernetes.io/docs/concepts/services-networking/dual-stack

This is an example output of `kubectl get svc my-service -o yaml` for a headless Service with selectors that has been configured with `SingleStack` ipFamilyPolicy after dual-stack was enabled on the cluster. It shows `clusterIP` set to `None` and the relevant dual-stack configuration fields.

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/name: MyApp
  name: my-service
spec:
  clusterIP: None
  clusterIPs:
  - None
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app.kubernetes.io/name: MyApp

```

--------------------------------

### Install Bash Completion on macOS

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl

Installs bash completion for kubectl on macOS. It provides different commands depending on the installed Bash version. If kubectl was installed via Homebrew, completion should work immediately. Otherwise, manual addition to the completion directory might be necessary.

```bash
brew install bash-completion

```

```bash
brew install bash-completion@2

```

```bash
kubectl completion bash > $(brew --prefix)/etc/bash_completion.d/kubectl

```

--------------------------------

### Install CoreDNS Addon to Kubernetes Cluster

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init-phase

Installs the CoreDNS addon components by interacting with the API server. Note that CoreDNS will not be scheduled until the CNI is installed. This command accepts various flags to customize the installation, such as specifying an image repository, kubeconfig file, Kubernetes version, and service CIDR.

```bash
kubeadm init phase addon coredns [flags]
```

--------------------------------

### Get ServiceAccount YAML Configuration

Source: https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin

Retrieves the YAML configuration of a specified ServiceAccount within a given namespace. This is useful for inspecting the ServiceAccount's details, including its associated secrets and annotations. It requires kubectl to be installed and configured to access the Kubernetes cluster.

```bash
kubectl -n examplens get serviceaccount/example-automated-thing -o yaml
```

--------------------------------

### Example kubeadm join Command

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

An example of the `kubeadm join` command used to add worker nodes to an already initialized Kubernetes cluster. This command requires the control-plane host address, a token, and a discovery token CA certificate hash.

```bash
kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

--------------------------------

### Execute Commands Inside the Container Shell

Source: https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container

These examples demonstrate running various commands within the interactive shell established in the 'shell-demo' container. They include listing directory contents, inspecting system files, and installing/running network and process utilities.

```bash
# Run this inside the container
ls /
cat /proc/mounts
cat /proc/1/maps
apt-get update
apt-get install -y tcpdump
tcpdump
apt-get install -y lsof
lsof
apt-get install -y procps
ps aux
ps aux | grep nginx

```

--------------------------------

### Locally Test API Reference (Makefile)

Source: https://kubernetes.io/docs/contribute/_print

This command publishes a local version of the API reference documentation for verification. It requires updating git submodules if they haven't been already, and then uses `make container-serve` to start a local server.

```bash
cd <web-base>
git submodule update --init --recursive --depth 1 # if not already done
make container-serve
```

--------------------------------

### Run Pod using Kubelet Static Manifest

Source: https://kubernetes.io/docs/tutorials/cluster-management/_print

Creates a Pod manifest file for a simple Nginx web server and copies it to the kubelet's staticPodPath. This demonstrates how to run pods in standalone mode using static manifests.

```bash
cat <<EOF > static-web.yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-web
spec:
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP
EOF
sudo cp static-web.yaml /etc/kubernetes/manifests/
```

--------------------------------

### Apply and Check Fine-Grained Pod Status (kubectl)

Source: https://kubernetes.io/docs/tutorials/security/seccomp

These kubectl commands apply the fine-grained seccomp Pod manifest and check its status. `kubectl apply` creates the Pod, and `kubectl get pod` confirms that it starts successfully, indicated by a `Running` status.

```bash
kubectl apply -f https://k8s.io/examples/pods/security/seccomp/ga/fine-pod.yaml

kubectl get pod fine-pod

```

--------------------------------

### Kubectl Create ClusterIP Service Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

These examples demonstrate how to create a ClusterIP service. The first example shows creating a service named 'my-cs' with port 5678 mapped to target port 8080. The second example illustrates creating a headless service by setting the clusterip to 'None'.

```bash
# Create a new ClusterIP service named my-cskubectl create service clusterip my-cs --tcp=5678:8080

# Create a new ClusterIP service named my-cs (in headless mode)kubectl create service clusterip my-cs --clusterip="None"
```

--------------------------------

### Configure Subordinate IDs for Kubelet User in Linux

Source: https://kubernetes.io/docs/concepts/workloads/pods/_print

This example shows the configuration for `/etc/subuid` and `/etc/subgid` files on a Linux node to support user namespaces for the `kubelet` user. It specifies the subordinate ID range, ensuring it starts at 65536 and has a count sufficient for the maximum number of pods.

```shell
# The format is
#   name:firstID:count of IDs
# where
# - firstID is 65536 (the minimum value possible)
# - count of IDs is 110 * 65536
#   (110 is the default limit for number of pods on the node)

kubelet:65536:7208960

```

--------------------------------

### Example Pod Manifest (BestEffort QoS - Custom Devices)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This Pod manifest runs in the 'BestEffort' QoS class as it lacks CPU and memory requests. It specifies requests and limits for two custom devices, example.com/deviceA and example.com/deviceB.

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      limits:
        example.com/deviceA: "1"
        example.com/deviceB: "1"
      requests:
        example.com/deviceA: "1"
        example.com/deviceB: "1"

```

--------------------------------

### Clean Up kubectl Convert Installation Files

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Removes the downloaded `kubectl convert` binary and its checksum file after successful installation. This helps in keeping the system clean.

```shell
rm kubectl-convert kubectl-convert.sha256
```

--------------------------------

### Install Bash Completion on macOS (Homebrew)

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

Installs bash completion for kubectl on macOS using Homebrew. It provides two options depending on the Bash version installed.

```bash
brew install bash-completion

```

```bash
brew install bash-completion@2

```

--------------------------------

### Execute Command in Existing Pod with kubectl

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

Executes a specified command within a running Pod. This is useful for inspecting the state or running diagnostic tools inside a Pod without starting a new interactive session. Requires Pod name and optionally container name.

```bash
kubectl exec <POD-NAME> -c <CONTAINER-NAME> -- <COMMAND>

```

--------------------------------

### Kubeadm Flags Environment File Example

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/kubelet-integration

This snippet shows the format of the `/var/lib/kubelet/kubeadm-flags.env` file, which contains arguments passed to the Kubelet during startup. It includes dynamic parameters like cgroup driver and other flags.

```bash
KUBELET_KUBEADM_ARGS="--flag1=value1 --flag2=value2 ..."

```

--------------------------------

### Kubernetes Scheduler Configuration Example

Source: https://kubernetes.io/docs/concepts/scheduling-eviction/_print

An example Kubernetes scheduler configuration snippet demonstrating how to set the `percentageOfNodesToScore` parameter to 50%. This configuration is part of the `KubeSchedulerConfiguration`.

```yaml
apiVersion: kubescheduler.config.k8s.io/v1alpha1
kind: KubeSchedulerConfiguration
algorithmSource:
  provider: DefaultProvider

...

percentageOfNodesToScore: 50

```

--------------------------------

### CEL Apply Configuration Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/_print

This example demonstrates how to create an apply configuration using CEL to set a single field within an object's spec.

```APIDOC
## Apply Configuration with CEL

### Description
Use CEL expressions to define apply configurations for Kubernetes resources. This allows for declarative setting of object fields.

### Method
N/A (This describes a configuration language, not an HTTP method)

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
CEL expressions are used within the configuration.

### Request Example
```cel
Object{
  spec: Object.spec{
    serviceAccountName: "example"
  }
}
```

### Response
#### Success Response (200)
N/A (This describes a configuration language)

#### Response Example
N/A
```

--------------------------------

### Start kubectl Proxy

Source: https://kubernetes.io/docs/tutorials/kubernetes-basics/_print

Starts a proxy server to access Kubernetes API objects. This is essential for interacting with Pods from your local machine.

```bash
kubectl proxy

```

--------------------------------

### Example TopologyInfo Population in Device Plugin

Source: https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/_print

Illustrates how a device plugin can populate the TopologyInfo struct with NUMA node information for a specific device. This example shows setting the device ID, health status, and NUMA node affinity.

```go
pluginapi.Device{ID: "25102017", Health: pluginapi.Healthy, Topology:&pluginapi.TopologyInfo{Nodes: []*pluginapi.NUMANode{&pluginapi.NUMANode{ID: 0,},}}}

```

--------------------------------

### Install Website Dependencies with npm

Source: https://kubernetes.io/docs/contribute/new-content/_print

This command installs the necessary Node.js dependencies for the Kubernetes website project. It ensures that all required packages are downloaded and configured correctly for local development. Run this after cloning the repository.

```bash
npm ci
```

--------------------------------

### Create a Pod with a Shell-Accessible Container

Source: https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container

This YAML defines a Kubernetes Pod named 'shell-demo' with a single nginx container. It includes an emptyDir volume mounted for potential data persistence within the container's lifecycle. This setup is a prerequisite for demonstrating shell access.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: shell-demo
spec:
  volumes:
  - name: shared-data
    emptyDir: {}
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: shared-data
      mountPath: /usr/share/nginx/html
  hostNetwork: true
  dnsPolicy: Default

```

--------------------------------

### Describe Web Service

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

This command provides detailed information about the 'web-tcp' service, including its type, IP address, ports, and endpoints. This is useful for understanding how to access the service externally.

```bash
kubectl describe svc web-tcp

```

--------------------------------

### Start a Kubernetes Deployment

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/http-proxy-access-api

This command deploys a sample 'hello-app' application to your Kubernetes cluster. It requires `kubectl` to be configured and a running Kubernetes cluster.

```bash
kubectl create deployment hello-app --image=gcr.io/google-samples/hello-app:2.0 --port=8080

```

--------------------------------

### Example: Create Priority Class with Preemption Policy

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example illustrates creating a PriorityClass with a specific preemption policy. The 'Never' policy prevents pods of this priority from preempting pods with lower priority.

```bash
# Create a priority class named high-priority that cannot preempt pods with lower prioritykubectl create priorityclass high-priority --value=1000 --description="high priority" --preemption-policy="Never"
```

--------------------------------

### Generate CA and Server Certificates with easyrsa

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This snippet demonstrates how to initialize easyrsa, build a Certificate Authority (CA), and generate a server certificate and key. It requires downloading and unpacking the easyrsa3 tool. The output includes the CA certificate, server certificate, and server key, which are then used to configure the API server.

```bash
curl -LO https://dl.k8s.io/easy-rsa/easy-rsa.tar.gz
tar xzf easy-rsa.tar.gz
cd easy-rsa-master/easyrsa3
./easyrsa init-pki

./easyrsa --batch "--req-cn=${MASTER_IP}@`date +%s`" build-ca nopass

./easyrsa --subject-alt-name="IP:${MASTER_IP},"\
"IP:${MASTER_IP},"\
"DNS:kubernetes,"\
"DNS:kubernetes.default,"\
"DNS:kubernetes.default.svc,"\
"DNS:kubernetes.default.svc.cluster,"\
"DNS:kubernetes.default.svc.cluster.local" \
--days=10000 \
build-server-full server nopass
```

--------------------------------

### Install apt Packages for Kubernetes Repository (Debian/Ubuntu)

Source: https://kubernetes.io/docs/setup/_print

Installs necessary packages for using the Kubernetes apt repository on Debian-based systems. This includes updating the package index and installing `apt-transport-https`, `ca-certificates`, `curl`, and `gpg`.

```bash
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

```

--------------------------------

### Kubernetes Version Sorting Example

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definition-versioning

Illustrates the sorting order of Kubernetes versions based on the defined algorithm. This helps understand how kubectl determines the default version for accessing custom resources.

```text
- v10
- v2
- v1
- v11beta2
- v10beta3
- v3beta1
- v12alpha1
- v11alpha2
- foo1
- foo10

```

--------------------------------

### Kubernetes API Server Authentication Configuration File Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/authentication

An example of a Kubernetes AuthenticationConfiguration file. This structured file allows for detailed configuration of API server authentication. Ensure to review and amend this example for your specific cluster security requirements.

```yaml
---
#
# CAUTION: this is an example configuration.
#          Check and amend this before you use it in your own cluster!
#
apiVersion: apiserver.config.k8s.io/v1
kind: AuthenticationConfiguration
anonymous:
  enabled: false

```

--------------------------------

### Install and Configure CRI-O (Bash)

Source: https://kubernetes.io/docs/tutorials/cluster-management/kubelet-standalone

Executes the downloaded CRI-O installation script with root privileges. This script installs CRI-O, CNI plugins, and container runtimes like crun and runc, and configures them.

```bash
sudo bash crio-install

```

--------------------------------

### Kubernetes Authorizer: Resource Check Example (Create Pods)

Source: https://kubernetes.io/docs/reference/using-api/_print

An example CEL expression to check if the current principal is allowed to create pods in the 'default' namespace.

```CEL
authorizer.group('').resource('pods').namespace('default').check('create').allowed()
```

--------------------------------

### Example: Watch Deployment Rollout Status

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example demonstrates how to use the 'kubectl rollout status' command to monitor the rollout status of a Kubernetes deployment named 'nginx'.

```bash
# Watch the rollout status of a deployment
kubectl rollout status deployment/nginx
```

--------------------------------

### Get Go dependencies for Kubernetes documentation

Source: https://kubernetes.io/docs/contribute/_print

Fetches essential Go packages required for Kubernetes documentation generation using the `go get` command. This includes packages for command-line flags, Cobra CLI framework, YAML parsing, and reference documentation tools.

```bash
go get -u github.com/spf13/pflag
go get -u github.com/spf13/cobra
go get -u gopkg.in/yaml.v2
go get -u github.com/kubernetes-sigs/reference-docs
```

--------------------------------

### Examine kube-proxy Log Entries

Source: https://kubernetes.io/docs/tasks/debug/debug-application/debug-service

This is an example of `kube-proxy` log output, which can be accessed via files like `/var/log/kube-proxy.log` or `journalctl`. It provides insights into the proxy's operations, including the mode it's running in (e.g., iptables) and endpoint synchronization status. Errors in these logs can indicate connectivity or configuration problems.

```shell
I1027 22:14:53.995134    5063 server.go:200] Running in resource-only container "/kube-proxy"
I1027 22:14:53.998163    5063 server.go:247] Using iptables Proxier.
I1027 22:14:54.038140    5063 proxier.go:352] Setting endpoints for "kube-system/kube-dns:dns-tcp" to [10.244.1.3:53]
I1027 22:14:54.038164    5063 proxier.go:352] Setting endpoints for "kube-system/kube-dns:dns" to [10.244.1.3:53]
I1027 22:14:54.038209    5063 proxier.go:352] Setting endpoints for "default/kubernetes:https" to [10.240.0.2:443]
I1027 22:14:54.038238    5063 proxier.go:429] Not syncing iptables until Services and Endpoints have been received from master
I1027 22:14:54.040048    5063 proxier.go:294] Adding new service "default/kubernetes:https" at 10.0.0.1:443/TCP
I1027 22:14:54.040154    5063 proxier.go:294] Adding new service "kube-system/kube-dns:dns" at 10.0.0.10:53/UDP
I1027 22:14:54.040223    5063 proxier.go:294] Adding new service "kube-system/kube-dns:dns-tcp" at 10.0.0.10:53/TCP
```

--------------------------------

### Kubernetes Resource Labeling Examples

Source: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels

Demonstrates how to apply labels to Kubernetes resources, such as pods, to categorize them. Examples show labeling for multi-tier applications like 'guestbook', distinguishing frontend and backend tiers, and master/replica roles for Redis.

```yaml
labels:
  app: guestbook
  tier: frontend
```

```yaml
labels:
  app: guestbook
  tier: backend
  role: master
```

```yaml
labels:
  app: guestbook
  tier: backend
  role: replica
```

--------------------------------

### Add Diagram Caption using Markdown (Inline Mermaid)

Source: https://kubernetes.io/docs/contribute/style/diagram-guide

This example shows how to add a diagram caption when using the Inline Mermaid method. Simple Markdown text is used directly below the diagram to provide a caption. This method is suitable for diagrams defined directly within the documentation using Mermaid syntax.

```markdown
Figure 4. Kubernetes Architecture Components

```

--------------------------------

### Install bash-completion v2 using Homebrew

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

This command installs bash-completion version 2, which is required for kubectl autocompletion on Bash 4.1+. It also provides instructions to add the necessary sourcing to the .bash_profile.

```bash
brew install bash-completion@2
```

--------------------------------

### List Available Plugins

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

The `kubectl plugin list` command lists all available kubectl plugins found on the user's PATH. Plugins must be executable and start with `kubectl-`. The `name-only` flag can be used to display only the binary names.

```bash
kubectl plugin list
```

--------------------------------

### Kubernetes Label Selector Examples

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/validating-admission-policy-binding-v1

Examples demonstrating how to use LabelSelectors for namespace and object selection in Kubernetes admission control policies. These selectors allow fine-grained control over which objects or namespaces the policy should apply to.

```yaml
namespaceSelector: {
  matchExpressions: [
    {
      key: "runlevel",
      operator: "NotIn",
      values: [ "0", "1" ]
    }
  ]
}
objectSelector: {
  matchExpressions: [
    {
      key: "environment",
      operator: "In",
      values: [ "prod", "staging" ]
    }
  ]
}
```

--------------------------------

### Mermaid Sequence Diagram: K8s System Flow

Source: https://kubernetes.io/docs/contribute/style/diagram-guide

This Mermaid code generates a sequence diagram illustrating the system flow for starting a container in Kubernetes. It depicts the interactions between various control plane components (api-server, etcd, controller-manager, scheduler) and node components (kubelet, container runtime) initiated by a user action.

```mermaid
%%{init:{"theme":"neutral"}}%%
sequenceDiagram
    actor me
    participant apiSrv as control plane<br><br>api-server
    participant etcd as control plane<br><br>etcd datastore
    participant cntrlMgr as control plane<br><br>controller<br>manager
    participant sched as control plane<br><br>scheduler
    participant kubelet as node<br><br>kubelet
    participant container as node<br><br>container<br>runtime
    me->>apiSrv: 1. kubectl create -f pod.yaml
    apiSrv-->>etcd: 2. save new state
    cntrlMgr->>apiSrv: 3. check for changes
    sched->>apiSrv: 4. watch for unassigned pods(s)
    apiSrv->>sched: 5. notify about pod w nodename=" "
    sched->>apiSrv: 6. assign pod to node
    apiSrv-->>etcd: 7. save new state
    kubelet->>apiSrv: 8. look for newly assigned pod(s)
    apiSrv->>kubelet: 9. bind pod to node
    kubelet->>container: 10. start container
    kubelet->>apiSrv: 11. update pod status
    apiSrv-->>etcd: 12. save new state

```

--------------------------------

### Apply and Manage Pod using Kubectl (Shell)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

These shell commands demonstrate the lifecycle management of a Kubernetes Pod. 'kubectl apply' creates the Pod from a YAML file, 'kubectl get pod' checks its status, 'kubectl describe pod' provides detailed information and events (useful for diagnosing scheduling issues), and 'kubectl delete pod' removes the Pod. Finally, 'kubectl delete namespace' cleans up the entire example environment.

```shell
kubectl apply -f https://k8s.io/examples/pods/resource/cpu-request-limit-2.yaml --namespace=cpu-example

```

```shell
kubectl get pod cpu-demo-2 --namespace=cpu-example

```

```shell
kubectl describe pod cpu-demo-2 --namespace=cpu-example

```

```shell
kubectl delete pod cpu-demo-2 --namespace=cpu-example

```

```shell
kubectl delete namespace cpu-example

```

--------------------------------

### Container Readiness and Startup Probes

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Details on configuring readiness and startup probes for containers. Readiness probes determine if a container is ready to serve traffic, while startup probes ensure initialization completes successfully before other probes are executed.

```APIDOC
## Container Probes

### Description
Manages the lifecycle of containers within a Pod, ensuring services are ready to receive traffic and handling initial startup conditions.

### Readiness Probe
- **startupProbe** (Probe) - Required - Indicates that the Pod has successfully initialized. If specified, no other probes are executed until this completes successfully. If this probe fails, the Pod will be restarted.

### Liveness Probe
- **livenessProbe** (Probe) - Optional - Periodic probe of container service readiness. Container will be removed from service endpoints if the probe fails. Cannot be updated.

### Endpoint
N/A (Configuration within Pod specification)

### Request Example
```json
{
  "containers": [
    {
      "name": "my-container",
      "image": "my-image",
      "readinessProbe": {
        "httpGet": {
          "path": "/healthz",
          "port": 8080
        },
        "initialDelaySeconds": 5,
        "periodSeconds": 10
      },
      "startupProbe": {
        "httpGet": {
          "path": "/startup",
          "port": 8080
        },
        "initialDelaySeconds": 15,
        "periodSeconds": 20
      }
    }
  ]
}
```

### Response
#### Success Response (200)
N/A (Probe results are internal to Kubernetes)

#### Response Example
N/A
```

--------------------------------

### Add Kubernetes APT Repository and Install Packages (Debian/Ubuntu)

Source: https://kubernetes.io/docs/setup/production-environment/_print

This snippet adds the Kubernetes APT repository to the system and then updates the package index to install kubelet, kubeadm, and kubectl. It also pins their versions to prevent automatic upgrades.

```bash
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.35/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

# Update the apt package index, install kubelet, kubeadm and kubectl, and pin their version:
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

# (Optional) Enable the kubelet service before running kubeadm:
sudo systemctl enable --now kubelet
```

--------------------------------

### Install Kompose on macOS using Homebrew

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

Install the latest release of Kompose on macOS using the Homebrew package manager. This is a convenient method for macOS users, simplifying the installation process and dependency management.

```shell
brew install kompose
```

--------------------------------

### Install Containerd on Windows

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Downloads and installs the Containerd runtime on a Windows machine. This script is part of the process for adding Windows worker nodes to a kubeadm cluster. Ensure you replace `CONTAINERD_VERSION` with a valid version number.

```powershell
curl.exe -LO https://raw.githubusercontent.com/kubernetes-sigs/sig-windows-tools/master/hostprocess/Install-Containerd.ps1
./Install-Containerd.ps1 -ContainerDVersion CONTAINERD_VERSION
```

--------------------------------

### Install CNI Plugins

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Downloads and installs the Container Network Interface (CNI) plugins, which are essential for pod networking in Kubernetes. This script specifies the version and architecture of the plugins and installs them into the `/opt/cni/bin` directory.

```shell
CNI_PLUGINS_VERSION="v1.3.0"
ARCH="amd64"
DEST="/opt/cni/bin"
sudo mkdir -p "$DEST"
curl -L "https://github.com/containernetworking/plugins/releases/download/${CNI_PLUGINS_VERSION}/cni-plugins-linux-${ARCH}-${CNI_PLUGINS_VERSION}.tgz" | sudo tar -C "$DEST" -xz
```

--------------------------------

### Kubectl Apply Command Examples

Source: https://kubernetes.io/docs/reference/kubectl

Provides examples for the 'kubectl apply' command, which is used to create or update resources from YAML or JSON files. It covers applying single files, multiple files, and all files within a directory.

```bash
# Apply a service definition from a file
kubectl apply -f example-service.yaml

# Apply a replication controller definition from a file
kubectl apply -f example-controller.yaml

# Apply all YAML/JSON files in a directory
kubectl apply -f <directory>
```

--------------------------------

### Kubectl Get Command Synopsis

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/_print

This is the general syntax for the kubectl get command. It outlines the available output formats, resource types, and filtering options. It's crucial for understanding how to retrieve and format Kubernetes resource information.

```bash
kubectl get [(-o|--output=)json|yaml|kyaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file|custom-columns|custom-columns-file|wide] (TYPE[.VERSION][.GROUP] [NAME | -l label] | TYPE[.VERSION][.GROUP]/NAME ...) [flags]
```

--------------------------------

### Use Haskell Kubernetes Client with Kubeconfig

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Demonstrates how to use the Haskell Kubernetes client, including setting up the client configuration with a kubeconfig file and dispatching a request to list all pods across namespaces.

```haskell
exampleWithKubeConfig :: IO ()
exampleWithKubeConfig = do
    oidcCache <- atomically $ newTVar $ Map.fromList []
    (mgr, kcfg) <- mkKubeClientConfig oidcCache $ KubeConfigFile "/path/to/kubeconfig"
    dispatchMime
            mgr
            kcfg
            (CoreV1.listPodForAllNamespaces (Accept MimeJSON))
        >>= print

```

--------------------------------

### Install Kubernetes Packages (YUM/DNF)

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Installs `kubelet`, `kubeadm`, and `kubectl` using the YUM or DNF package manager. The `--disableexcludes=kubernetes` or `--setopt=disable_excludes=kubernetes` option ensures that the packages from the Kubernetes repository are installed correctly.

```shell
# For systems with DNF:
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

# For systems with DNF5:
sudo yum install -y kubelet kubeadm kubectl --setopt=disable_excludes=kubernetes
```

--------------------------------

### Print Kubeadm Default Configurations (Shell)

Source: https://kubernetes.io/docs/reference/config-api/_print

Commands to print the default configurations for 'init' and 'join' actions in kubeadm. These defaults can be used as a starting point for creating custom configuration files.

```shell
kubeadm config print init-defaults

```

```shell
kubeadm config print join-defaults

```

--------------------------------

### Create ConfigMap from Multiple Environment Files using kubectl

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Starting with Kubernetes v1.23, you can specify the --from-env-file argument multiple times to create a ConfigMap from several data sources. This example demonstrates creating a ConfigMap named 'config-multi-env-files' from two different environment property files. The resulting ConfigMap merges data from all specified files.

```bash
kubectl create configmap config-multi-env-files \
        --from-env-file=configure-pod-container/configmap/game-env-file.properties \
        --from-env-file=configure-pod-container/configmap/ui-env-file.properties

kubectl get configmap config-multi-env-files -o yaml
```

--------------------------------

### kubeadm init phase addon coredns

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init-phase

Installs the CoreDNS addon components via the API server. Note that the DNS server will not be scheduled until CNI is installed.

```APIDOC
## kubeadm init phase addon coredns

### Description
Install the CoreDNS addon components via the API server. Please note that although the DNS server is deployed, it will not be scheduled until CNI is installed.

### Method
POST (implied by installation action)

### Endpoint
/apis/kubeadm.k8s.io/v1beta3/namespaces/kube-system/configmaps/kubeadm-config/phases/addon/coredns/apply

### Parameters
#### Query Parameters
- **dry-run** (string) - Optional - Don't apply any changes; just output what would be done.
- **feature-gates** (string) - Optional - A set of key=value pairs that describe feature gates for various features.
- **print-manifest** (boolean) - Optional - Print the addon manifests to STDOUT instead of installing them

#### Request Body
- **config** (string) - Optional - Path to a kubeadm configuration file.
- **image-repository** (string) - Optional - Choose a container registry to pull control plane images from. Default: "registry.k8s.io"
- **kubeconfig** (string) - Optional - The kubeconfig file to use when talking to the cluster. Default: "/etc/kubernetes/admin.conf"
- **kubernetes-version** (string) - Optional - Choose a specific Kubernetes version for the control plane. Default: "stable-1"
- **service-cidr** (string) - Optional - Use alternative range of IP address for service VIPs. Default: "10.96.0.0/12"
- **service-dns-domain** (string) - Optional - Use alternative domain for services, e.g. "myorg.internal". Default: "cluster.local"
- **rootfs** (string) - Optional - The path to the 'real' host root filesystem. This will cause kubeadm to chroot into the provided path.

### Request Example
```json
{
  "config": "/path/to/kubeadm-config.yaml",
  "image-repository": "myregistry.com/k8s",
  "kubernetes-version": "v1.28.0",
  "service-cidr": "10.100.0.0/16",
  "service-dns-domain": "mydomain.local"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates the success of the operation.

#### Response Example
```json
{
  "status": "CoreDNS addon installed successfully."
}
```
```

--------------------------------

### Configure emptyDir Volume with Memory Limit (YAML)

Source: https://kubernetes.io/docs/concepts/storage/volumes

This example demonstrates how to configure an emptyDir volume to use memory as its medium, with a specified size limit. This is useful for ephemeral storage that requires faster access.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: registry.k8s.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir:
      sizeLimit: 500Mi
      medium: Memory

```

--------------------------------

### Install Kubernetes Apt Repository Prerequisites (Debian/Ubuntu)

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

This command updates the apt package index and installs necessary packages for using the Kubernetes apt repository on Debian-based systems.

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

```

--------------------------------

### Create ConfigMap from File

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to create a ConfigMap from files or directories. You can specify individual files with custom keys or let Kubernetes use the filename as the key.

```APIDOC
## POST /api/v1/namespaces/{namespace}/configmaps

### Description
Creates a new ConfigMap resource in a specified Kubernetes namespace.

### Method
POST

### Endpoint
`/api/v1/namespaces/{namespace}/configmaps`

### Parameters
#### Path Parameters
- **namespace** (string) - Required - The namespace for the ConfigMap.

#### Query Parameters
- **dry-run** (string) - Optional - Specifies the dry-run mode (e.g., "client", "server").
- **field-manager** (string) - Optional - Name of the manager used to track field ownership.

#### Request Body
- **metadata** (object) - Required - Contains the name and labels for the ConfigMap.
  - **name** (string) - Required - The name of the ConfigMap.
  - **namespace** (string) - Optional - The namespace of the ConfigMap.
- **data** (object) - Optional - Key-value pairs representing the ConfigMap data.
- **binaryData** (object) - Optional - Key-value pairs representing binary ConfigMap data.

### Request Example
```json
{
  "apiVersion": "v1",
  "kind": "ConfigMap",
  "metadata": {
    "name": "my-config"
  },
  "data": {
    "key1": "value1",
    "key2": "value2"
  }
}
```

### Response
#### Success Response (201 Created)
- **metadata** (object) - Information about the created ConfigMap.
- **data** (object) - The data stored in the ConfigMap.
- **binaryData** (object) - The binary data stored in the ConfigMap.

#### Response Example
```json
{
  "apiVersion": "v1",
  "kind": "ConfigMap",
  "metadata": {
    "name": "my-config",
    "namespace": "default",
    "creationTimestamp": "2023-10-27T10:00:00Z"
  },
  "data": {
    "key1": "value1",
    "key2": "value2"
  }
}
```
```

--------------------------------

### InitConfiguration

Source: https://kubernetes.io/docs/reference/config-api/_print

Contains initialization-specific runtime information for 'kubeadm init', used only during the initial cluster setup.

```APIDOC
## InitConfiguration

### Description
InitConfiguration contains a list of elements that is specific "kubeadm init"-only runtime information. These fields are solely used the first time `kubeadm init` runs.

### Method
N/A (This is a configuration object definition)

### Endpoint
N/A

### Parameters
#### Fields
- **apiVersion** (string) - `kubeadm.k8s.io/v1beta3` - API version.
- **kind** (string) - `InitConfiguration` - Kind of the configuration.
- **bootstrapTokens** ([]BootstrapToken) - A set of Bootstrap Tokens to create during `kubeadm init`.
- **nodeRegistration** (`NodeRegistrationOptions`) - Holds fields related to registering the new control-plane node to the cluster.
- **localAPIEndpoint** (`APIEndpoint`) - Represents the endpoint of the API server instance deployed on this control plane node.
- **certificateKey** (string) - Sets the key with which certificates and keys are encrypted prior to being uploaded in a Secret.
- **skipPhases** ([]string) - A list of phases to skip during command execution.
- **patches** (`Patches`) - Contains options related to applying patches to components deployed by kubeadm during `kubeadm init`.
```

--------------------------------

### List Available kubectl Plugins

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl

Lists all available kubectl plugins found on the user's PATH. Plugins must be executable and start with 'kubectl-'. The 'name-only' flag can be used to display only the binary names.

```bash
kubectl plugin list
kubectl plugin list --name-only
```

--------------------------------

### Kubelet Configuration with Hairpin Mode

Source: https://kubernetes.io/docs/tasks/debug/debug-application/_print

This is an example output of the 'ps auxw | grep kubelet' command, showing the Kubelet process and its arguments. Notably, it includes the '--hairpin-mode=promiscuous-bridge' flag, indicating how the Kubelet is configured to handle traffic that loops back to its source via a Service.

```shell
root      3392  1.1  0.8 186804 65208 ?        Sl   00:51  11:11 /usr/local/bin/kubelet --enable-debugging-handlers=true --config=/etc/kubernetes/manifests --allow-privileged=true --v=4 --cluster-dns=10.0.0.10 --cluster-domain=cluster.local --configure-cbr0=true --cgroup-root=/ --system-cgroups=/system --hairpin-mode=promiscuous-bridge --runtime-cgroups=/docker-daemon --kubelet-cgroups=/kubelet --babysit-daemons=true --max-pods=110 --serialize-image-pulls=false --outofdisk-transition-frequency=0
```

--------------------------------

### Device Attribute and Capacity Access Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/extend-resources/_print

This example demonstrates how to access device attributes and capacities using a specific expression syntax. It shows how to reference driver, model, family, and module information, and includes a robust approach to checking for attribute existence before referencing them. The `cel.bind()` function is also shown for simplifying expressions.

```CEL
device.driver
device.attributes["dra.example.com"].model
device.attributes["ext.example.com"].family
device.capacity["dra.example.com"].modules

cel.bind(dra, device.attributes["dra.example.com"], dra.someBool && dra.anotherBool)
```

--------------------------------

### List PriorityClasses using Kubernetes API Client (Go)

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/_print

Demonstrates how to list all PriorityClass objects using the Kubernetes Go client library. It initializes a clientset and then calls the List method on the schedulingV1().PriorityClasses() resource.

```go
package main

import (
	"context"
	"fmt"
	"log"

	metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
	schedulingv1 "k8s.io/client-go/kubernetes/typed/scheduling/v1"
	"k8s.io/client-go/tools/clientcmd"
)

func main() {
	// Load Kubernetes configuration
	config, err := clientcmd.BuildConfigFromFlags("", clientcmd.RecommendedHomeFile)
	if err != nil {
		log.Fatalf("Error building kubeconfig: %s", err.Error())
	}

	// Create a Kubernetes clientset
	clientset, err := schedulingv1.NewForConfig(config)
	if err != nil {
		log.Fatalf("Error creating clientset: %s", err.Error())
	}

	// List PriorityClasses
	pcs, err := clientset.PriorityClasses().List(context.TODO(), metav1.ListOptions{})
	if err != nil {
		log.Fatalf("Error listing PriorityClasses: %s", err.Error())
	}

	fmt.Println("PriorityClasses:")
	for _, pc := range pcs.Items {
		fmt.Printf("- %s (Value: %d)\n", pc.Name, pc.Value)
	}
}
```

--------------------------------

### Start a Hazelcast pod exposing a port using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts a Hazelcast pod and configures it to expose port 5701. This is useful for services that require specific network ports to be accessible.

```bash
kubectl run hazelcast --image=hazelcast/hazelcast --port=5701
```

--------------------------------

### Start a Hazelcast pod with environment variables using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl

This command starts a Hazelcast pod and sets environment variables within the container. This is useful for configuring application behavior without modifying the container image. Dependencies include kubectl and a Kubernetes cluster.

```bash
kubectl run hazelcast --image=hazelcast/hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"

```

--------------------------------

### Install kubectl Bash Completion on macOS

Source: https://kubernetes.io/docs/reference/kubectl/_print

Installs bash completion for kubectl on macOS using Homebrew. It handles different Bash versions and integrates with the kubectl installation.

```bash
# Installing bash completion on macOS using homebrew
## If running Bash 3.2 included with macOS
brew install bash-completion
## or, if running Bash 4.1+
brew install bash-completion@2
## If kubectl is installed via homebrew, this should start working immediately
## If you've installed via other means, you may need add the completion to your completion directory
kubectl completion bash > $(brew --prefix)/etc/bash_completion.d/kubectl
```

--------------------------------

### Deprecated CustomResourceDefinition (v1beta1) Example (YAML)

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definition-versioning

An older YAML example of a CustomResourceDefinition using apiextensions.k8s.io/v1beta1, marking versions as deprecated. This demonstrates the structure for deprecation warnings in an earlier Kubernetes API version.

```yaml
# Deprecated in v1.16 in favor of apiextensions.k8s.io/v1
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: crontabs.example.com
spec:
  group: example.com
  names:
    plural: crontabs
    singular: crontab
    kind: CronTab
  scope: Namespaced
  validation: ...
  versions:
  - name: v1alpha1
    served: true
    storage: false
    # This indicates the v1alpha1 version of the custom resource is deprecated.
    # API requests to this version receive a warning header in the server response.
    deprecated: true
    # This overrides the default warning returned to API clients making v1alpha1 API requests.
    deprecationWarning: "example.com/v1alpha1 CronTab is deprecated; see http://example.com/v1alpha1-v1 for instructions to migrate to example.com/v1 CronTab"
  - name: v1beta1
    served: true
    # This indicates the v1beta1 version of the custom resource is deprecated.
    # API requests to this version receive a warning header in the server response.
    # A default warning message is returned for this version.
    deprecated: true
  - name: v1
    served: true
    storage: true

```

--------------------------------

### Kubernetes EncryptionConfiguration Example

Source: https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data

An example of an EncryptionConfiguration file for Kubernetes. This configuration specifies resources to encrypt (secrets, configmaps, etc.) and the encryption providers to use, such as AES-CBC with a specified key or an identity provider for fallback.

```yaml
---
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
      - configmaps
      - pandas.awesome.bears.example
    providers:
      - aescbc:
          keys:
            - name: key1
              # See the following text for more details about the secret value
              secret: <BASE 64 ENCODED SECRET>
      - identity: {} # this fallback allows reading unencrypted secrets;
                     # for example, during initial migration

```

--------------------------------

### Kubectl Apply: Creating Resources from Standard Input

Source: https://kubernetes.io/docs/reference/kubectl/_print

Shows how to create multiple Kubernetes resources, including Pods and Secrets, by piping YAML definitions to `kubectl apply -f -`. This method is useful for dynamic resource creation or when defining resources inline.

```bash
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: busybox-sleep
spec:
  containers:
  - name: busybox
    image: busybox:1.28
    args:
    - sleep
    - "1000000"
---
apiVersion: v1
kind: Pod
metadata:
  name: busybox-sleep-less
spec:
  containers:
  - name: busybox
    image: busybox:1.28
    args:
    - sleep
    - "1000"
EOF

kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  password: $(echo -n "s33msi4" | base64 -w0)
  username: $(echo -n "jane" | base64 -w0)
EOF
```

--------------------------------

### Install kubectl with Macports

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Installs kubectl on macOS using the Macports package manager. This method is suitable for users who prefer or use Macports.

```bash
sudo port selfupdate
sudo port install kubectl
```

--------------------------------

### Kubeadm Join Configuration Example

Source: https://kubernetes.io/docs/reference/config-api/_print

Example of a Kubernetes JoinConfiguration object used with `kubeadm join --config`. This configuration specifies runtime settings for joining a node to a cluster, including discovery methods and node registration details.

```yaml
apiVersion: kubeadm.k8s.io/v1beta3
kind: JoinConfiguration
  ...
```

--------------------------------

### Install kubectl with Homebrew

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Installs kubectl on macOS using the Homebrew package manager. This is a convenient method for users who already use Homebrew.

```bash
brew install kubectl
```

```bash
brew install kubernetes-cli
```

--------------------------------

### Example: Create ConfigMap from Literal Key-Value Pairs using kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_configmap

This example illustrates creating a ConfigMap named 'my-config' using direct literal key-value pairs. 'key1' is assigned the value 'config1', and 'key2' is assigned the value 'config2'.

```bash
kubectl create configmap my-config --from-literal=key1=config1 --from-literal=key2=config2
```

--------------------------------

### List Pods using Java Kubernetes client

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Demonstrates using the Java Kubernetes client to load an out-of-cluster kubeconfig file and list all pods in the cluster. It requires the `kubernetes-client` library.

```java
package io.kubernetes.client.examples;

import io.kubernetes.client.ApiClient;
import io.kubernetes.client.ApiException;
import io.kubernetes.client.Configuration;
import io.kubernetes.client.apis.CoreV1Api;
import io.kubernetes.client.models.V1Pod;
import io.kubernetes.client.models.V1PodList;
import io.kubernetes.client.util.ClientBuilder;
import io.kubernetes.client.util.KubeConfig;
import java.io.FileReader;
import java.io.IOException;

/**
 * A simple example of how to use the Java API from an application outside a kubernetes cluster
 *
 * <p>Easiest way to run this: mvn exec:java
 * -Dexec.mainClass="io.kubernetes.client.examples.KubeConfigFileClientExample"
 *
 */
public class KubeConfigFileClientExample {
  public static void main(String[] args) throws IOException, ApiException {

    // file path to your KubeConfig
    String kubeConfigPath = "~/.kube/config";

    // loading the out-of-cluster config, a kubeconfig from file-system
    ApiClient client =
        ClientBuilder.kubeconfig(KubeConfig.loadKubeConfig(new FileReader(kubeConfigPath))).build();

    // set the global default api-client to the in-cluster one from above
    Configuration.setDefaultApiClient(client);

    // the CoreV1Api loads default api-client from global configuration.
    CoreV1Api api = new CoreV1Api();

    // invokes the CoreV1Api client
    V1PodList list = api.listPodForAllNamespaces(null, null, null, null, null, null, null, null, null);
    System.out.println("Listing all pods: ");
    for (V1Pod item : list.getItems()) {
      System.out.println(item.getMetadata().getName());
    }
  }
}

```

--------------------------------

### Get VolumeAttributesClass (HTTP GET)

Source: https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/volume-attributes-class-v1

Retrieves a specific VolumeAttributesClass by its name using an HTTP GET request. The name of the VolumeAttributesClass is specified as a path parameter.

```http
GET /apis/storage.k8s.io/v1/volumeattributesclasses/my-volume-attributes-class
Host: kubernetes.default.svc
Accept: application/json
```

--------------------------------

### Kubeadm ClusterConfiguration Example (YAML)

Source: https://kubernetes.io/docs/reference/config-api/_print

Configures cluster-wide settings for `kubeadm init`, including networking, etcd, and control plane component configurations. This is used for settings that apply to the entire cluster.

```yaml
apiVersion: kubeadm.k8s.io/v1beta4
kind: ClusterConfiguration
etcd:

  # one of local or external
  local:
    imageRepository: "registry.k8s.io"
    imageTag: "3.2.24"
    dataDir: "/var/lib/etcd"
    extraArgs:
      - name: listen-client-urls
        value: http://10.100.0.1:2379
    extraEnvs:
      - name: SOME_VAR
        value: SOME_VALUE
    serverCertSANs:
      - ec2-10-100-0-1.compute-1.amazonaws.com
    peerCertSANs:
      - 10.100.0.1
  # external:
  #   endpoints:
  #     - 10.100.0.1:2379
  #     - 10.100.0.2:2379
  #   caFile: "/etcd/kubernetes/pki/etcd/etcd-ca.crt"
  #   certFile: "/etcd/kubernetes/pki/etcd/etcd.crt"
  #   keyFile: "/etcd/kubernetes/pki/etcd/etcd.key"

networking:
  serviceSubnet: "10.96.0.0/16"
  podSubnet: "10.244.0.0/24"
  dnsDomain: "cluster.local"
kubernetesVersion: "v1.21.0"
controlPlaneEndpoint: "10.100.0.1:6443"
apiServer:
  extraArgs:
    - name: authorization-mode
      value: Node,RBAC
  extraEnvs:
    - name: SOME_VAR
      value: SOME_VALUE
  extraVolumes:
    - name: "some-volume"
      hostPath: "/etc/some-path"

```

--------------------------------

### Apply Kubernetes Deployment (kubectl)

Source: https://kubernetes.io/docs/tutorials/_print

This command applies the Kubernetes deployment configuration from the specified URL. It creates the Deployment and associated ReplicaSet, launching five pods running the Hello World application.

```bash
kubectl apply -f https://k8s.io/examples/service/load-balancer-example.yaml

```

--------------------------------

### Create Resource Quota with Hard Limits

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This example demonstrates how to create a new resource quota with specified hard limits for CPU, memory, pods, and other resources. The command utilizes the `kubectl create quota` command with the `--hard` flag.

```bash
kubectl create quota my-quota --hard=cpu=1,memory=1G,pods=2,services=3,replicationcontrollers=2,resourcequotas=1,secrets=5,persistentvolumeclaims=10
```

--------------------------------

### Example: Kubectl Create Job from CronJob

Source: https://kubernetes.io/docs/reference/kubectl/_print

Shows how to create a new Kubernetes job based on the configuration of an existing cron job.

```bash
# Create a job from a cron job named "a-cronjob"
kubectl create job test-job --from=cronjob/a-cronjob
```

--------------------------------

### Enable Node Authorizer and NodeRestriction (Command Line)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

These command-line examples demonstrate how to enable the Node authorizer and the NodeRestriction admission plugin for the Kubernetes API server. The first example shows enabling the Node authorizer using the --authorization-mode flag, while the second enables the NodeRestriction admission plugin using --enable-admission-plugins.

```bash
kube-apiserver --authorization-mode=...,Node --other-options --more-options

```

```bash
kube-apiserver --enable-admission-plugins=...,NodeRestriction,...

```

--------------------------------

### Configure Kubelet with Web-Hosted Manifest URL (Bash)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/static-pod

This example shows how to configure the kubelet on Fedora to use a web-hosted static Pod manifest. The `--manifest-url` argument points to the URL of the manifest file.

```bash
KUBELET_ARGS="--cluster-dns=10.254.0.10 --cluster-domain=kube.local --manifest-url=<manifest-url>"
```

--------------------------------

### Role Binding Creation Usage (kubectl)

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This provides the general usage syntax for the `kubectl create rolebinding` command. It outlines the required arguments (NAME) and optional flags for specifying cluster roles, roles, users, groups, service accounts, and dry-run behavior.

```bash
kubectl create rolebinding NAME --clusterrole=NAME|--role=NAME [--user=username] [--group=groupname] [--serviceaccount=namespace:serviceaccountname] [--dry-run=server|client|none]

```

--------------------------------

### Kubernetes Memory Manager State File Example

Source: https://kubernetes.io/docs/tasks/debug/debug-cluster/topology

An example JSON structure representing the memory manager state file found at `/var/lib/kubelet/memory_manager_state` on a Kubernetes node. It details NUMA node configurations, memory allocations, and pod entries.

```json
{
   "policyName":"Static",
   "machineState":{
      "0":{
         "numberOfAssignments":1,
         "memoryMap":{
            "hugepages-1Gi":{
               "total":0,
               "systemReserved":0,
               "allocatable":0,
               "reserved":0,
               "free":0
            },
            "memory":{
               "total":134987354112,
               "systemReserved":3221225472,
               "allocatable":131766128640,
               "reserved":131766128640,
               "free":0
            }
         },
         "nodes":[
            0,
            1
         ]
      },
      "1":{
         "numberOfAssignments":1,
         "memoryMap":{
            "hugepages-1Gi":{
               "total":0,
               "systemReserved":0,
               "allocatable":0,
               "reserved":0,
               "free":0
            },
            "memory":{
               "total":135286722560,
               "systemReserved":2252341248,
               "allocatable":133034381312,
               "reserved":29295144960,
               "free":103739236352
            }
         },
         "nodes":[
            0,
            1
         ]
      }
   },
   "entries":{
      "fa9bdd38-6df9-4cf9-aa67-8c4814da37a8":{
         "guaranteed":[
            {
               "numaAffinity":[
                  0,
                  1
               ],
               "type":"memory",
               "size":161061273600
            }
         ]
      }
   },
   "checksum":4142013182
}

```

--------------------------------

### Set Download Directory for Binaries

Source: https://kubernetes.io/docs/setup/_print

This snippet defines and creates a directory where command-line tools like kubeadm and kubelet will be downloaded. It's important to set this to a writable location, with a specific recommendation for Flatcar Container Linux.

```bash
DOWNLOAD_DIR="/usr/local/bin"
sudo mkdir -p "$DOWNLOAD_DIR"
```

--------------------------------

### Kubectl Get

Source: https://kubernetes.io/docs/reference/kubectl/_print

Documentation for the `kubectl get` command, used to list one or more resources.

```APIDOC
## kubectl get

### Description

List one or more resources. This command retrieves and displays information about Kubernetes resources.

### Method

`kubectl get`

### Endpoint

N/A (Command-line interface)

### Parameters

#### Query Parameters

- **<resource_type>** (string) - Required - The type of resource to list (e.g., pods, services, replicationcontrollers).
- **-o <output_format>** (string) - Optional - Specifies the output format (e.g., wide, json, yaml).
- **--field-selector=<field_selector>** (string) - Optional - Select resources based on a field selector.

### Request Example

```bash
# List all pods in plain-text output format.
kubectl get pods

# List all pods in plain-text output format and include additional information (such as node name).
kubectl get pods -o wide

# List the replication controller with the specified name in plain-text output format. Tip: You can shorten and replace the 'replicationcontroller' resource type with the alias 'rc'.
kubectl get replicationcontroller <rc-name>

# List all replication controllers and services together in plain-text output format.
kubectl get rc,services

# List all daemon sets in plain-text output format.
kubectl get ds

# List all pods running on node server01
kubectl get pods --field-selector=spec.nodeName=server01
```

### Response

#### Success Response (List of resources)

- **Resource List** (string) - A table or formatted list of the requested resources and their details.

#### Response Example

```text
NAME          READY   STATUS    RESTARTS   AGE
pod-1         1/1     Running   0          1m
pod-2         1/1     Running   0          2m
```
```

--------------------------------

### Kubernetes kubectl logs Examples

Source: https://kubernetes.io/docs/reference/kubectl/_print

This snippet showcases various ways to fetch logs from pods and containers using kubectl. It covers filtering by pod name, deployment, labels, and includes options for streaming logs, showing previous logs, limiting output size, and adding timestamps.

```bash
# Return snapshot logs from pod nginx with only one container
kubectl logs nginx

# Return snapshot logs from pod nginx, prefixing each line with the source pod and container name
kubectl logs nginx --prefix

# Return snapshot logs from pod nginx, limiting output to 500 bytes
kubectl logs nginx --limit-bytes=500

# Return snapshot logs from pod nginx, waiting up to 20 seconds for it to start running.
kubectl logs nginx --pod-running-timeout=20s

# Return snapshot logs from pod nginx with multi containers
kubectl logs nginx --all-containers=true

# Return snapshot logs from all pods in the deployment nginx
kubectl logs deployment/nginx --all-pods=true

# Return snapshot logs from all containers in pods defined by label app=nginx
kubectl logs -l app=nginx --all-containers=true

# Return snapshot logs from all pods defined by label app=nginx, limiting concurrent log requests to 10 pods
kubectl logs -l app=nginx --max-log-requests=10

# Return snapshot of previous terminated ruby container logs from pod web-1
kubectl logs -p -c ruby web-1

# Begin streaming the logs from pod nginx, continuing even if errors occur
kubectl logs nginx -f --ignore-errors=true

# Begin streaming the logs of the ruby container in pod web-1
kubectl logs -f -c ruby web-1

# Begin streaming the logs from all containers in pods defined by label app=nginx
kubectl logs -f -l app=nginx --all-containers=true

# Display only the most recent 20 lines of output in pod nginx
kubectl logs --tail=20 nginx

# Show all logs from pod nginx written in the last hour
kubectl logs --since=1h nginx

# Show all logs with timestamps from pod nginx starting from August 30, 2024, at 06:00:00 UTC
kubectl logs nginx --since-time=2024-08-30T06:00:00Z --timestamps=true

# Show logs from a kubelet with an expired serving certificate
kubectl logs --insecure-skip-tls-verify-backend nginx

# Return snapshot logs from first container of a job named hello
kubectl logs job/hello

# Return snapshot logs from container nginx-1 of a deployment named nginx
kubectl logs deployment/nginx -c nginx-1
```

--------------------------------

### Example: Set Deployment Service Account

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example demonstrates how to set the service account for a specific deployment named 'nginx-deployment' to 'serviceaccount1'.

```bash
# Set deployment nginx-deployment's service account to serviceaccount1
kubectl set serviceaccount deployment nginx-deployment serviceaccount1
```

--------------------------------

### Configure Kubectl User Credentials

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_config/_print

These examples show how to set various authentication credentials for a Kubernetes user entry using `kubectl config set-credentials`. This includes setting client keys, basic auth, embedding certificates, and configuring different auth providers like GCP and OIDC. It also covers setting up exec plugins with arguments and environment variables.

```bash
# Set only the "client-key" field on the "cluster-admin"
# entry, without touching other values
kubectl config set-credentials cluster-admin --client-key=~/.kube/admin.key

# Set basic auth for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --username=admin --password=uXFGweU9l35qcif

# Embed client certificate data in the "cluster-admin" entry
kubectl config set-credentials cluster-admin --client-certificate=~/.kube/admin.crt --embed-certs=true

# Enable the Google Compute Platform auth provider for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --auth-provider=gcp

# Enable the OpenID Connect auth provider for the "cluster-admin" entry with additional arguments
kubectl config set-credentials cluster-admin --auth-provider=oidc --auth-provider-arg=client-id=foo --auth-provider-arg=client-secret=bar

# Remove the "client-secret" config value for the OpenID Connect auth provider for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --auth-provider=oidc --auth-provider-arg=client-secret-

# Enable new exec auth plugin for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --exec-command=/path/to/the/executable --exec-api-version=client.authentication.k8s.io/v1beta1

# Enable new exec auth plugin for the "cluster-admin" entry with interactive mode
kubectl config set-credentials cluster-admin --exec-command=/path/to/the/executable --exec-api-version=client.authentication.k8s.io/v1beta1 --exec-interactive-mode=Never

# Define new exec auth plugin arguments for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --exec-arg=arg1 --exec-arg=arg2

# Create or update exec auth plugin environment variables for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --exec-env=key1=val1 --exec-env=key2=val2

# Remove exec auth plugin environment variables for the "cluster-admin" entry
kubectl config set-credentials cluster-admin --exec-env=var-to-remove-
```

--------------------------------

### Kubernetes CLI: `kubectl auth whoami` Output Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/authentication

Example output from the `kubectl auth whoami` command, showing the authenticated user's username and groups.

```text
  ATTRIBUTE         VALUE
  Username          george.boole
  Groups            [system:authenticated]
```

--------------------------------

### Example: Set Labels for Deployment Creation

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_set/_print

Illustrates setting labels for a Deployment before its creation. This example uses dry-run and YAML output to pipe resources through kubectl commands for labeling.

```bash
kubectl create deployment my-dep --image=nginx -o yaml --dry-run=client | kubectl label --local -f - environment=qa -o yaml | kubectl create -f -
```

--------------------------------

### Device Plugin Workflow

Source: https://kubernetes.io/docs/concepts/extend-kubernetes/_print

The general workflow for a device plugin involves initialization, starting a gRPC service, registering with the kubelet, and serving requests.

```APIDOC
## Device Plugin Workflow

### Description
This section details the sequential steps a device plugin must follow to operate within the Kubernetes environment, from initial setup to ongoing operation and handling restarts.

### Workflow Steps:
1.  **Initialization**: Perform vendor-specific initialization and ensure devices are ready.
2.  **Start gRPC Service**: Launch a gRPC service using a Unix socket at `/var/lib/kubelet/device-plugins/`. This service implements the `DevicePlugin` interface.
3.  **Register with Kubelet**: Register the plugin with the kubelet via the Unix socket at `/var/lib/kubelet/device-plugins/kubelet.sock`. **Crucially, the gRPC service must be serving before registration.**
4.  **Serving Mode**: After successful registration, the plugin monitors device health, reports state changes to the kubelet, and handles `Allocate` gRPC requests. During allocation, it may perform device-specific preparations and returns `AllocateResponse` containing container runtime configurations.

### Handling Kubelet Restarts:
- A device plugin must detect kubelet restarts.
- When a new kubelet instance starts, it removes existing Unix sockets under `/var/lib/kubelet/device-plugins/`.
- The device plugin can monitor for the deletion of its Unix socket and re-register itself with the new kubelet instance.
```

--------------------------------

### Create Kubernetes Ingress with kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/_print

These examples demonstrate how to create Kubernetes Ingress resources using the `kubectl create ingress` command. They cover scenarios such as simple routing, TLS configuration, multiple hosts and paths, and default backends. The `--rule` flag is used to define host and path mappings to services, and options like `--class`, `--annotation`, and `--default-backend` allow for further customization.

```bash
# Create a single ingress called 'simple' that directs requests to foo.com/bar to svc
# svc1:8080 with a TLS secret "my-cert"
kubectl create ingress simple --rule="foo.com/bar=svc1:8080,tls=my-cert"

# Create a catch all ingress of "/path" pointing to service svc:port and Ingress Class as "otheringress"
kubectl create ingress catch-all --class=otheringress --rule="/path=svc:port"

# Create an ingress with two annotations: ingress.annotation1 and ingress.annotations2
kubectl create ingress annotated --class=default --rule="foo.com/bar=svc:port" \
--annotation ingress.annotation1=foo \
--annotation ingress.annotation2=bla

# Create an ingress with the same host and multiple paths
kubectl create ingress multipath --class=default \
--rule="foo.com/=svc:port" \
--rule="foo.com/admin/=svcadmin:portadmin"

# Create an ingress with multiple hosts and the pathType as Prefix
kubectl create ingress ingress1 --class=default \
--rule="foo.com/path*=svc:8080" \
--rule="bar.com/admin*=svc2:http"

# Create an ingress with TLS enabled using the default ingress certificate and different path types
kubectl create ingress ingtls --class=default \
--rule="foo.com/=svc:https,tls" \
--rule="foo.com/path/subpath*=othersvc:8080"

# Create an ingress with TLS enabled using a specific secret and pathType as Prefix
kubectl create ingress ingsecret --class=default \
--rule="foo.com/*=svc:8080,tls=secret1"

# Create an ingress with a default backend
kubectl create ingress ingdefault --class=default \
--default-backend=defaultsvc:http \
--rule="foo.com/*=svc:8080,tls=secret1"
```

--------------------------------

### Example Job Events Output

Source: https://kubernetes.io/docs/concepts/workloads/controllers/job

This is an example output from `kubectl describe jobs/myjob`, illustrating the 'Suspended' and 'Resumed' events. These events directly correlate with changes to the `.spec.suspend` field and show the effect on pod lifecycle.

```text
Name:           myjob
...
Events:
  Type    Reason            Age   From            Message
  ----    ------            ----  ----            -------
  Normal  SuccessfulCreate  12m   job-controller  Created pod: myjob-hlrpl
  Normal  SuccessfulDelete  11m   job-controller  Deleted pod: myjob-hlrpl
  Normal  Suspended         11m   job-controller  Job suspended
  Normal  SuccessfulCreate  3s    job-controller  Created pod: myjob-jvb44
  Normal  Resumed           3s    job-controller  Job resumed
```

--------------------------------

### Kubernetes Ingress with Resource Backend Example

Source: https://kubernetes.io/docs/concepts/services-networking/_print

An example of a Kubernetes Ingress resource configured to use custom resources as backends. This is useful for ingressing data to non-Service resources like object storage buckets.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-resource-backend
spec:
  defaultBackend:
    resource:
      apiGroup: k8s.example.com
      kind: StorageBucket
      name: static-assets
  rules:
    - http:
        paths:
          - path: /icons
            pathType: ImplementationSpecific
            backend:
              resource:
                apiGroup: k8s.example.com
                kind: StorageBucket
                name: icon-assets

```

--------------------------------

### Upload Signed Certificate to Kubernetes CSR Status

Source: https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster

Populates the signed certificate into the status field of a Kubernetes CertificateSigningRequest (CSR) object. This command uses `kubectl` to get the CSR in JSON format, `jq` to inject the base64-encoded certificate into the `.status.certificate` field, and then replaces the CSR's status with the modified JSON. Ensure `jq` is installed and the certificate file `ca-signed-server.pem` exists.

```bash
kubectl get csr my-svc.my-namespace -o json | \
  jq '.status.certificate = "$(base64 ca-signed-server.pem | tr -d '\n')"' | \
  kubectl replace --raw /apis/certificates.k8s.io/v1/certificatesigningrequests/my-svc.my-namespace/status -f -
```

--------------------------------

### Start a New etcd Member

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This section outlines the environment variables and command to start a newly added etcd member. It configures the etcd instance with its name, the initial cluster configuration including the new member, and specifies that it's joining an existing cluster state. This command is executed on the machine designated for the new etcd member.

```shell
export ETCD_NAME="member4"
export ETCD_INITIAL_CLUSTER="member2=http://10.0.0.2:2380,member3=http://10.0.0.3:2380,member4=http://10.0.0.4:2380"
export ETCD_INITIAL_CLUSTER_STATE=existing
etcd [flags]
```

--------------------------------

### Verify CNI Bridge Plugin Installation

Source: https://kubernetes.io/docs/tutorials/_print

This command checks the version of the CNI bridge plugin, which is installed and configured by the cri-o installer. It helps confirm that the network plugins are set up correctly for Kubernetes.

```bash
/opt/cni/bin/bridge --version

```

--------------------------------

### Example Docker Compose File

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

This is a sample `docker-compose.yml` file used to demonstrate the Kompose conversion process. It defines three services: `redis-leader`, `redis-replica`, and `web`, with specified images, ports, and configurations.

```yaml
services:

  redis-leader:
    container_name: redis-leader
    image: redis
    ports:
      - "6379"

  redis-replica:
    container_name: redis-replica
    image: redis
    ports:
      - "6379"
    command: redis-server --replicaof redis-leader 6379 --dir /tmp

  web:
    container_name: web
    image: quay.io/kompose/web
    ports:
      - "8080:8080"
    environment:
      - GET_HOSTS_FROM=dns
    labels:
      kompose.service.type: LoadBalancer

```

--------------------------------

### Example Pod with Injected Sidecar Container

Source: https://kubernetes.io/docs/reference/access-authn-authz/mutating-admission-policy

This is an example of a Pod manifest after the MutatingAdmissionPolicy has been applied. It demonstrates the addition of the 'mesh-proxy' initContainer, as defined in the policy's mutation rules.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
  namespace: default
spec:
  ...
  initContainers:
  - name: mesh-proxy
    image: mesh/proxy:v1.0.0
    args: ["proxy", "sidecar"]
    restartPolicy: Always
  - name: myapp-initializer
    image: example/initializer:v1.0.0
  ...

```

--------------------------------

### Start Multi-Node etcd Cluster

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This command starts a multi-node etcd cluster for production environments, recommended for durability and high availability. It configures client URLs for multiple nodes. Ensure IP<n> variables are set to your client IP addresses.

```bash
etcd --listen-client-urls=http://$IP1:2379,http://$IP2:2379,http://$IP3:2379,http://$IP4:2379,http://$IP5:2379 --advertise-client-urls=http://$IP1:2379,http://$IP2:2379,http://$IP3:2379,http://$IP4:2379,http://$IP5:2379

```

--------------------------------

### Copy Pod, Add Debug Container, and Set Specific Images

Source: https://kubernetes.io/docs/reference/kubectl/_print

This example creates a copy of 'mypod' as 'my-debugger', adds a debug container using the 'debian' image, and updates specific application container images ('app' and 'sidecar') to their debug versions. This allows for debugging with updated dependencies.

```bash
kubectl debug mypod -it --copy-to=my-debugger --image=debian --set-image=app=app:debug,sidecar=sidecar:debug
```

--------------------------------

### Install Bash using Homebrew

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

This command installs or upgrades Bash using Homebrew. It is used on macOS when the default Bash version is older than 4.1, which is necessary for proper kubectl autocompletion.

```bash
brew install bash
```

--------------------------------

### Start Minikube for Cilium

Source: https://kubernetes.io/docs/tasks/administer-cluster/network-policy-provider/cilium-network-policy

Command to start Minikube with the necessary network plugin for Cilium integration. Requires Minikube version v1.5.2 or higher.

```bash
minikube start --network-plugin=cni
```

--------------------------------

### Set Download Directory for Binaries

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Configures and creates a writable directory for downloading binary files. This is a prerequisite for installing Kubernetes components. It ensures that the specified download directory exists and is accessible.

```shell
DOWNLOAD_DIR="/usr/local/bin"
sudo mkdir -p "$DOWNLOAD_DIR"
```

--------------------------------

### Minimal Kubernetes Ingress Resource Example

Source: https://kubernetes.io/docs/concepts/services-networking/_print

A basic example of a Kubernetes Ingress resource configuration. This YAML defines an Ingress with a specific ingress class and a rule to route traffic for a path to a Kubernetes Service.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: minimal-ingress
spec:
  ingressClassName: nginx-example
  rules:
  - http:
      paths:
      - path: /testpath
        pathType: Prefix
        backend:
          service:
            name: test
            port:
              number: 80

```

--------------------------------

### Explain Deployment in Supported API Versions

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_explain/_print

Fetches the explanation for a 'deployment' resource, specifically for a given API version. This is useful when multiple versions of an API exist.

```bash
kubectl explain deployments --api-version=apps/v1
```

--------------------------------

### Locally Test Documentation (Make)

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/kubectl

Builds and serves the Kubernetes documentation locally using the 'container-serve' make target. This allows for previewing the generated documentation before committing changes. It also includes a step to update git submodules if necessary.

```make
cd <web-base>
git submodule update --init --recursive --depth 1 # if not already done
make container-serve
```

--------------------------------

### Install missing ebtables and ethtool

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm

This section provides commands to install `ebtables` and `ethtool` on Debian/Ubuntu and CentOS/Fedora systems. These packages are often required by kubeadm during installation, and missing them can lead to pre-flight check warnings.

```bash
# For Ubuntu/Debian users
apt install ebtables ethtool

# For CentOS/Fedora users
yum install ebtables ethtool

```

--------------------------------

### Install Curl and Test Nginx Server - Bash

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization

These commands are executed within the Nginx container's shell. First, 'apt-get update' refreshes the package list, followed by 'apt-get install curl' to install the curl utility. Finally, 'curl localhost' sends a request to the Nginx server to verify it's serving the content prepared by the init container.

```bash
root@nginx:~# apt-get update
root@nginx:~# apt-get install curl
root@nginx:~# curl localhost

```

--------------------------------

### Access Web Service with Minikube

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

If using minikube, this command opens the web service in your default browser. It's a convenient way to access your application during local development.

```bash
minikube service web-tcp

```

--------------------------------

### Namespace Selector Examples for Kubernetes Admission Webhooks

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/_print

Demonstrates how to use namespace selectors to control which namespaces an admission policy applies to. It shows examples for excluding specific runlevels and including specific environments.

```json
{
  "namespaceSelector": {
    "matchExpressions": [
      {
        "key": "runlevel",
        "operator": "NotIn",
        "values": [ "0", "1" ]
      }
    ]
  }
}
```

```json
{
  "namespaceSelector": {
    "matchExpressions": [
      {
        "key": "environment",
        "operator": "In",
        "values": [ "prod", "staging" ]
      }
    ]
  }
}
```

--------------------------------

### Configure Kubelet Parameters Using a JSON File

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This snippet demonstrates how to configure Kubelet parameters using a JSON file, which is the recommended approach for simplifying node deployment and configuration management. The configuration file is a representation of the KubeletConfiguration struct and requires read permissions for the kubelet. It allows setting parameters like IP address, port, image pull serialization, and eviction thresholds.

```json
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
address: "192.168.0.8"
port: 20250
serializeImagePulls: false
evictionHard:
    memory.available:  "100Mi"
    nodefs.available:  "10%"
    nodefs.inodesFree: "5%"
    imagefs.available: "15%"
    imagefs.inodesFree: "5%"
```

--------------------------------

### GET /apis/node.k8s.io/v1/runtimeclasses

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/_print

Lists or watches all RuntimeClass objects. This endpoint is used to get a collection of all configured RuntimeClasses.

```APIDOC
## GET /apis/node.k8s.io/v1/runtimeclasses

### Description
Lists or watches all RuntimeClass objects. This endpoint is used to get a collection of all configured RuntimeClasses.

### Method
GET

### Endpoint
/apis/node.k8s.io/v1/runtimeclasses

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks
- **continue** (string) - Optional - continue
- **fieldSelector** (string) - Optional - fieldSelector
- **labelSelector** (string) - Optional - labelSelector
- **limit** (integer) - Optional - limit
- **pretty** (string) - Optional - pretty-print output
- **resourceVersion** (string) - Optional - resourceVersion
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents
- **timeoutSeconds** (integer) - Optional - timeoutSeconds
- **watch** (boolean) - Optional - watch

### Response
#### Success Response (200)
- **RuntimeClassList** (object) - OK

#### Error Response
- **401** - Unauthorized
```

--------------------------------

### Create a CronJob

Source: https://kubernetes.io/docs/reference/kubectl/quick-reference

Creates a Kubernetes CronJob that executes a command at a specified schedule. This example sets up a CronJob named 'hello' to run a busybox container every minute, printing 'Hello World'.

```bash
kubectl create cronjob hello --image=busybox:1.28   --schedule="*/1 * * * *" -- echo "Hello World"
```

--------------------------------

### Start Single-Node etcd Cluster

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This command starts a single-node etcd cluster for testing purposes. It configures the client URLs for listening and advertising. Ensure PRIVATE_IP is set to your etcd client IP.

```bash
etcd --listen-client-urls=http://$PRIVATE_IP:2379 \
   --advertise-client-urls=http://$PRIVATE_IP:2379

```

--------------------------------

### GET /api/v1/namespaces

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/_print

Lists or watches all Namespaces in the cluster. This endpoint is used to get a collection of all namespaces available.

```APIDOC
## GET /api/v1/namespaces

### Description
Lists or watches all Namespaces in the cluster. This endpoint is used to get a collection of all namespaces available.

### Method
GET

### Endpoint
/api/v1/namespaces

### Parameters
#### Query Parameters
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, but the initial request and the persistent "Keep-Alive" connection can be turned off.
- **continue** (string) - Optional - The continue option should be set when retrieving large number of results to get the next page of results.
- **dryRun** (string) - Optional - When present, indicates that modifications should not be persisted. Valid values are: "All", "None".
- **fieldSelector** (string) - Optional - Selector to filter fields on.
- **gracePeriodSeconds** (integer) - Optional - The duration in seconds before the object is deleted. Allows for graceful deletion of an object.
- **ignoreStoreReadErrorWithClusterBreakingPotential** (boolean) - Optional - If true, ignore errors that might indicate a cluster is breaking.
- **labelSelector** (string) - Optional - Selector to filter on labels.
- **limit** (integer) - Optional - limit is a maximum number of responses to return for a list call. If more items exist, a continue token is returned.
- **propagationPolicy** (string) - Optional - Represents the policy that governs the deletion of dependent objects.
- **resourceVersion** (string) - Optional - resourceVersion sets the identity of a resource version.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines whether the specified resourceVersion must match current version of the resource or whether it can be any version.
- **sendInitialEvents** (boolean) - Optional - `sendInitialEvents=true` or `false` indicates whether to send initial events for list calls.
- **timeoutSeconds** (integer) - Optional - Timeout for the request.

### Response
#### Success Response (200)
- **NamespaceList** (object) - Contains a list of Namespace objects.

#### Response Example
```json
{
  "apiVersion": "v1",
  "kind": "NamespaceList",
  "metadata": {
    "selfLink": "/api/v1/namespaces",
    "resourceVersion": "12345"
  },
  "items": [
    {
      "apiVersion": "v1",
      "kind": "Namespace",
      "metadata": {
        "name": "default",
        "creationTimestamp": "2023-10-27T09:00:00Z"
      },
      "spec": {
        "finalizers": []
      },
      "status": {
        "phase": "Active"
      }
    },
    {
      "apiVersion": "v1",
      "kind": "Namespace",
      "metadata": {
        "name": "kube-system",
        "creationTimestamp": "2023-10-27T09:01:00Z"
      },
      "spec": {
        "finalizers": []
      },
      "status": {
        "phase": "Active"
      }
    }
  ]
}
```

#### Error Response (401)
- **Unauthorized** - Indicates that the request lacks valid authentication credentials.
```

--------------------------------

### StorageClass Example for PersistentVolumeClaim Resize

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example demonstrates a StorageClass configuration that allows PersistentVolumeClaim (PVC) resizing. By setting `allowVolumeExpansion` to `true`, PVCs created from this StorageClass can be expanded. This is crucial for the PersistentVolumeClaimResize admission controller to permit such operations.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: gluster-vol-default
provisioner: kubernetes.io/glusterfs
parameters:
  resturl: "http://192.168.10.100:8080"
  restuser: ""
  secretNamespace: ""
  secretName: ""
allowVolumeExpansion: true

```

--------------------------------

### kubeadm init phase addon kube-proxy

Source: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init-phase

Installs the kube-proxy addon components via the API server.

```APIDOC
## kubeadm init phase addon kube-proxy

### Description
Install the kube-proxy addon components via the API server.

### Method
POST (implied by installation action)

### Endpoint
/apis/kubeadm.k8s.io/v1beta3/namespaces/kube-system/configmaps/kubeadm-config/phases/addon/kube-proxy/apply

### Parameters
#### Query Parameters
- **dry-run** (string) - Optional - Don't apply any changes; just output what would be done.
- **feature-gates** (string) - Optional - A set of key=value pairs that describe feature gates for various features.

#### Request Body
- **config** (string) - Optional - Path to a kubeadm configuration file.
- **image-repository** (string) - Optional - Choose a container registry to pull control plane images from. Default: "registry.k8s.io"
- **kubeconfig** (string) - Optional - The kubeconfig file to use when talking to the cluster. Default: "/etc/kubernetes/admin.conf"
- **kubernetes-version** (string) - Optional - Choose a specific Kubernetes version for the control plane. Default: "stable-1"
- **service-cidr** (string) - Optional - Use alternative range of IP address for service VIPs. Default: "10.96.0.0/12"
- **service-dns-domain** (string) - Optional - Use alternative domain for services, e.g. "myorg.internal". Default: "cluster.local"
- **rootfs** (string) - Optional - The path to the 'real' host root filesystem. This will cause kubeadm to chroot into the provided path.

### Request Example
```json
{
  "config": "/path/to/kubeadm-config.yaml",
  "image-repository": "myregistry.com/k8s",
  "kubernetes-version": "v1.28.0"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates the success of the operation.

#### Response Example
```json
{
  "status": "Kube-proxy addon installed successfully."
}
```
```

--------------------------------

### Initializing a Dual-Stack Kubernetes Cluster with Kubeadm (CLI)

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

Example command to initialize a dual-stack Kubernetes control plane node using kubeadm. It specifies both IPv4 and IPv6 CIDR ranges for Pods and Services.

```shell
# These address ranges are exampleskubeadm init --pod-network-cidr=10.244.0.0/16,2001:db8:42:0::/56 --service-cidr=10.96.0.0/16,2001:db8:42:1::/112
```

--------------------------------

### Compose Deployment and Service Resources with Kustomize

Source: https://kubernetes.io/docs/tasks/manage-kubernetes-objects/_print

This example shows how to compose a Kubernetes application consisting of a Deployment and a Service. It involves creating separate YAML files for each resource and then referencing them in a kustomization.yaml file using the 'resources' field.

```shell
# Create a deployment.yaml file
cat <<EOF > deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  selector:
    matchLabels:
      run: my-nginx
  replicas: 2
  template:
    metadata:
      labels:
        run: my-nginx
    spec:
      containers:
      - name: my-nginx
        image: nginx
        ports:
        - containerPort: 80
EOF

# Create a service.yaml file
cat <<EOF > service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nginx
  labels:
    run: my-nginx
spec:
  ports:
  - port: 80
    protocol: TCP
  selector:
    run: my-nginx
EOF

# Create a kustomization.yaml composing them
cat <<EOF >./kustomization.yaml
resources:
- deployment.yaml
- service.yaml
EOF
```

--------------------------------

### GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Lists or watches all StorageVersionMigration objects.

```APIDOC
## GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations

### Description
Lists or watches all StorageVersionMigration objects.

### Method
GET

### Endpoint
/apis/storagemigration.k8s.io/v1beta1/storageversionmigrations

### Parameters
#### Query Parameters
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be returned to the caller with the appropriate Content-Type header.

### Response
#### Success Response (200)
- **StorageVersionMigrationList** (Object) - OK
  - **apiVersion** (string)
  - **kind** (string)
  - **metadata** (ListMeta)
  - **items** (Array[StorageVersionMigration])

#### Error Response (401)
- **Unauthorized**
```

--------------------------------

### Kubernetes Deployment with a Sidecar Container

Source: https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers

This example demonstrates a Kubernetes Deployment named 'myapp' with two containers. The primary 'myapp' container runs an Alpine image and continuously writes to a log file. The 'logshipper' container, defined as an init container with `restartPolicy: Always`, acts as a sidecar, tailing the log file. Both containers share a volume for log data. This setup effectively uses a sidecar for log shipping.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: alpine:latest
          command: ['sh', '-c', 'while true; do echo "logging" >> /opt/logs.txt; sleep 1; done']
          volumeMounts:
            - name: data
              mountPath: /opt
      initContainers:
        - name: logshipper
          image: alpine:latest
          restartPolicy: Always
          command: ['sh', '-c', 'tail -F /opt/logs.txt']
          volumeMounts:
            - name: data
              mountPath: /opt
      volumes:
        - name: data
          emptyDir: {}

```

--------------------------------

### Initialize Zsh Completion System

Source: https://kubernetes.io/docs/tasks/tools/_print

Initializes the Zsh completion system by loading `compinit`. This is necessary if the `compdef` command is not found, ensuring that Zsh's completion framework is properly set up before sourcing kubectl completion.

```zsh
autoload -Uz compinit
compinit
```

--------------------------------

### Install Kubernetes apt Packages (Debian/Ubuntu)

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

Updates the apt package index and installs necessary packages for the Kubernetes apt repository, including transport-https, ca-certificates, and curl. This is a prerequisite for adding the Kubernetes repository.

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```

--------------------------------

### Create a Pod for Ephemeral Container Example (kubectl)

Source: https://kubernetes.io/docs/tasks/debug/_print

This command creates a basic pod using the `pause` image, which serves as a target for debugging with ephemeral containers. It's a prerequisite for demonstrating `kubectl debug`.

```bash
kubectl run ephemeral-demo --image=registry.k8s.io/pause:3.1 --restart=Never
```

--------------------------------

### Start a Hazelcast pod with environment variables using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts a Hazelcast pod and sets two environment variables: DNS_DOMAIN to 'cluster' and POD_NAMESPACE to 'default'. Environment variables are crucial for configuring application behavior within the container.

```bash
kubectl run hazelcast --image=hazelcast/hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"
```

--------------------------------

### Explain Resource Documentation in Different Format

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_explain/_print

Retrieves the documentation for a Kubernetes resource and renders it in a specified output format, such as 'plaintext-openapiv2'.

```bash
kubectl explain deployment --output=plaintext-openapiv2
```

--------------------------------

### Configure API Server with easyrsa Certificates

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This snippet shows the parameters to add to the API server's start configuration when using certificates generated by easyrsa. It specifies the paths to the CA certificate, server certificate, and server key files.

```bash
--client-ca-file=/yourdirectory/ca.crt
--tls-cert-file=/yourdirectory/server.crt
--tls-private-key-file=/yourdirectory/server.key
```

--------------------------------

### Structural Schema Correction for Example 1 (Kubernetes CRD)

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/_print

This example provides the correct structural schema for the previous non-structural example. It adheres to rule 2 by specifying properties outside of the 'allOf' block.

```yaml
properties:
  foo:
    # ...
allOf:
- properties:
    foo:
      # ...

```

--------------------------------

### Kubeadm Reset Configuration Example

Source: https://kubernetes.io/docs/reference/config-api/kubeadm-config

Shows the basic structure for `ResetConfiguration` used with the `kubeadm reset --config` command. This configuration type is minimal and primarily serves as a placeholder for reset-specific options.

```yaml
apiVersion: kubeadm.k8s.io/v1beta4
kind: ResetConfiguration
...

```

--------------------------------

### Create versioned directories for documentation

Source: https://kubernetes.io/docs/contribute/_print

Executes the `createversiondirs` make target within the reference-docs directory. This action creates a versioned directory (e.g., v1_34) and copies the necessary kubectl reference configuration files into it.

```bash
cd <rdocs-base>
make createversiondirs
```

--------------------------------

### Clone Required Go Repositories

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/kubectl

This command sequence fetches necessary Go packages and repositories, including pflag, cobra, yaml, and reference-docs, using the `go get` command. These are essential dependencies for building and generating documentation.

```bash
go get -u github.com/spf13/pflag
go get -u github.com/spf13/cobra
go get -u gopkg.in/yaml.v2
go get -u github.com/kubernetes-sigs/reference-docs
```

--------------------------------

### Start New etcd Member

Source: https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd

Initializes and starts a new etcd member on a specified machine. This involves setting environment variables for the etcd name, initial cluster configuration, and cluster state before running the etcd binary.

```bash
export ETCD_NAME="member4"
export ETCD_INITIAL_CLUSTER="member2=http://10.0.0.2:2380,member3=http://10.0.0.3:2380,member4=http://10.0.0.4:2380"
export ETCD_INITIAL_CLUSTER_STATE=existing
etcd [flags]

```

--------------------------------

### Install Kubernetes Apt Repository Prerequisites (Debian/Ubuntu)

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

This command updates the apt package index and installs necessary packages for using the Kubernetes apt repository on Debian-based systems. It includes `apt-transport-https`, `ca-certificates`, `curl`, and `gpg`.

```bash
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

```

--------------------------------

### Structural Schema Correction for Example 2 (Kubernetes CRD)

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/_print

This example presents the corrected structural schema for the previous non-structural example. It follows rule 2 by defining properties for items outside the 'allOf' block.

```yaml
items:
  properties:
    foo:
      # ...
allOf:
- items:
    properties:
      foo:
        # ...

```

--------------------------------

### Create Pod from Manifest

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Creates the Kubernetes Pod defined in the 'pod-resize.yaml' file within the 'qos-example' namespace.

```bash
kubectl create -f pod-resize.yaml -n qos-example
```

--------------------------------

### List All Containers with Docker and Pods with kubectl

Source: https://kubernetes.io/docs/reference/kubectl/_print

Compares listing all containers (including stopped ones) using 'docker ps -a' with listing all pods using 'kubectl get po'.

```bash
docker ps -a
```

```bash
kubectl get po
```

--------------------------------

### Example: Create a NodePort Service

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example demonstrates how to create a new NodePort service named 'my-ns' and map TCP port 5678 on the service to port 8080 on the target pods.

```bash
# Create a new NodePort service named my-ns
kubectl create service nodeport my-ns --tcp=5678:8080
```

--------------------------------

### List Minikube Addons

Source: https://kubernetes.io/docs/tutorials/_print

Lists all addons supported by Minikube and their current status (enabled/disabled). This command helps in understanding the available addons and their configurations.

```bash
minikube addons list
```

--------------------------------

### Standard Impersonation Examples

Source: https://kubernetes.io/docs/reference/access-authn-authz/user-impersonation

Examples of RBAC rules for standard impersonation of user extras and UIDs.

```APIDOC
## Standard Impersonation

### Description
These examples demonstrate how to grant permissions to impersonate specific user attributes or UIDs using standard Kubernetes RBAC.

### Method
N/A (RBAC Configuration)

### Endpoint
N/A (RBAC Configuration)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
# Can impersonate the extras field "scopes" with the values "view" and "development"
- apiGroups: ["authentication.k8s.io"]
  resources: ["userextras/scopes"]
  verbs: ["impersonate"]
  resourceNames: ["view", "development"]

# Can impersonate the uid "06f6ce97-e2c5-4ab8-7ba5-7654dd08d52b"
- apiGroups: ["authentication.k8s.io"]
  resources: ["uids"]
  verbs: ["impersonate"]
  resourceNames: ["06f6ce97-e2c5-4ab8-7ba5-7654dd08d52b"]
```

### Response
#### Success Response (200)
N/A (RBAC Configuration)

#### Response Example
N/A (RBAC Configuration)
```

--------------------------------

### Conversion Webhook - Successful Conversion (v1beta1 - Deprecated)

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/_print

This example shows a successful conversion response from a webhook using the deprecated apiextensions.k8s.io/v1beta1 API version. It is functionally similar to the v1 example but is marked as deprecated.

```APIDOC
## POST /apis/apiextensions.k8s.io/v1beta1/conversionreviews

### Description
Handles conversion of custom resources between API versions. This endpoint is deprecated in favor of apiextensions.k8s.io/v1.

### Method
POST

### Endpoint
/apis/apiextensions.k8s.io/v1beta1/conversionreviews

### Parameters
#### Request Body
- **apiVersion** (string) - Required - Specifies the API version of the ConversionReview object.
- **kind** (string) - Required - Specifies the kind of the object, which is "ConversionReview".
- **request** (object) - Required - Contains the details of the conversion request.
  - **uid** (string) - Required - Unique identifier for the request.
  - **desiredAPIVersion** (string) - Required - The target API version for conversion.
  - **objects** (array) - Required - A list of objects to be converted.

### Request Example
```json
{
  "apiVersion": "apiextensions.k8s.io/v1beta1",
  "kind": "ConversionReview",
  "request": {
    "uid": "705ab4f5-6393-11e8-b7cc-42010a800002",
    "desiredAPIVersion": "example.com/v1",
    "objects": [
      {
        "kind": "CronTab",
        "apiVersion": "example.com/v1beta1",
        "metadata": {
          "name": "local-crontab",
          "namespace": "default"
        },
        "host": "localhost",
        "port": "1234"
      }
    ]
  }
}
```

### Response
#### Success Response (200)
- **apiVersion** (string) - The API version of the ConversionReview object.
- **kind** (string) - The kind of the object, which is "ConversionReview".
- **response** (object) - Contains the result of the conversion.
  - **uid** (string) - Required - Copied from the request.uid.
  - **result** (object) - Required - Indicates the status of the conversion.
    - **status** (string) - Required - "Success" if conversion was successful.
  - **convertedObjects** (array) - Required - Contains the converted objects.

#### Response Example
```json
{
  "apiVersion": "apiextensions.k8s.io/v1beta1",
  "kind": "ConversionReview",
  "response": {
    "uid": "705ab4f5-6393-11e8-b7cc-42010a800002",
    "result": {
      "status": "Success"
    },
    "convertedObjects": [
      {
        "kind": "CronTab",
        "apiVersion": "example.com/v1",
        "metadata": {
          "creationTimestamp": "2019-09-04T14:03:02Z",
          "name": "local-crontab",
          "namespace": "default",
          "resourceVersion": "143",
          "uid": "3415a7fc-162b-4300-b5da-fd6083580d66"
        },
        "host": "localhost",
        "port": "1234"
      }
    ]
  }
}
```
```

--------------------------------

### GET /apis/apiregistration.k8s.io/v1/apiservices

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/_print

Lists or watches all APIServices.

```APIDOC
## GET /apis/apiregistration.k8s.io/v1/apiservices

### Description
Lists or watches objects of kind APIService.

### Method
GET

### Endpoint
/apis/apiregistration.k8s.io/v1/apiservices

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks
- **continue** (string) - Optional - continue
- **fieldSelector** (string) - Optional - fieldSelector
- **labelSelector** (string) - Optional - labelSelector
- **limit** (integer) - Optional - limit
- **pretty** (string) - Optional - pretty
- **resourceVersion** (string) - Optional - resourceVersion
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents
- **timeoutSeconds** (integer) - Optional - timeoutSeconds
- **watch** (boolean) - Optional - watch

### Response
#### Success Response (200)
- **APIServiceList** (object) - Returns a list of APIService objects.

#### Error Response
- **401** - Unauthorized
```

--------------------------------

### Create a Kubernetes ClusterRole with specific permissions

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

These examples illustrate the use of `kubectl create clusterrole` to define cluster-wide permissions. They demonstrate creating ClusterRoles with various configurations, including basic verbs and resources, resource names, API groups, subresource access, non-resource URLs, and aggregation rules for combining permissions.

```bash
kubectl create clusterrole pod-reader --verb=get,list,watch --resource=pods

```

```bash
kubectl create clusterrole pod-reader --verb=get --resource=pods --resource-name=readablepod --resource-name=anotherpod

```

```bash
kubectl create clusterrole foo --verb=get,list,watch --resource=replicasets.apps

```

```bash
kubectl create clusterrole foo --verb=get,list,watch --resource=pods,pods/status

```

```bash
kubectl create clusterrole "foo" --verb=get --non-resource-url=/logs/*

```

```bash
kubectl create clusterrole monitoring --aggregation-rule="rbac.example.com/aggregate-to-monitoring=true"

```

--------------------------------

### CEL Device Selector Expression Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/resource-claim-v1

This example demonstrates a CEL expression used to select a device based on its driver and attributes. The expression evaluates to true if the device meets the specified criteria.

```CEL
device.driver == "dra.example.com" && device.attributes["dra.example.com"].model == "example-model"
```

--------------------------------

### Explain Kubernetes Resource Fields

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

The `kubectl explain` command retrieves documentation for Kubernetes resources and their fields. It can describe a resource generally or a specific field using JSONPath notation. Information is fetched from the server in OpenAPI format. Supported resources can be listed using `kubectl api-resources`.

```bash
kubectl explain pods
kubectl explain pods.spec.containers
```

--------------------------------

### Example Pod Using a PriorityClass (YAML)

Source: https://kubernetes.io/docs/concepts/scheduling-eviction/_print

Configures a Pod named 'nginx' to use the 'high-priority' PriorityClass. This ensures the pod is scheduled according to the priority defined in the 'high-priority' PriorityClass.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  priorityClassName: high-priority

```

--------------------------------

### Install and Hold Kubernetes Packages (APT)

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Updates the APT package index and installs `kubelet`, `kubeadm`, and `kubectl`. The `apt-mark hold` command prevents these packages from being automatically upgraded during system updates, ensuring manual control over Kubernetes versioning.

```shell
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

--------------------------------

### Kubectl Config Set-Context Command Example

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_config/_print

Demonstrates how to use the 'kubectl config set-context' command to modify specific fields within a kubeconfig context. This example shows updating the user associated with the 'gce' context.

```bash
kubectl config set-context gce --user=cluster-admin
```

--------------------------------

### Kubernetes EndpointSlices List Example

Source: https://kubernetes.io/docs/tasks/debug/debug-application/_print

An example output of listing Kubernetes EndpointSlices. This shows the name of the EndpointSlice, the address type, the ports exposed, and the list of endpoints (Pod IPs). If ENDPOINTS is '<none>', check Service selector and Pod labels.

```text
NAME              ADDRESSTYPE   PORTS   ENDPOINTS
hostnames-ytpni   IPv4          9376    10.244.0.5,10.244.0.6,10.244.0.7

```

--------------------------------

### Apply Kubernetes Resources from Files and Directories

Source: https://kubernetes.io/docs/reference/kubectl/quick-reference

Manages Kubernetes applications by applying resource definitions from YAML or JSON files. Supports applying single files, multiple files, all files within a directory, or resources from a URL. Also includes commands for creating single resources like deployments and jobs.

```bash
kubectl apply -f ./my-manifest.yaml                 # create resource(s)
kubectl apply -f ./my1.yaml -f ./my2.yaml           # create from multiple files
kubectl apply -f ./dir                              # create resource(s) in all manifest files in dir
kubectl apply -f https://example.com/manifest.yaml  # create resource(s) from url (Note: this is an example domain and does not contain a valid manifest)
kubectl create deployment nginx --image=nginx       # start a single instance of nginx

# create a Job which prints "Hello World"
kubectl create job hello --image=busybox:1.28 -- echo "Hello World"
```

--------------------------------

### CEL Rule Examples for Different Scopes

Source: https://kubernetes.io/docs/reference/kubernetes-api/extend-resources/_print

Provides concrete examples of CEL rules applied to different data structures like maps of objects, lists of integers, and string values.

```JSON
{"rule": "self.components['Widget'].priority < 10"}
```

```JSON
{"rule": "self.values.all(value, value >= 0 && value < 100)"}
```

```JSON
{"rule": "self.startsWith('kube')"}
```

--------------------------------

### Kubernetes ControllerRevision Data Serialization Example (Go)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Illustrates how to handle serialized data within a ControllerRevision using Go's runtime package. It shows the conversion between external (with RawExtension) and internal (with runtime.Object) representations.

```go
package main

import (
	"encoding/json"
	"k8s.io/apimachinery/pkg/runtime"
)

// External package representation
type MyAPIObjectExternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin           runtime.RawExtension `json:"myPlugin"`
}

// Internal package representation
type MyAPIObjectInternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin           runtime.Object `json:"myPlugin"`
}

type PluginA struct {
	AOption string `json:"aOption"`
}

func main() {
	// Example of data on the wire (JSON)
	jsonData := []byte(`{
		"kind":"MyAPIObject",
		"apiVersion":"v1",
		"myPlugin": {
			"kind":"PluginA",
			"aOption":"foo"
		}
	}`) 

	var externalObject MyAPIObjectExternal
	json.Unmarshal(jsonData, &externalObject)

	// In a real scenario, you would use pkg/conversion to copy to the internal struct
	// This would involve unpacking the JSON stored in RawExtension.

	// For demonstration, let's assume we have the internal object directly
	internalObject := MyAPIObjectInternal{
		MyPlugin: &PluginA{AOption: "foo"},
	}

	// The runtime.DefaultScheme would handle the conversion process.
	_ = internalObject
}
```

--------------------------------

### Readiness Probe Configuration

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes

This section details how to configure readiness probes, which are used to determine if a container is ready to serve traffic. It explains the syntax and provides an example.

```APIDOC
## Readiness Probe Configuration

### Description
Readiness probes are configured similarly to liveness probes. They determine if a container is ready to receive traffic. If a readiness probe fails, the Pod will not receive traffic until the probe succeeds.

### Method
N/A (Configuration within Pod/Deployment spec)

### Endpoint
N/A (Configuration within Pod/Deployment spec)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```yaml
readinessProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
  initialDelaySeconds: 5
  periodSeconds: 5
```

### Response
#### Success Response (200)
N/A (Probe success/failure affects Pod readiness status, not a direct API response)

#### Response Example
N/A
```

--------------------------------

### Check Minikube Version

Source: https://kubernetes.io/docs/tasks/administer-cluster/network-policy-provider/cilium-network-policy

Command to check the installed version of Minikube. This is a prerequisite for certain Cilium installations.

```bash
minikube version
```

--------------------------------

### Download Kind Configuration

Source: https://kubernetes.io/docs/tutorials/security/seccomp

This command downloads the example 'kind' configuration file from the specified URL. This file is used to create a local Kubernetes cluster with pre-configured settings.

```bash
curl -L -O https://k8s.io/examples/pods/security/seccomp/kind.yaml
```

--------------------------------

### Kubernetes Role for Superuser Access (Example)

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This YAML defines a Role that grants wildcard access to all resources and all verbs within the 'example.com' API group. This is intended as an example of broad permissions, similar to the built-in 'cluster-admin' role, and should not be used in production environments.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: example.com-superuser # DO NOT USE THIS ROLE, IT IS JUST AN EXAMPLE
rules:
- apiGroups: ["example.com"]
  resources: ["*"]
  verbs: ["*"]

```

--------------------------------

### kubectl port-forward Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Demonstrates various ways to use `kubectl port-forward` to establish connections between local ports and ports within Kubernetes resources.

```APIDOC
## POST /port-forward

### Description
Forwards local ports to ports on Kubernetes resources like pods, deployments, or services.
This command is useful for accessing applications running inside the cluster from your local machine.

### Method
POST

### Endpoint
/port-forward

### Parameters
#### Path Parameters
- **resource_type** (string) - Required - The type of Kubernetes resource (e.g., pod, deployment, service).
- **resource_name** (string) - Required - The name of the Kubernetes resource.

#### Query Parameters
- **local_port** (integer) - Required - The local port to listen on.
- **target_port** (integer or string) - Required - The port on the Kubernetes resource to forward to. Can be a port number or a named port.
- **address** (string) - Optional - Comma-separated list of addresses to listen on. Defaults to "localhost".
- **pod-running-timeout** (duration) - Optional - Time to wait until at least one pod is running. Defaults to "1m0s".

### Request Example
```bash
# Forward local port 5000 to pod 'mypod' port 5000
kubectl port-forward pod/mypod 5000:5000

# Forward local port 8443 to service 'myservice' named port 'https'
kubectl port-forward service/myservice 8443:https

# Forward local port 8888 to pod 'mypod' port 5000, listening on all interfaces
kubectl port-forward --address 0.0.0.0 pod/mypod 8888:5000
```

### Response
#### Success Response (200)
- **message** (string) - Indicates that the port forwarding is established.

#### Response Example
```json
{
  "message": "Port forwarding started successfully."
}
```

### Error Handling
- **404 Not Found**: If the specified resource does not exist.
- **400 Bad Request**: If the port forwarding configuration is invalid.
- **500 Internal Server Error**: If an unexpected error occurs on the server.
```

--------------------------------

### Install Recommended Docker CE Version (CentOS 7)

Source: https://kubernetes.io/docs/setup/_print

This sequence of commands installs a recommended, more recent version of Docker CE (18.06.1) on CentOS 7. This is an alternative workaround for the etcd pod restart issue, addressing the incompatibility with older Docker versions.

```bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce-18.06.1.ce-3.el7.x86_64
```

--------------------------------

### Create Interactive Debug Session on Node

Source: https://kubernetes.io/docs/reference/kubectl/_print

This example demonstrates creating an interactive debugging session directly on a Kubernetes node ('mynode') using a busybox image. The debugging container runs in the host's namespaces, and the host's filesystem is mounted at '/host', enabling low-level node inspection.

```bash
kubectl debug node/mynode -it --image=busybox
```

--------------------------------

### Configure Node Allocatable Resources in Kubelet

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This example shows how to configure kubelet settings to reserve compute resources for system daemons, known as 'Node Allocatable'. This prevents pods from consuming all node resources, ensuring system daemons have sufficient capacity. Configuration is done via the kubelet configuration file.

```yaml
# Example kubelet configuration snippet (actual file path may vary)
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
# ... other configurations ...
cgroupsPerQOS: true
# ... other configurations ...

```

--------------------------------

### Cluster Node Labels Example

Source: https://kubernetes.io/docs/concepts/scheduling-eviction/_print

Shows a sample cluster configuration with four nodes, detailing their status, roles, age, version, and specific labels including zone information.

```shell
NAME    STATUS   ROLES    AGE     VERSION   LABELS
node1   Ready    <none>   4m26s   v1.16.0   node=node1,zone=zoneA
node2   Ready    <none>   3m58s   v1.16.0   node=node2,zone=zoneA
node3   Ready    <none>   3m17s   v1.16.0   node=node3,zone=zoneB
node4   Ready    <none>   2m43s   v1.16.0   node=node4,zone=zoneB
```

--------------------------------

### Kubernetes Probes (Liveness, Readiness, Startup)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Details on configuring liveness, readiness, and startup probes for containers. Note that probes are not allowed for ephemeral containers.

```APIDOC
## Kubernetes Probes

### Description
Probes are used to perform health checks on containers. Kubernetes supports three types of probes: livenessProbe, readinessProbe, and startupProbe. Probes are not allowed for ephemeral containers.

### Liveness Probe
- **livenessProbe** (Probe) - Determines if the container is running. If the liveness probe fails, the kubelet will restart the container.

### Readiness Probe
- **readinessProbe** (Probe) - Determines if the container is ready to serve traffic. If the readiness probe fails, the endpoint will be removed from the service.

### Startup Probe
- **startupProbe** (Probe) - Used for applications that take a long time to start. The startup probe is executed after the container starts. If the startup probe fails, the container will be restarted. Once the startup probe succeeds, the liveness and readiness probes take over.

### Note
Probes are not allowed for ephemeral containers.
```

--------------------------------

### Example: Update Multiple Resource Types

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_set/kubectl_set_image

This example shows how to update the 'nginx' container image to 'nginx:1.9.1' for all deployments and replication controllers in the current namespace. The --all flag is used to select all resources of the specified types. This operation affects multiple resources simultaneously.

```bash
kubectl set image deployments,rc nginx=nginx:1.9.1 --all
```

--------------------------------

### ValidatingAdmissionPolicy Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/validating-admission-policy

An example of a ValidatingAdmissionPolicy that enforces image naming conventions based on namespace labels.

```APIDOC
## ValidatingAdmissionPolicy

### Description
This resource defines a policy that can be used to validate admission requests. It uses the Common Expression Language (CEL) to define the validation rules.

### Method
N/A (This is a Kubernetes resource definition, not an API endpoint)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingAdmissionPolicy
metadata:
  name: "image-matches-namespace-environment.policy.example.com"
spec:
  failurePolicy: Fail
  matchConstraints:
    resourceRules:
    - apiGroups:   ["apps"]
      apiVersions: ["v1"]
      operations:  ["CREATE", "UPDATE"]
      resources:   ["deployments"]
  variables:
  - name: environment
    expression: "'environment' in namespaceObject.metadata.labels ? namespaceObject.metadata.labels['environment'] : 'prod'"
  - name: exempt
    expression: "'exempt' in object.metadata.labels && object.metadata.labels['exempt'] == 'true'"
  - name: containers
    expression: "object.spec.template.spec.containers"
  - name: containersToCheck
    expression: "variables.containers.filter(c, c.image.contains('example.com/'))"
  validations:
  - expression: "variables.exempt || variables.containersToCheck.all(c, c.image.startsWith(variables.environment + '.'))"
    messageExpression: "'only ' + variables.environment + ' images are allowed in namespace ' + namespaceObject.metadata.name"
```

### Response
N/A (This is a resource definition)

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Example Kubelet Reserved Memory Settings (YAML)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This YAML snippet provides examples of kubelet configuration settings for CPU and memory reservations. `kubeReserved` and `systemReserved` are used to reserve resources for Kubernetes system components and the operating system, respectively. These values are crucial for calculating node allocatable memory.

```yaml
kubeReserved: { cpu: "500m", memory: "50Mi" } # half a CPU, 50MiB of memory
systemReserved: { cpu: "500m", memory: "256Mi" } # half a CPU, 256MiB of memory
```

--------------------------------

### GET and LIST Resource Version Semantics

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

Details the behavior of resourceVersion for GET requests and the interaction between resourceVersion and resourceVersionMatch for LIST requests.

```APIDOC
## GET and LIST Resource Version Semantics

### Description
This documentation outlines the semantics of the `resourceVersion` parameter for `get` and `list` operations in the Kubernetes API. It also details the behavior introduced with the `resourceVersionMatch` parameter for `list` requests starting from v1.19.

### GET Semantics

| resourceVersion unset | resourceVersion="0" | resourceVersion="{value other than 0}" |
|---|---|---|
| Most Recent | Any | Not older than |

### LIST Semantics with `resourceVersionMatch`

Starting from v1.19, the `resourceVersionMatch` parameter influences how `resourceVersion` is interpreted in `list` requests. It is recommended to always set `resourceVersionMatch` when setting `resourceVersion` on a `list` request, but be prepared for older API servers that might ignore it.

**Note:** Setting `resourceVersionMatch` without `resourceVersion` is invalid.

### `resourceVersionMatch` and Paging Parameters for LIST Requests

| resourceVersionMatch param | paging params | resourceVersion not set | resourceVersion="0" | resourceVersion="{value other than 0}" |
|---|---|---|---|---|
| _unset_ | _limit unset_ | Most Recent | Any | Not older than |
| _unset_ | limit=<n>, _continue unset_ | Most Recent | Any | Exact |
| _unset_ | limit=<n>, continue=<token> | Continuation | Continuation | Invalid, HTTP `400 Bad Request` |
| `resourceVersionMatch=Exact` | _limit unset_ | Invalid | Invalid | Exact |
| `resourceVersionMatch=Exact` | limit=<n>, _continue unset_ | Invalid | Invalid | Exact |
| `resourceVersionMatch=NotOlderThan` | _limit unset_ | Invalid | Any | Not older than |
| `resourceVersionMatch=NotOlderThan` | limit=<n>, _continue unset_ | Invalid | Any | Not older than |

### Recommendations

- Unless strong consistency is required, using `resourceVersionMatch=NotOlderThan` with a known `resourceVersion` is preferred for better performance and scalability compared to leaving both unset (which requires quorum reads).
- Always be prepared to handle cases where the API server might ignore `resourceVersionMatch`.
```

--------------------------------

### Example: Create High Priority Class

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example demonstrates how to create a PriorityClass named 'high-priority' with a value of 1000 and a description. This is a common use case for defining critical workloads.

```bash
# Create a priority class named high-prioritykubectl create priorityclass high-priority --value=1000 --description="high priority"
```

--------------------------------

### Example: Update container image using strategic merge patch

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_patch

Demonstrates updating a container's image within a pod. This example highlights the need for merge keys (like container name) when using strategic merge patch for complex objects.

```bash
kubectl patch pod valid-pod -p '{"spec":{"containers":[{"name":"kubernetes-serve-hostname","image":"new image"}]}}'
```

--------------------------------

### GET /api/v1/persistentvolumes/{name}

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Retrieves a specific PersistentVolume by its name. This endpoint allows you to get detailed information about a single persistent volume.

```APIDOC
## GET /api/v1/persistentvolumes/{name}

### Description
Retrieves a specific PersistentVolume by its name. This endpoint allows you to get detailed information about a single persistent volume.

### Method
GET

### Endpoint
/api/v1/persistentvolumes/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the PersistentVolume to retrieve.

#### Query Parameters
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, but the server may and may not honor this. If not specified, the API returns the serialized object.

### Response
#### Success Response (200)
- **PersistentVolume** (object) - A detailed object representing the PersistentVolume.

#### Response Example
```json
{
  "apiVersion": "v1",
  "kind": "PersistentVolume",
  "metadata": {
    "name": "my-pv"
  },
  "spec": {
    "capacity": {
      "storage": "5Gi"
    },
    "volumeMode": "Filesystem",
    "accessModes": [
      "ReadWriteOnce"
    ],
    "persistentVolumeReclaimPolicy": "Retain",
    "storageClassName": "my-storage-class",
    "csi": {
      "driver": "csi.example.com",
      "volumeHandle": "vol-12345",
      "readOnly": false
    }
  },
  "status": {
    "phase": "Bound"
  }
}
```

#### Error Response
- **401** - Unauthorized
```

--------------------------------

### Get Pod Details

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Retrieves the detailed YAML configuration of the 'resize-demo' Pod in the 'qos-example' namespace. Used to verify initial resource allocation and status.

```bash
# Wait a moment for the pod to be running
kubectl get pod resize-demo --output=yaml -n qos-example
```

--------------------------------

### Copy Pod and Set All Container Images

Source: https://kubernetes.io/docs/reference/kubectl/_print

This example creates a copy of 'mypod' as 'my-debugger' and changes the images of all containers within the copied pod to 'busybox'. This is helpful for testing compatibility with different base images or diagnosing image-related problems.

```bash
kubectl debug mypod --copy-to=my-debugger --set-image=*=busybox
```

--------------------------------

### Configure Proxy Settings for Windows Kubernetes Installation

Source: https://kubernetes.io/docs/tasks/debug/debug-cluster/windows

Sets HTTP and HTTPS proxy environment variables for the machine, which is necessary when a Windows Server node is behind a proxy during Kubernetes installation. This ensures that the installation process can reach external resources.

```powershell
[Environment]::SetEnvironmentVariable("HTTP_PROXY", "http://proxy.example.com:80/", [EnvironmentVariableTarget]::Machine)
[Environment]::SetEnvironmentVariable("HTTPS_PROXY", "http://proxy.example.com:443/", [EnvironmentVariableTarget]::Machine)
```

--------------------------------

### Kubelet Bootstrap Kubeconfig Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/kubelet-tls-bootstrapping

A sample kubeconfig file used for kubelet bootstrapping. It specifies the cluster details, including the certificate authority path and the API server URL, along with user credentials containing a bootstrap token.

```yaml
apiVersion: v1
kind: Config
clusters:
- cluster:
    certificate-authority: /var/lib/kubernetes/ca.pem
    server: https://my.server.example.com:6443
  name: bootstrap
contexts:
- context:
    cluster: bootstrap
    user: kubelet-bootstrap
  name: bootstrap
current-context: bootstrap
preferences: {}
users:
- name: kubelet-bootstrap
  user:
    token: 07401b.f395accd246ae52d

```

--------------------------------

### CEL JSON Patch Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/mutating-admission-policy-v1beta1

This example shows how to construct a JSON patch using CEL to conditionally modify a value in a Kubernetes object.

```APIDOC
## JSON Patch with CEL

### Description
Define mutations for Kubernetes objects using CEL expressions that generate JSON patches. This allows for granular and conditional updates.

### Method
Not Applicable (This describes a configuration language, not an API endpoint)

### Endpoint
Not Applicable

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None (This is a CEL expression)

### Request Example
```cel
[
  JSONPatch{op: "test", path: "/spec/example", value: "Red"},
  JSONPatch{op: "replace", path: "/spec/example", value: "Green"}
]
```

### Response
#### Success Response (200)
None (This is a configuration definition)

#### Response Example
None
```

--------------------------------

### kubectl label Examples: Adding and Overwriting Labels

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_label/_print

Demonstrates how to add a new label to a pod and how to overwrite an existing label's value using the --overwrite flag. These examples illustrate basic label manipulation on a specified pod.

```bash
# Update pod 'foo' with the label 'unhealthy' and the value 'true'
kubectl label pods foo unhealthy=true

# Update pod 'foo' with the label 'status' and the value 'unhealthy', overwriting any existing value
kubectl label --overwrite pods foo status=unhealthy
```

--------------------------------

### GET and LIST Resource Version Semantics

Source: https://kubernetes.io/docs/reference/using-api/_print

Details the behavior of resourceVersion for GET requests and the combined effect of resourceVersion and resourceVersionMatch for LIST requests.

```APIDOC
## GET and LIST Resource Version Semantics

### Description
This documentation outlines the semantics of the `resourceVersion` parameter for `GET` and `LIST` operations in the Kubernetes API. It also details the behavior when `resourceVersionMatch` is used with `LIST` requests, as introduced in v1.19.

### GET Request Semantics

| `resourceVersion` unset | `resourceVersion`="0" | `resourceVersion`="{value other than 0}" |
|---|---|---|
| Most Recent | Any | Not older than |

### LIST Request Semantics

For `LIST` requests, the `resourceVersionMatch` parameter (available from v1.19) influences how `resourceVersion` is interpreted. It is recommended to always set `resourceVersionMatch` when setting `resourceVersion` on a `LIST` request, but be prepared for older API servers that may ignore it.

Using `resourceVersionMatch=NotOlderThan` with a known `resourceVersion` generally offers better performance and scalability than leaving these parameters unset.

Setting `resourceVersionMatch` without `resourceVersion` is invalid.

#### `resourceVersionMatch` and Paging Parameters for LIST Requests

| `resourceVersionMatch` param | Paging Params | `resourceVersion` not set | `resourceVersion`="0" | `resourceVersion`="{value other than 0}" |
|---|---|---|---|---|
| `unset` | `_limit` unset | Most Recent | Any | Not older than |
| `unset` | `limit`=<n>, `_continue` unset | Most Recent | Any | Exact |
| `unset` | `limit`=<n>, `continue`=<token> | Continuation | Continuation | Invalid, HTTP `400 Bad Request` |
| `Exact` | `_limit` unset | Invalid | Invalid | Exact |
| `Exact` | `limit`=<n>, `_continue` unset | Invalid | Invalid | Exact |
| `NotOlderThan` | `_limit` unset | Invalid | Any | Not older than |
| `NotOlderThan` | `limit`=<n>, `_continue` unset | Invalid | Any | Not older than |
```

--------------------------------

### Kubernetes Label Selector Example for Namespace Filtering

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Demonstrates how to use `namespaceSelector` to filter admission policy application based on namespace labels. This example selects namespaces not associated with 'runlevel' 0 or 1.

```yaml
namespaceSelector:
  matchExpressions:
    - key: runlevel
      operator: NotIn
      values:
        - "0"
        - "1"
```

--------------------------------

### Install Docker CE Version 18.06 on CentOS

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm

This command installs a more recent recommended version of Docker CE (18.06.1.ce-3.el7.x86_64) on CentOS. It first adds the Docker CE repository and then installs the specified version, serving as an alternative workaround for etcd pod restart issues.

```bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce-18.06.1.ce-3.el7.x86_64
```

--------------------------------

### Kubectl Port Forwarding Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This snippet showcases various ways to use `kubectl port-forward` to establish connections to pods, deployments, and services. It demonstrates forwarding specific ports, using named ports, and specifying local and remote port mappings. Ensure you have kubectl configured and the target resources exist in your cluster.

```bash
# Listen on ports 5000 and 6000 locally, forwarding data to/from ports 5000 and 6000 in the pod
kubectl port-forward pod/mypod 5000 6000

# Listen on ports 5000 and 6000 locally, forwarding data to/from ports 5000 and 6000 in a pod selected by the deployment
kubectl port-forward deployment/mydeployment 5000 6000

# Listen on port 8443 locally, forwarding to the targetPort of the service's port named "https" in a pod selected by the service
kubectl port-forward service/myservice 8443:https

# Listen on port 8888 locally, forwarding to 5000 in the pod
kubectl port-forward pod/mypod 8888:5000

# Listen on port 8888 on all addresses, forwarding to 5000 in the pod
kubectl port-forward --address 0.0.0.0 pod/mypod 8888:5000

# Listen on port 8888 on localhost and selected IP, forwarding to 5000 in the pod
kubectl port-forward --address localhost,10.19.21.23 pod/mypod 8888:5000

# Listen on a random port locally, forwarding to 5000 in the pod
kubectl port-forward pod/mypod :5000
```

--------------------------------

### Download Kompose Binary for Linux, macOS, and Windows

Source: https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes

Download the Kompose binary for your operating system by using `curl`. This method fetches the latest release directly from GitHub. After downloading, make the binary executable and move it to a directory in your system's PATH.

```shell
# Linux
curl -L https://github.com/kubernetes/kompose/releases/download/v1.34.0/kompose-linux-amd64 -o kompose

# macOS
curl -L https://github.com/kubernetes/kompose/releases/download/v1.34.0/kompose-darwin-amd64 -o kompose

# Windows
curl -L https://github.com/kubernetes/kompose/releases/download/v1.34.0/kompose-windows-amd64.exe -o kompose.exe

chmod +x kompose
sudo mv ./kompose /usr/local/bin/kompose
```

--------------------------------

### Install crictl for CRI Interaction

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm

Installs the crictl command-line interface, which is used for interacting with the Container Runtime Interface (CRI). This is optional for kubeadm but required for direct CRI interaction. It downloads a specific version and architecture of crictl and extracts it to the specified download directory.

```shell
CRICTL_VERSION="v1.31.0"
ARCH="amd64"
curl -L "https://github.com/kubernetes-sigs/cri-tools/releases/download/${CRICTL_VERSION}/crictl-${CRICTL_VERSION}-linux-${ARCH}.tar.gz" | sudo tar -C $DOWNLOAD_DIR -xz
```

--------------------------------

### Running and Monitoring a Kubernetes Job (Shell)

Source: https://kubernetes.io/docs/concepts/workloads/controllers/_print

These shell commands demonstrate how to apply the Job configuration, check its status, and retrieve logs. The `kubectl apply` command creates the Job, `kubectl describe job` provides detailed status, and `kubectl logs` shows the output from the Job's Pods. The `kubectl get pods` command with a JSONPath output is used to dynamically fetch Pod names for log retrieval.

```shell
# Apply the Job configuration
kubectl apply -f https://kubernetes.io/examples/controllers/job.yaml

# Check the status of the Job
kubectl describe job pi
kubectl get job pi -o yaml

# Get the names of Pods belonging to the Job
pods=$(kubectl get pods --selector=batch.kubernetes.io/job-name=pi --output=jsonpath='{.items[*].metadata.name}')
echo $pods

# View the standard output of a Pod
kubectl logs $pods

# Alternative way to view Job logs
kubectl logs jobs/pi

```

--------------------------------

### Readiness Probe Configuration

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes

This section details how to configure readiness probes, which are used to determine if a container is ready to serve traffic. It explains the similarity to liveness probes and provides an example of an exec-based readiness probe.

```APIDOC
## Readiness Probe Configuration

### Description
Readiness probes are configured similarly to liveness probes, using the `readinessProbe` field instead of `livenessProbe`. They determine if a container is ready to receive traffic. Configuration for HTTP and TCP readiness probes is identical to their liveness probe counterparts.

### Example `readinessProbe` Configuration

```yaml
readinessProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
  initialDelaySeconds: 5
  periodSeconds: 5
```

### Key Considerations
- Readiness and liveness probes can be used in parallel.
- Using both ensures traffic is only sent to ready containers and unhealthy containers are restarted.
- Incorrect implementation can lead to resource starvation.
```

--------------------------------

### CEL JSON Patch with Object Value Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/mutating-admission-policy-v1beta1

This example illustrates how to use CEL to add a nested object to a JSON patch, such as setting spec.selector.

```APIDOC
## JSON Patch with Object Value using CEL

### Description
Construct JSON patches with complex object values using CEL. This example shows how to add a `matchLabels` object to `spec.selector`.

### Method
Not Applicable (This describes a configuration language, not an API endpoint)

### Endpoint
Not Applicable

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None (This is a CEL expression)

### Request Example
```cel
[
  JSONPatch{
    op: "add",
    path: "/spec/selector",
    value: Object.spec.selector{matchLabels: {"environment": "test"}}
  }
]
```

### Response
#### Success Response (200)
None (This is a configuration definition)

#### Response Example
None
```

--------------------------------

### Download kubectl Binary with Curl on Linux (arm64)

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

Downloads the latest stable kubectl binary for Linux on ARM64 architecture using curl. This method requires manual installation and validation.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"
```

--------------------------------

### Configure Kubelet with Manifest URL (Fedora)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

This example shows how to configure the kubelet on Fedora to use a web-hosted manifest file. The `--manifest-url` argument points to the location of the Pod definition file.

```bash
KUBELET_ARGS="--cluster-dns=10.254.0.10 --cluster-domain=kube.local --manifest-url=<manifest-url>"

```

--------------------------------

### Install crictl for CRI Interaction

Source: https://kubernetes.io/docs/setup/_print

This snippet installs `crictl`, a command-line interface for interacting with container runtimes that implement the Container Runtime Interface (CRI). While optional for `kubeadm`, it's useful for debugging and managing container runtimes.

```bash
CRICTL_VERSION="v1.31.0"
ARCH="amd64"
curl -L "https://github.com/kubernetes-sigs/cri-tools/releases/download/${CRICTL_VERSION}/crictl-${CRICTL_VERSION}-linux-${ARCH}.tar.gz" | sudo tar -C $DOWNLOAD_DIR -xz
```

--------------------------------

### GET /apis/scheduling.k8s.io/v1/priorityclasses

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/priority-class-v1

Lists all PriorityClasses or watches for changes. This endpoint is used to get a collection of all defined priority classes.

```APIDOC
## GET /apis/scheduling.k8s.io/v1/priorityclasses

### Description
Lists or watches objects of kind PriorityClass.

### Method
GET

### Endpoint
/apis/scheduling.k8s.io/v1/priorityclasses

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks requests watch events with a time limit.
- **continue** (string) - Optional - continue may be set to the last token returned by the server in order to resume a stalled list call.
- **fieldSelector** (string) - Optional - A selector to restrict the list of returned objects by their fields, e.g. "metadata.name=name".
- **labelSelector** (string) - Optional - A selector to restrict the list of returned objects by their labels, e.g. "metadata.label1=label1,metadata.label2=label2".
- **limit** (integer) - Optional - limit is the maximum number of resources to return for this list in one page. Default value: 500.
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be returned to the caller with the appropriate ContentType of application/json.
- **resourceVersion** (string) - Optional - resourceVersion sets a constraint on what resource versions a consistent list is expected from. See https://kubernetes.io/docs/reference/using-api/api-concepts/#resource-versions for details.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines how resourceVersion is matched between the client and server. Possible values: "Exact" or "Approximate".
- **sendInitialEvents** (boolean) - Optional - `sendInitialEvents=true` with the feature gate `InitialEvents` facilitates the streaming of initial events to the subscriber.
- **timeoutSeconds** (integer) - Optional - timeoutSeconds long-running requests have a timeout in seconds where the server is expected to complete the request. Server clients should set request timeout of corresponding HTTP requests to avoid timing out.
- **watch** (boolean) - Optional - Watch for changes to the specified objects.

### Response
#### Success Response (200)
- **PriorityClassList** (Object) - A list of PriorityClass objects.

#### Response Example
```json
{
  "apiVersion": "scheduling.k8s.io/v1",
  "kind": "PriorityClassList",
  "items": [
    {
      "apiVersion": "scheduling.k8s.io/v1",
      "kind": "PriorityClass",
      "metadata": {
        "name": "high-priority"
      },
      "value": 1000,
      "globalDefault": false,
      "description": "This priority class should be used for critical system components."
    },
    {
      "apiVersion": "scheduling.k8s.io/v1",
      "kind": "PriorityClass",
      "metadata": {
        "name": "low-priority"
      },
      "value": -1000,
      "globalDefault": false,
      "description": "This priority class should be used for non-critical batch jobs."
    }
  ]
}
```
```

--------------------------------

### Configure EmptyDir Volume with Size Limit (YAML)

Source: https://kubernetes.io/docs/concepts/storage/volumes

Provides an example of configuring an `emptyDir` volume in a Kubernetes Pod with a specified size limit. This volume is initially empty and is used for scratch space or temporary data. The `sizeLimit` ensures the volume does not exceed a certain capacity.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: registry.k8s.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir:
      sizeLimit: 500Mi

```

--------------------------------

### Download kubectl Binary with Curl on Linux (amd64)

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

Downloads the latest stable kubectl binary for Linux on x86-64 architecture using curl. This method requires manual installation and validation.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

--------------------------------

### GET /api/v1/namespaces/{name}

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/_print

Retrieves a specific Namespace by its name. This endpoint allows you to get detailed information about a particular namespace within the Kubernetes cluster.

```APIDOC
## GET /api/v1/namespaces/{name}

### Description
Retrieves a specific Namespace by its name. This endpoint allows you to get detailed information about a particular namespace within the Kubernetes cluster.

### Method
GET

### Endpoint
/api/v1/namespaces/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the Namespace to retrieve.

#### Query Parameters
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, but the initial request and the persistent "Keep-Alive" connection can be turned off.

### Response
#### Success Response (200)
- **Namespace** (object) - Contains the details of the requested Namespace.

#### Response Example
```json
{
  "apiVersion": "v1",
  "kind": "Namespace",
  "metadata": {
    "name": "example-namespace",
    "creationTimestamp": "2023-10-27T10:00:00Z"
  },
  "spec": {
    "finalizers": []
  },
  "status": {
    "phase": "Active"
  }
}
```

#### Error Response (401)
- **Unauthorized** - Indicates that the request lacks valid authentication credentials.
```

--------------------------------

### EncryptionConfiguration Example (YAML)

Source: https://kubernetes.io/docs/reference/config-api/_print

An example of the EncryptionConfiguration structure in YAML format. This configuration defines how different resource types are encrypted using various providers like AES-CBC. It supports wildcards for resource selection and specifies key management.

```yaml
kind: EncryptionConfiguration
apiVersion: apiserver.config.k8s.io/v1
resources:
- resources:
  - events
  providers:
  - identity: {}  # do not encrypt events even though *.* is specified below
- resources:
  - secrets
  - configmaps
  - pandas.awesome.bears.example
  providers:
  - aescbc:
      keys:
      - name: key1
        secret: c2VjcmV0IGlzIHNlY3VyZQ==
- resources:
  - '*.apps'
  providers:
  - aescbc:
      keys:
      - name: key2
        secret: c2VjcmV0IGlzIHNlY3VyZSwgb3IgaXMgaXQ/Cg==
- resources:
  - '*.*'
  providers:
  - aescbc:
      keys:
      - name: key3
        secret: c2VjcmV0IGlzIHNlY3VyZSwgSSB0aGluaw==
```

--------------------------------

### Add Kubernetes Zypper Repository

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux

This command adds the Kubernetes zypper repository configuration to the system. It overwrites any existing configuration in `/etc/zypp/repos.d/kubernetes.repo`. This is a prerequisite for installing kubectl using zypper on SUSE-based systems.

```bash
cat <<EOF | sudo tee /etc/zypp/repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/repodata/repomd.xml.key
EOF
```

--------------------------------

### Create a Namespace with kubectl

Source: https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod

Creates a new Kubernetes namespace named 'qos-example' to isolate resources created during this exercise. This is a prerequisite for the subsequent Pod creation steps.

```bash
kubectl create namespace qos-example
```

--------------------------------

### Kubernetes API Versioning: Avoid Comments on Alternatives

Source: https://kubernetes.io/docs/contribute/style/style-guide

In code and configuration examples, refrain from including comments that suggest alternative versions or older syntax. Focus on providing clear, current examples. The `apiVersion` field is a common area where this guidance applies.

```yaml
apiVersion: v1
kind: Pod
...
```

--------------------------------

### Clean up installation files

Source: https://kubernetes.io/docs/tasks/tools/_print

Removes the downloaded kubectl convert plugin executable and its checksum file after successful installation. This command uses 'del' to delete the files.

```shell
del kubectl-convert.exe
del kubectl-convert.exe.sha256
```

--------------------------------

### Create and Navigate to .kube Directory

Source: https://kubernetes.io/docs/tasks/tools/_print

These commands guide the user through creating a .kube directory in their home directory and then navigating into it. This directory is essential for storing kubectl configuration files.

```shell
# If you're using cmd.exe, run: cd %USERPROFILE%
cd ~
```

```shell
mkdir .kube
```

```shell
cd .kube
```

--------------------------------

### Typical Gateway Resource Example (Kubernetes YAML)

Source: https://kubernetes.io/docs/concepts/services-networking/gateway

This example shows a typical Gateway resource configuration. It defines an instance of traffic handling infrastructure, specifying the `gatewayClassName` it belongs to and its listeners. The `listeners` section configures protocol, port, hostname, and route attachment rules, such as `allowedRoutes` for cross-namespace access.

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: example-gateway
  namespace: example-namespace
spec:
  gatewayClassName: example-class
  listeners:
  - name: http
    protocol: HTTP
    port: 80
    hostname: "www.example.com"
    allowedRoutes:
      namespaces:
        from: Same

```

--------------------------------

### Format Token Authentication File for Kube-API Server

Source: https://kubernetes.io/docs/reference/access-authn-authz/kubelet-tls-bootstrapping

This example shows the required format for a token authentication file used by the kube-apiserver. Each line represents a token with its associated user and group information.

```text
02b50b05283e98dd0fd71db496ef01e8,kubelet-bootstrap,10001,"system:bootstrappers"

```

--------------------------------

### Kubernetes: Run Pods with kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This snippet shows basic usage of `kubectl run` to start pods with specified images. It covers simple pod creation, exposing ports, setting environment variables, and applying labels.

```bash
# Start a nginx pod
kubectl run nginx --image=nginx

# Start a hazelcast pod and let the container expose port 5701
kubectl run hazelcast --image=hazelcast/hazelcast --port=5701

# Start a hazelcast pod and set environment variables "DNS_DOMAIN=cluster" and "POD_NAMESPACE=default" in the container
kubectl run hazelcast --image=hazelcast/hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"

# Start a hazelcast pod and set labels "app=hazelcast" and "env=prod" in the container
kubectl run hazelcast --image=hazelcast/hazelcast --labels="app=hazelcast,env=prod"
```

--------------------------------

### Example StorageVersionMigration Status Output

Source: https://kubernetes.io/docs/tasks/manage-kubernetes-objects/storage-version-migration

Provides an example of the status output for a StorageVersionMigration object, indicating the progress and success of the migration. It shows conditions like 'Running' and 'Succeeded'.

```yaml
kind: StorageVersionMigration
apiVersion: storagemigration.k8s.io/v1beta1
metadata:
  name: secrets-migration
  uid: 628f6922-a9cb-4514-b076-12d3c178967c
  resourceVersion: "90"
  creationTimestamp: "2024-03-12T20:29:45Z"
spec:
  resource:
    group: ""
    resource: secrets
status:
  conditions:
  - type: Running
    status: "False"
    lastUpdateTime: "2024-03-12T20:29:46Z"
    reason: StorageVersionMigrationInProgress
  - type: Succeeded
    status: "True"
    lastUpdateTime: "2024-03-12T20:29:46Z"
    reason: StorageVersionMigrationSucceeded
  resourceVersion: "84"

```

--------------------------------

### Apply DRA Example Job (kubectl)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

This command applies the example DRA Job configuration to a Kubernetes cluster. It fetches the YAML definition from the provided URL and creates the Job object.

```bash
kubectl apply -f https://k8s.io/examples/dra/dra-example-job.yaml

```

--------------------------------

### Configure Startup and Liveness Probes for Slow Starting Containers

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

This YAML configuration shows how to use both startup and liveness probes to manage applications with long initialization times. The startup probe allows ample time for the application to start, after which the liveness probe takes over for ongoing health checks.

```yaml
ports:
- name: liveness-port
  containerPort: 8080

livenessProbe:
  httpGet:
    path: /healthz
    port: liveness-port
  failureThreshold: 1
  periodSeconds: 10

startupProbe:
  httpGet:
    path: /healthz
    port: liveness-port
  failureThreshold: 30
  periodSeconds: 10


```

--------------------------------

### Kubernetes Reserved Resources Configuration Example

Source: https://kubernetes.io/docs/tasks/administer-cluster/memory-manager

Example configuration for kubeReserved and systemReserved settings in Kubernetes. These settings define the amount of CPU and memory reserved for Kubernetes system daemons and the operating system, respectively. These values are crucial for calculating allocatable resources.

```yaml
kubeReserved: { cpu: "500m", memory: "50Mi" } # half a CPU, 50MiB of memory
systemReserved: { cpu: "500m", memory: "256Mi" } # half a CPU, 256MiB of memory
```

--------------------------------

### Container Startup Command (Shell)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes

This shell command is executed when the container starts. It first creates a file named '/tmp/healthy', then sleeps for 30 seconds, removes the file, and sleeps for another 600 seconds. This sequence is designed to make the liveness probe succeed initially and then fail.

```shell
/bin/sh -c "touch /tmp/healthy; sleep 30; rm -f /tmp/healthy; sleep 600"

```

--------------------------------

### Example Cloud Controller Manager DaemonSet Configuration (Kubernetes)

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This example demonstrates how to configure the cloud-controller-manager as a DaemonSet within a Kubernetes cluster. It assumes masters can run pods and have the 'node-role.kubernetes.io/master' role. This configuration serves as a guideline and may require adjustments for specific cloud environments.

```yaml
# This is an example of how to set up cloud-controller-manager as a Daemonset in your cluster.
# It assumes that your masters can run pods and has the role node-role.kubernetes.io/master
# Note that this Daemonset will not work straight out of the box for your cloud, this is

```

--------------------------------

### Example kube-apiserver Lease object definition

Source: https://kubernetes.io/docs/concepts/architecture/_print

This is an example YAML output for a kube-apiserver Lease object. It shows the API version, kind, metadata (including labels and name), and spec details like the holder identity, lease duration, and renewal time.

```yaml
apiVersion: coordination.k8s.io/v1
kind: Lease
metadata:
  creationTimestamp: "2023-07-02T13:16:48Z"
  labels:
    apiserver.kubernetes.io/identity: kube-apiserver
    kubernetes.io/hostname: master-1
  name: apiserver-07a5ea9b9b072c4a5f3d1c3702
  namespace: kube-system
  resourceVersion: "334899"
  uid: 90870ab5-1ba9-4523-b215-e4d4e662acb1
spec:
  holderIdentity: apiserver-07a5ea9b9b072c4a5f3d1c3702_0c8914f7-0f35-440e-8676-7844977d3a05
  leaseDurationSeconds: 3600
  renewTime: "2023-07-04T21:58:48.065888Z"

```

--------------------------------

### Pod DNS Policy Example: ClusterFirstWithHostNet

Source: https://kubernetes.io/docs/concepts/services-networking/_print

This example demonstrates a Kubernetes Pod configured with `hostNetwork: true` and `dnsPolicy: ClusterFirstWithHostNet`. This policy is necessary for Pods running with host networking to ensure proper DNS resolution within the cluster.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - image: busybox:1.28
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
    name: busybox
  restartPolicy: Always
  hostNetwork: true
  dnsPolicy: ClusterFirstWithHostNet

```

--------------------------------

### Get ClusterRole HTTP Request (Kubernetes API)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Demonstrates an HTTP GET request to retrieve a specific ClusterRole by its name. Requires the 'name' path parameter.

```http
GET /apis/rbac.authorization.k8s.io/v1/clusterroles/{name} HTTP/1.1
Host: kubernetes.default.svc
Authorization: Bearer <token>
```

--------------------------------

### Create Namespace with kubectl

Source: https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/_print

Creates a new Kubernetes namespace named 'quota-pod-example'. This isolates resources for the demonstration.

```bash
kubectl create namespace quota-pod-example
```

--------------------------------

### Get ServiceAccount API Request (HTTP)

Source: https://kubernetes.io/docs/reference/kubernetes-api/authentication-resources/service-account-v1

HTTP GET request to retrieve a specific ServiceAccount by its name and namespace. Requires authentication.

```http
GET /api/v1/namespaces/{namespace}/serviceaccounts/{name} HTTP/1.1
Host: kubernetes.default.svc
Authorization: Bearer <token>
```

--------------------------------

### Drain node with force and grace period using kubectl

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

These examples demonstrate how to use the 'kubectl drain' command to remove pods from a node. The first example forces the drain even if pods are not managed by controllers. The second example specifies a grace period for pod termination.

```bash
# Drain node "foo", even if there are pods not managed by a replication controller, replica set, job, daemon set, or stateful set on it
kubectl drain foo --force

# As above, but abort if there are pods not managed by a replication controller, replica set, job, daemon set, or stateful set, and use a grace period of 15 minutes
kubectl drain foo --grace-period=900
```

--------------------------------

### Kubernetes Runtime Object Conversion with RawExtension (Go)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Demonstrates how to use RawExtension for handling arbitrary driver-specific data in Kubernetes API objects. It shows the conversion process between internal and external struct representations, allowing for flexible data serialization and deserialization.

```Go
package main

import (
	"encoding/json"
	"fmt"
	runtime "k8s.io/apimachinery/pkg/runtime"
)

// Internal package:
type MyAPIObjectInternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin          runtime.Object `json:"myPlugin"`
}

type PluginAInternal struct {
	AOption string `json:"aOption"`
}

// External package:
type MyAPIObjectExternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin          runtime.RawExtension `json:"myPlugin"`
}

type PluginAExternal struct {
	AOption string `json:"aOption"`
}

func main() {
	// Example of serialized JSON data
	jsonData := `{
		"kind":"MyAPIObject",
		"apiVersion":"v1",
		"myPlugin": {
			"kind":"PluginA",
			"aOption":"foo"
		}
	}`

	// Decode into external object
	var externalObj MyAPIObjectExternal
	err := json.Unmarshal([]byte(jsonData), &externalObj)
	if err != nil {
		fmt.Printf("Error unmarshalling external object: %v\n", err)
		return
	}

	fmt.Printf("External Object MyPlugin Kind: %s\n", externalObj.MyPlugin.Kind)

	// Simulate conversion to internal object (simplified)
	// In a real scenario, this would involve pkg/conversion and runtime.Scheme

	// For demonstration, let's manually create an internal object from external data
	var internalPlugin runtime.Object
	if externalObj.MyPlugin.Type == "application/json" {
		var pluginAInternal PluginAInternal
		err = json.Unmarshal(externalObj.MyPlugin.Raw, &pluginAInternal)
		if err != nil {
			fmt.Printf("Error unmarshalling plugin A internal: %v\n", err)
			return
		}
		internalPlugin = &pluginAInternal
	}

	internalObj := MyAPIObjectInternal{
		TypeMeta: externalObj.TypeMeta,
		MyPlugin: internalPlugin,
	}

	fmt.Printf("Internal Object MyPlugin Type: %+v\n", internalObj.MyPlugin)
	if pluginA, ok := internalObj.MyPlugin.(*PluginAInternal);
		ok {
		fmt.Printf("Internal PluginA Option: %s\n", pluginA.AOption)
		}
}

```

--------------------------------

### Create Kubelet Manifest Directory

Source: https://kubernetes.io/docs/tutorials/_print

This command creates the necessary directory for Kubelet manifest files. These manifests define the pods that Kubelet will manage.

```bash
sudo mkdir -p /etc/kubernetes/manifests

```

--------------------------------

### Example of Enabled SidecarContainers Feature Gate Metric

Source: https://kubernetes.io/docs/tutorials/configuration/pod-sidecar-containers

This is an example output from the metrics endpoint indicating that the SidecarContainers feature gate is enabled (value is 1) and is in the BETA stage.

```text
kubernetes_feature_enabled{name="SidecarContainers",stage="BETA"} 1
```

--------------------------------

### Serve Kubernetes Website Locally with Hugo CLI

Source: https://kubernetes.io/docs/contribute/new-content/_print

This command serves the Kubernetes website locally using the Hugo server command. It's a direct alternative for users on Windows or those who cannot use the 'make' command. The '--buildFuture' flag includes content from the future release.

```bash
hugo server --buildFuture
```

--------------------------------

### CEL JSON Patch with Escaped Key Example

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/mutating-admission-policy-v1beta1

This example demonstrates how to safely add a label with special characters (like '/') to the metadata using CEL and `jsonpatch.escapeKey`.

```APIDOC
## JSON Patch with Escaped Key using CEL

### Description
Use the `jsonpatch.escapeKey` CEL function to handle JSON patch path keys that contain special characters like '/' and '~', ensuring correct label application.

### Method
Not Applicable (This describes a configuration language, not an API endpoint)

### Endpoint
Not Applicable

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None (This is a CEL expression)

### Request Example
```cel
[
  JSONPatch{
    op: "add",
    path: "/metadata/labels/" + jsonpatch.escapeKey("example.com/environment"),
    value: "test"
  },
]
```

### Response
#### Success Response (200)
None (This is a configuration definition)

#### Response Example
None
```

--------------------------------

### Kubectl Autocomplete Setup for Fish Shell

Source: https://kubernetes.io/docs/reference/kubectl/_print

This snippet details the process of setting up autocompletion for kubectl in the Fish shell. It requires kubectl version 1.23 or above and involves creating a completion file in the specified directory.

```fish
echo 'kubectl completion fish | source' > ~/.config/fish/completions/kubectl.fish && source ~/.config/fish/completions/kubectl.fish
```

--------------------------------

### Query Pods and Services by Label

Source: https://kubernetes.io/docs/tutorials/_print

Uses label selectors (`-l`) with `kubectl get pods` and `kubectl get services` to filter and retrieve specific resources. This demonstrates efficient resource management using labels.

```bash
kubectl get pods -l app=kubernetes-bootcamp
kubectl get services -l app=kubernetes-bootcamp

```

--------------------------------

### Create Hello World Deployment (YAML)

Source: https://kubernetes.io/docs/tasks/access-application-cluster/_print

Defines a Kubernetes Deployment for the 'hello-app' with two replicas. It specifies the container image and the port the application listens on.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  selector:
    matchLabels:
      run: load-balancer-example
  replicas: 2
  template:
    metadata:
      labels:
        run: load-balancer-example
    spec:
      containers:
        - name: hello-world
          image: us-docker.pkg.dev/google-samples/containers/gke/hello-app:2.0
          ports:
            - containerPort: 8080
              protocol: TCP

```

--------------------------------

### Kubernetes RawExtension for Versioned Structs (Go)

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/_print

Demonstrates how to use RawExtension for handling arbitrary driver-specific data in Kubernetes. It shows the internal and external struct definitions and how data is serialized and deserialized.

```Go
package main

import (
	"encoding/json"
	runtime "k8s.io/apimachinery/pkg/runtime"
)

// Internal package:
type MyAPIObjectInternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin runtime.Object `json:"myPlugin"`
}

type PluginAInternal struct {
	AOption string `json:"aOption"`
}

// External package:
type MyAPIObjectExternal struct {
	runtime.TypeMeta `json:",inline"`
	MyPlugin runtime.RawExtension `json:"myPlugin"`
}

type PluginAExternal struct {
	AOption string `json:"aOption"`
}

func main() {
	// Example of how the JSON might look on the wire:
	jsonOutput := `{
		"kind":"MyAPIObject",
		"apiVersion":"v1",
		"myPlugin": {
			"kind":"PluginA",
			"aOption":"foo"
		}
	}`

	var externalObject MyAPIObjectExternal
	json.Unmarshal([]byte(jsonOutput), &externalObject)

	// In a real scenario, pkg/conversion would handle copying to the internal struct
	// and unpacking the RawExtension.

	// For demonstration, let's simulate the unpacked data:
	var pluginAData PluginAExternal
	json.Unmarshal(externalObject.MyPlugin.Raw, &pluginAData)

	// The runtime.Object in the internal struct would hold a representation of PluginAInternal
	// after conversion.
}

```

--------------------------------

### Get IPAddress Operation (HTTP Request)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Shows how to retrieve a specific IPAddress resource by its name using an HTTP GET request. The name is provided as a path parameter.

```http
GET /apis/networking.k8s.io/v1/ipaddresses/192.168.1.5
Host: kubernetes.default.svc
```

--------------------------------

### Kubernetes Deployment for Web Application (WordPress) with Labels

Source: https://kubernetes.io/docs/concepts/overview/_print

Example of a Kubernetes Deployment for a WordPress web application, including labels for name, instance, version, management tool, component, and the broader application it's part of. This comprehensive labeling aids in managing complex application stacks.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app.kubernetes.io/name: wordpress
    app.kubernetes.io/instance: wordpress-abcxyz
    app.kubernetes.io/version: "4.9.4"
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/component: server
    app.kubernetes.io/part-of: wordpress
...

```

--------------------------------

### Execute command in a Kubernetes pod from a deployment or service

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl

Provides examples of executing a command ('date') in the first pod associated with a deployment ('mydeployment') or a service ('myservice').

```bash
kubectl exec deploy/mydeployment -- date

```

```bash
kubectl exec svc/myservice -- date

```

--------------------------------

### Start an Nginx pod overriding spec with JSON using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts an Nginx pod and overrides its specification with a partial JSON object. This allows for advanced customization of pod settings beyond the standard command-line flags.

```bash
kubectl run nginx --image=nginx --overrides='{ "apiVersion": "v1", "spec": { ... } }'
```

--------------------------------

### Kubernetes CLI Command with Placeholders

Source: https://kubernetes.io/docs/contribute/_print

Demonstrates how to use angle brackets for placeholders in Kubernetes CLI commands. This format helps users understand what information needs to be replaced. The example shows describing a pod and specifying a namespace.

```bash
kubectl describe pod <pod-name> -n <namespace>
```

--------------------------------

### Kubelet TLS Bootstrapping

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

Explains the process of TLS bootstrapping for Kubelets, which automates the creation and signing of client TLS certificates for secure communication with the Kubernetes API server.

```APIDOC
## Kubelet TLS Bootstrapping

### Description
This section describes the TLS bootstrapping process for Kubelets, which simplifies the initialization of worker nodes by automating the creation and signing of client TLS certificates. These certificates are essential for secure communication between Kubelets and the Kubernetes API server.

### Process Overview
When a worker node starts, the Kubelet performs the following steps:
1. Looks for its `kubeconfig` file.
2. Retrieves the API server URL and credentials (TLS key and signed certificate) from the `kubeconfig`.
3. Attempts to communicate with the API server using these credentials.

### Prerequisites for Communication
- The `kubeconfig` file must exist on the local host and contain a key and certificate.
- The certificate must be signed by a Certificate Authority (CA) trusted by the API server.

### Cluster Administrator Responsibilities
- Creating the CA key and certificate.
- Distributing the CA certificate to control plane nodes.
- Creating a unique key and certificate for each Kubelet.
- Signing Kubelet certificates using the CA key.
- Distributing the Kubelet key and signed certificate to the respective nodes.

### TLS Bootstrapping Automation
TLS Bootstrapping aims to simplify and automate steps 3 onwards of the administrator responsibilities, particularly for initializing or scaling a cluster.
```

--------------------------------

### Kubernetes Statusz Structured JSON Response Example

Source: https://kubernetes.io/docs/reference/instrumentation/zpages

An example of the structured JSON response from the `/statusz` endpoint when requested with the appropriate `Accept` header. This format provides machine-readable details about the component's status.

```json
{
  "kind": "Statusz",
  "apiVersion": "config.k8s.io/v1alpha1",
  "metadata": {
    "name": "kube-apiserver"
  },
  "startTime": "2025-10-29T00:30:01Z",
  "uptimeSeconds": 856,
  "goVersion": "go1.23.2",
  "binaryVersion": "1.35.0",
  "emulationVersion": "1.35",
  "paths": [
    "/healthz",
    "/livez",
    "/metrics",
    "/readyz",
    "/statusz",
    "/version"
  ]
}

```

--------------------------------

### Kubectl Commands for Applying and Querying Labels

Source: https://kubernetes.io/docs/concepts/overview/_print

Demonstrates kubectl commands for applying a Kubernetes resource definition, listing pods with specific label columns, and filtering pods based on multiple labels.

```bash
kubectl apply -f examples/guestbook/all-in-one/guestbook-all-in-one.yaml
kubectl get pods -Lapp -Ltier -Lrole
```

```bash
kubectl get pods -lapp=guestbook,role=replica
```

--------------------------------

### Kubernetes ABAC Policy Example

Source: https://kubernetes.io/docs/concepts/security/_print

An example of an Attribute-Based Access Control (ABAC) policy for Kubernetes. This policy defines permissions for a specific user, namespace, resource, and action (read-only).

```json
{
    "apiVersion": "abac.authorization.kubernetes.io/v1beta1",
    "kind": "Policy",
    "spec": {
        "user": "bob",
        "namespace": "projectCaribou",
        "resource": "pods",
        "readonly": true
    }
}

```

--------------------------------

### Kubernetes StatefulSet Example with Headless Service

Source: https://kubernetes.io/docs/concepts/workloads/controllers/statefulset

This example demonstrates the essential components of a Kubernetes StatefulSet, including a Headless Service for network identity and volumeClaimTemplates for persistent storage. It defines a deployment of 3 nginx replicas with stable storage.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  clusterIP: None
  selector:
    app: nginx
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  selector:
    matchLabels:
      app: nginx # has to match .spec.template.metadata.labels
  serviceName: "nginx"
  replicas: 3 # by default is 1
  minReadySeconds: 10 # by default is 0
  template:
    metadata:
      labels:
        app: nginx # has to match .spec.selector.matchLabels
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: registry.k8s.io/nginx-slim:0.24
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "my-storage-class"
      resources:
        requests:
          storage: 1Gi

```

--------------------------------

### Download Kubelet Binary (amd64)

Source: https://kubernetes.io/docs/tutorials/_print

This command downloads the latest stable version of the Kubelet binary for the amd64 architecture. It uses `curl` to fetch the binary from the official Kubernetes release repository.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubelet"

```

--------------------------------

### Example DNS Name to IP Mapping for Control Plane Endpoint

Source: https://kubernetes.io/docs/setup/_print

This example demonstrates how to map a custom DNS name to an IP address for the control-plane endpoint. This mapping is crucial for setting up a shared endpoint for all control-plane nodes, especially when planning for high availability.

```text
192.168.0.102 cluster-endpoint

```

--------------------------------

### Configure Volume Plugin Directory

Source: https://kubernetes.io/docs/reference/config-api/_print

Sets the full path to the directory where Kubelet searches for additional third-party volume plugins. This allows for extending storage capabilities beyond the built-in options.

```go
volumePluginDir string
```

--------------------------------

### Role Rules Examples

Source: https://kubernetes.io/docs/reference/access-authn-authz/rbac

Provides examples of defining rules within Role or ClusterRole objects to grant specific permissions on Kubernetes resources.

```APIDOC
## Role Rules Examples

### Description
These examples illustrate how to define the `rules` section within Role or ClusterRole objects to specify permissions for various Kubernetes resources and non-resource URLs.

### Method
N/A (Declarative Configuration)

### Endpoint
N/A (Declarative Configuration)

### Parameters
N/A

### Request Example
```yaml
# Allow reading "pods" resources in the core API Group:
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]

# Allow reading/writing Deployments in the "apps" API groups:
rules:
- apiGroups: ["apps"]
  resources: ["deployments"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

# Allow reading Pods (core group) and reading/writing Jobs (batch group):
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
- apiGroups: ["batch"]
  resources: ["jobs"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

# Allow reading a ConfigMap named "my-config":
rules:
- apiGroups: [""]
  resources: ["configmaps"]
  resourceNames: ["my-config"]
  verbs: ["get"]

# Allow reading "nodes" resources in the core group:
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "list", "watch"]

# Allow GET and POST to non-resource endpoint /healthz and subpaths:
rules:
- nonResourceURLs: ["/healthz", "/healthz/*"]
  verbs: ["get", "post"]
```

### Response
N/A (Declarative Configuration)

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Querying Services using kubectl

Source: https://kubernetes.io/docs/reference/networking/_print

This snippet demonstrates how to use the kubectl command-line tool to list all services in a Kubernetes cluster. It shows the output format, including ClusterIP, type, and age.

```bash
kubectl get services

```

```text
NAME         TYPE        CLUSTER-IP        EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   2001:db8:1:2::1   <none>        443/TCP   3d1h

```

--------------------------------

### Custom HPA Downscale Stabilization Window

Source: https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale

Example of how to set a custom downscale stabilization window for an HPA. This specific example sets the window to 60 seconds (1 minute).

```yaml
behavior:
  scaleDown:
    stabilizationWindowSeconds: 60

```

--------------------------------

### Apply DRA example Job using kubectl

Source: https://kubernetes.io/docs/tasks/configure-pod-container/assign-resources/allocate-devices-dra

This command applies the DRA example Job to your Kubernetes cluster. Ensure you have the necessary DRA device plugin configured and that the referenced `resourceClaimTemplate.yaml` and `resourceClaim.yaml` exist.

```bash
kubectl apply -f https://k8s.io/examples/dra/dra-example-job.yaml

```

--------------------------------

### GET /api/v1/namespaces/{namespace}/limitranges

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Lists all LimitRanges within a specified namespace. This is useful for getting an overview of resource usage constraints applied across different resources in a namespace.

```APIDOC
## GET /api/v1/namespaces/{namespace}/limitranges

### Description
Lists all LimitRanges within a specified namespace. This is useful for getting an overview of resource usage constraints applied across different resources in a namespace.

### Method
GET

### Endpoint
/api/v1/namespaces/{namespace}/limitranges

### Parameters
#### Path Parameters
- **namespace** (string) - Required - Namespace

#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks requests watch events with a time constraint.
- **continue** (string) - Optional - continue may be set to the last token returned by the server in order to continue the list from the same point onwards.
- **fieldSelector** (string) - Optional - A selector to restrict the list of returned objects by their fields. Supported fields are: metadata.name, metadata.namespace, metadata.uid, spec.name, spec.namespace, spec.type.
- **labelSelector** (string) - Optional - A selector to restrict the list of returned objects by their labels. Supports '=', '==', and '!='.
- **limit** (integer) - Optional - limit is a maximum number of responses to return for a list call. If more items exist, the server will set the continue token to be used for retrieving the next page.
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and used for the human-readable format.
- **resourceVersion** (string) - Optional - resourceVersion sets the identity of a resource instance to be fetched. The server will return that instance if it matches the requested resourceVersion.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines how resourceVersion is matched against existing data.
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents=true indicates that the server should send initial events in a watch stream. This is useful for clients that need to receive all events from the beginning of the stream.
- **timeoutSeconds** (integer) - Optional - timeoutSeconds long-running requests have a timeout of 30 seconds. Set to 0 to indicate never timeout.
- **watch** (boolean) - Optional - Watch for changes to the specified resource.

### Response
#### Success Response (200)
- **LimitRangeList** (object) - OK

#### Response Example
{
  "example": "{\n  \"apiVersion\": \"v1\",\n  \"kind\": \"LimitRangeList\",\n  \"metadata\": {\n    \"resourceVersion\": \"a1b2c3d4e5f6\"\n  },\n  \"items\": [\n    {\n      \"apiVersion\": \"v1\",\n      \"kind\": \"LimitRange\",\n      \"metadata\": {\n        \"name\": \"example-limitrange\",\n        \"namespace\": \"default\"\n      },\n      \"spec\": {\n        \"limits\": [\n          {\n            \"type\": \"Container\",\n            \"max\": {\n              \"cpu\": \"1\",\n              \"memory\": \"1Gi\"\n            }\n          }\n        ]\n      }\n    }\n  ]\n}"
}
```

--------------------------------

### Examples of Setting Kubeconfig Values

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_config/_print

Demonstrates various ways to use 'kubectl config set' to update cluster server addresses, certificate authority data, context cluster assignments, and user client key data, including the use of base64 encoding and the --set-raw-bytes flag.

```bash
# Set the server field on the my-cluster cluster to https://1.2.3.4
kubectl config set clusters.my-cluster.server https://1.2.3.4

# Set the certificate-authority-data field on the my-cluster cluster
kubectl config set clusters.my-cluster.certificate-authority-data $(echo "cert_data_here" | base64 -i -)

# Set the cluster field in the my-context context to my-cluster
kubectl config set contexts.my-context.cluster my-cluster

# Set the client-key-data field in the cluster-admin user using --set-raw-bytes option
kubectl config set users.cluster-admin.client-key-data cert_data_here --set-raw-bytes=true
```

--------------------------------

### Kubectl Rollout History Examples

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

Illustrates how to use the `kubectl rollout history` command to view the revision history of Kubernetes deployments and specific daemonset revisions.

```bash
# View the rollout history of a deployment
kubectl rollout history deployment/abc

# View the details of daemonset revision 3
kubectl rollout history daemonset/abc --revision=3
```

--------------------------------

### Remove kubectl Checksum File

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Deletes the downloaded kubectl checksum file after successful installation and validation. This helps keep the download directory clean.

```bash
rm kubectl.sha256
```

--------------------------------

### Example: Local Image Update with Output

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_set/kubectl_set_image

This example demonstrates updating the 'nginx' container image to 'nginx:1.9.1' from a local file without contacting the Kubernetes API server. The --local flag enables local execution, and -o yaml specifies the output format. This is useful for testing or previewing changes.

```bash
kubectl set image -f path/to/file.yaml nginx=nginx:1.9.1 --local -o yaml
```

--------------------------------

### Cleanup Kubelet Service and Files

Source: https://kubernetes.io/docs/tutorials/_print

These commands provide a comprehensive cleanup procedure for the kubelet service and associated configuration and data directories. This is useful for removing a standalone kubelet installation.

```bash
sudo systemctl disable --now kubelet.service
sudo systemctl daemon-reload
sudo rm /etc/systemd/system/kubelet.service
sudo rm /usr/bin/kubelet
sudo rm -rf /etc/kubernetes
sudo rm -rf /var/lib/kubelet
sudo rm -rf /var/log/containers
sudo rm -rf /var/log/pods

```

--------------------------------

### Container Startup Probe

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/_print

Configures a startup probe to ensure a container has successfully initialized. Other probes are not executed until the startup probe succeeds. Failure restarts the pod.

```APIDOC
## GET /api/v1/namespaces/{namespace}/pods/{podName}/startupProbe

### Description
Retrieves the startup probe configuration for a specific container within a pod.

### Method
GET

### Endpoint
/api/v1/namespaces/{namespace}/pods/{podName}/startupProbe

### Parameters
#### Path Parameters
- **namespace** (string) - Required - The namespace of the pod.
- **podName** (string) - Required - The name of the pod.

### Response
#### Success Response (200)
- **probe** (Probe) - The startup probe configuration.

#### Response Example
```json
{
  "probe": {
    "initialDelaySeconds": 10,
    "periodSeconds": 20,
    "timeoutSeconds": 5,
    "failureThreshold": 5,
    "tcpSocket": {
      "port": 8000
    }
  }
}
```
```

--------------------------------

### Example: Delete Minikube Cluster

Source: https://kubernetes.io/docs/reference/kubectl/generated/_print

This example shows how to use the 'kubectl config delete-cluster' command to remove the 'minikube' cluster configuration from the kubeconfig file.

```bash
kubectl config delete-cluster minikube
```

--------------------------------

### Minimal GatewayClass Example (Kubernetes YAML)

Source: https://kubernetes.io/docs/concepts/services-networking/gateway

This example demonstrates a minimal GatewayClass resource. It defines a class of gateways and specifies the controller responsible for managing them. The `controllerName` field is crucial for associating Gateways with their implementing controller.

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: GatewayClass
metadata:
  name: example-class
spec:
  controllerName: example.com/gateway-controller

```

--------------------------------

### Example Signed ConfigMap Structure

Source: https://kubernetes.io/docs/reference/access-authn-authz/bootstrap-tokens

This is an example of a ConfigMap that has been signed. It includes a 'jws-kubeconfig-07401b' field containing the JWS signature and a 'kubeconfig' field with the cluster information.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: cluster-info
  namespace: kube-public
data:
  jws-kubeconfig-07401b: eyJhbGciOiJIUzI1NiIsImtpZCI6IjA3NDAxYiJ9..tYEfbo6zDNo40MQE07aZcQX2m3EB2rO3NuXtxVMYm9U
  kubeconfig: |
    apiVersion: v1
    clusters:
    - cluster:
        certificate-authority-data: <really long certificate data>
        server: https://10.138.0.2:6443
      name: ""
    contexts: []
    current-context: ""
    kind: Config
    preferences: {}
    users: []

```

--------------------------------

### Get ControllerRevision API Request (HTTP)

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/_print

Demonstrates the HTTP GET request to retrieve a specific ControllerRevision by its name and namespace. It outlines the required path parameters and optional query parameters.

```http
GET /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name} HTTP/1.1
Host: example.com
Accept: application/json

# Query Parameters:
# pretty: string (optional)
```

--------------------------------

### Kubernetes ClusterRole and RoleBinding Example for Role Granting

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

This example demonstrates a Kubernetes ClusterRole that grants permissions to create RoleBindings and bind ClusterRoles, and a RoleBinding that allows a specific user to grant predefined roles within a namespace. It addresses the scenario where a user needs to grant permissions they might not directly possess.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: role-grantor
rules:
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["rolebindings"]
  verbs: ["create"]
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["clusterroles"]
  verbs: ["bind"]
  # omit resourceNames to allow binding any ClusterRole
  resourceNames: ["admin","edit","view"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: role-grantor-binding
  namespace: user-1-namespace
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: role-grantor
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: user-1

```

--------------------------------

### Kubernetes API GET Request for ServiceList

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

Demonstrates a GET request to the Kubernetes API to retrieve a list of Services. The response is a ServiceList object containing metadata and an array of Service items.

```http
GET /api/v1/services

```

```json
{
  "kind": "ServiceList",
  "apiVersion": "v1",
  "metadata": {
    "resourceVersion": "2947301"
  },
  "items": [
    {
      "metadata": {
        "name": "kubernetes",
        "namespace": "default",
...
      "metadata": {
        "name": "kube-dns",
        "namespace": "kube-system",
...

```

--------------------------------

### Kubernetes CLI Command to Deploy Application

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/_print

This command deploys a sample 'hello-app' application to the Kubernetes cluster using a specified container image and exposing it on port 8080. It's a prerequisite for testing API access or other cluster functionalities.

```bash
kubectl create deployment hello-app --image=gcr.io/google-samples/hello-app:2.0 --port=8080
```

--------------------------------

### List Kubectl Plugins

Source: https://kubernetes.io/docs/reference/kubectl/_print

Lists all available kubectl plugins found on the user's PATH. Plugins are identified as executable files starting with 'kubectl-'.

```bash
kubectl plugin list
```

--------------------------------

### Apply Configuration from Kustomization Directory

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

Applies resources defined in a kustomization directory, which typically contains a kustomization.yaml file. This allows for managing complex configurations using kustomize.

```bash
kubectl apply -k dir/
```

--------------------------------

### Get CertificateSigningRequest Status API Request

Source: https://kubernetes.io/docs/reference/kubernetes-api/authentication-resources/certificate-signing-request-v1

Retrieves the status of a specific CertificateSigningRequest. This operation uses an HTTP GET request targeting the '/status' subresource and requires the 'name' parameter in the path.

```http
GET /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/status HTTP/1.1
Host: your-kubernetes-api-host


```

--------------------------------

### Kubectl Get Command

Source: https://kubernetes.io/docs/reference/kubectl

Illustrates common uses of the `kubectl get` command for listing resources in various formats and with different filters.

```APIDOC
## Kubectl Get Command

### Description
The `kubectl get` command is used to list one or more resources. It supports various output formats and filtering options.

### Method
N/A (This describes command-line usage, not a specific HTTP method)

### Endpoint
N/A (This describes command-line usage, not a specific API endpoint)

### Parameters
#### Query Parameters
- **-o <output_format>** (string) - Optional - Specifies the output format (e.g., `wide`, `yaml`, `json`).
- **--field-selector=<field_selector>** (string) - Optional - Filters resources based on field values.

### Request Example
#### List all pods
```bash
kubectl get pods
```

#### List all pods with additional info (`-o wide`)
```bash
kubectl get pods -o wide
```

#### List a specific replication controller (alias `rc`)
```bash
kubectl get replicationcontroller <rc-name>
```

#### List multiple resource types
```bash
kubectl get rc,services
```

#### List all pods on a specific node
```bash
kubectl get pods --field-selector=spec.nodeName=server01
```

### Response
#### Success Response (200)
- **List of Resources** - Information about the requested resources, formatted as specified.

#### Response Example (for `kubectl get pods`)
```
NAME       READY   STATUS    RESTARTS   AGE
pod-1      1/1     Running   0          5m
pod-2      1/1     Running   0          3m
```
```

--------------------------------

### kubectl run Examples: Dry Run and Overrides

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/_print

Shows how to perform a dry run to preview the Kubernetes API objects that would be created without actually deploying them. Also demonstrates using the `--overrides` flag to apply partial JSON configurations to the pod specification.

```bash
# Dry run; print the corresponding API objects without creating them
kubectl run nginx --image=nginx --dry-run=client

# Start a nginx pod, but overload the spec with a partial set of values parsed from JSON
kubectl run nginx --image=nginx --overrides='{ "apiVersion": "v1", "spec": { ... } }'
```

--------------------------------

### Describe Node to Verify Extended Resources

Source: https://kubernetes.io/docs/tasks/administer-cluster/extended-resource-node

Displays detailed information about a specific Kubernetes node, including its advertised capacity. This command is used to confirm that the extended resource, such as 'example.com/dongle', has been successfully added and is visible in the node's capacity.

```bash
kubectl describe node <your-node-name>

```

--------------------------------

### Running the update-imported-docs Tool

Source: https://kubernetes.io/docs/contribute/generate-ref-docs/_print

Command-line instructions for executing the `update-imported-docs.py` script. It requires the path to a configuration file and the release version as arguments. An example demonstrates its usage.

```bash
cd <web-base>/update-imported-docs
./update-imported-docs.py <configuration-file.yml> <release-version>

# Example:
./update-imported-docs.py reference.yml 1.17

```

--------------------------------

### GET /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Lists or watches all ValidatingWebhookConfiguration objects.

```APIDOC
## GET /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations

### Description
Lists or watches objects of kind ValidatingWebhookConfiguration.

### Method
GET

### Endpoint
/apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks requests watch events with a time limit.
- **continue** (string) - Optional - continue lists of objects, the server's next value for the watch. Only when empty list returned.
- **fieldSelector** (string) - Optional - A selector to restrict the list of returned objects by their fields. Supported fields are: metadata.creationTimestamp, metadata.name, metadata.namespace, metadata.resourceVersion, metadata.uid.
- **labelSelector** (string) - Optional - A selector to restrict the list of returned objects by their labels. Supported operators are Equals, NotEquals, In, NotIn, Exists, DoesNotExist.
- **limit** (integer) - Optional - limit is the maximum number of results to return from this API call. Default is 10.
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be returned to the caller with the appropriate Content-Type header.
- **resourceVersion** (string) - Optional - resourceVersion sets the identity of a resource instance that is the target of the watch. If the resource is older than the specified resourceVersion, the watch will be closed and the API will return an error.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines how resourceVersion values are matched between the client and server. Possible values are: "", "Exact", "Approximate".
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents=true ensures that the watch event stream includes events that occurred prior to the watch being established.
- **timeoutSeconds** (integer) - Optional - timeoutSeconds long-running requests. Deprecated: prefer the appropriate timeout context headers.
- **watch** (boolean) - Optional - Watch for changes to the requested resource.

### Response
#### Success Response (200)
- **ValidatingWebhookConfigurationList** - A list of ValidatingWebhookConfiguration objects.

#### Response Example
```json
{
  "apiVersion": "admissionregistration.k8s.io/v1",
  "kind": "ValidatingWebhookConfigurationList",
  "items": [
    {
      "apiVersion": "admissionregistration.k8s.io/v1",
      "kind": "ValidatingWebhookConfiguration",
      "metadata": {
        "name": "example-webhook-1"
      },
      "webhooks": [
        {
          "name": "mutate.example.com",
          "clientConfig": {
            "service": {
              "name": "my-service-1",
              "namespace": "my-namespace",
              "path": "/mutate"
            },
            "caBundle": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCg=="
          },
          "rules": [
            {
              "operations": [ "CREATE" ],
              "apiGroups": [ "apps" ],
              "apiVersions": [ "v1" ],
              "resources": [ "deployments" ]
            }
          ]
        }
      ]
    },
    {
      "apiVersion": "admissionregistration.k8s.io/v1",
      "kind": "ValidatingWebhookConfiguration",
      "metadata": {
        "name": "example-webhook-2"
      },
      "webhooks": [
        {
          "name": "validate.example.com",
          "clientConfig": {
            "service": {
              "name": "my-service-2",
              "namespace": "my-namespace",
              "path": "/validate"
            },
            "caBundle": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCg=="
          },
          "rules": [
            {
              "operations": [ "UPDATE" ],
              "apiGroups": [ "core" ],
              "apiVersions": [ "v1" ],
              "resources": [ "pods" ]
            }
          ]
        }
      ]
    }
  ]
}
```

#### Error Response (401)
- **Unauthorized** - Indicates that the request lacks valid authentication credentials.
```

--------------------------------

### Describe Node Resources for Pod (kubectl)

Source: https://kubernetes.io/docs/concepts/scheduling-eviction/_print

This kubectl command provides details about the resources allocated to the 'test-pod' on the node it's scheduled to. It displays the total CPU and Memory requests and limits, which include the Pod's overhead, offering insight into how the scheduler made its decision.

```bash
kubectl describe node | grep test-pod -B2
```

--------------------------------

### Kubernetes Certificate File Paths and Arguments

Source: https://kubernetes.io/docs/setup/best-practices/certificates

This table lists the default CN, recommended key and certificate paths, and the corresponding command-line arguments for various Kubernetes components. It helps in understanding where to place certificate files and how to reference them in component configurations.

```text
DefaultCN| recommendedkeypath| recommendedcertpath| command| keyargument| certargument  
etcd-ca| etcd/ca.key| etcd/ca.crt| kube-apiserver| | --etcd-cafile  
kube-apiserver-etcd-client| apiserver-etcd-client.key| apiserver-etcd-client.crt| kube-apiserver| --etcd-keyfile| --etcd-certfile  
kubernetes-ca| ca.key| ca.crt| kube-apiserver| | --client-ca-file  
kubernetes-ca| ca.key| ca.crt| kube-controller-manager| --cluster-signing-key-file| --client-ca-file,--root-ca-file,--cluster-signing-cert-file  
kube-apiserver| apiserver.key| apiserver.crt| kube-apiserver| --tls-private-key-file| --tls-cert-file  
kube-apiserver-kubelet-client| apiserver-kubelet-client.key| apiserver-kubelet-client.crt| kube-apiserver| --kubelet-client-key| --kubelet-client-certificate  
front-proxy-ca| front-proxy-ca.key| front-proxy-ca.crt| kube-apiserver| | --requestheader-client-ca-file  
front-proxy-ca| front-proxy-ca.key| front-proxy-ca.crt| kube-controller-manager| | --requestheader-client-ca-file  
front-proxy-client| front-proxy-client.key| front-proxy-client.crt| kube-apiserver| --proxy-client-key-file| --proxy-client-cert-file  
etcd-ca| etcd/ca.key| etcd/ca.crt| etcd| | --trusted-ca-file,--peer-trusted-ca-file  
kube-etcd| etcd/server.key| etcd/server.crt| etcd| --key-file| --cert-file  
kube-etcd-peer| etcd/peer.key| etcd/peer.crt| etcd| --peer-key-file| --peer-cert-file  
etcd-ca| | etcd/ca.crt| etcdctl| | --cacert  
kube-etcd-healthcheck-client| etcd/healthcheck-client.key| etcd/healthcheck-client.crt| etcdctl| --key| --cert  
```

--------------------------------

### Delete DRA example Job using kubectl

Source: https://kubernetes.io/docs/tasks/configure-pod-container/assign-resources/allocate-devices-dra

This command deletes the DRA example Job previously applied to the cluster. It uses the same URL as the apply command.

```bash
kubectl delete -f https://k8s.io/examples/dra/dra-example-job.yaml

```

--------------------------------

### Forbidden Field Validation Tag Example

Source: https://kubernetes.io/docs/reference/using-api/declarative-validation

Provides an example of the '+k8s:forbidden' tag, which signifies that a particular field must not be specified. This tag is useful for fields that should not be present during creation or updates of a resource.

```go
type MyStruct struct {
    // +k8s:forbidden
    MyField string `json:"myField"`
}

```

--------------------------------

### ApplyConfiguration Mutation Example (CEL)

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/_print

Demonstrates how to define an ApplyConfiguration mutation using a CEL expression. This example sets the 'serviceAccountName' field within the 'spec' of an object. Apply configurations are used for structured merge diff operations.

```cel
Object{
  spec: Object.spec{
    serviceAccountName: "example"
  }
}

```

--------------------------------

### Per-Namespace Parameters and Parameter Selectors

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

Explains how to configure parameters on a per-namespace basis and how to use label selectors to dynamically select parameter resources.

```APIDOC
## Per-Namespace Parameters and Parameter Selectors

### Description
This section details the configuration options for parameter resources in ValidatingAdmissionPolicies, focusing on per-namespace parameter binding and the use of label selectors for dynamic parameter selection.

### Method
N/A (Configuration Guide)

### Endpoint
N/A (Configuration Guide)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
N/A

### Notes
- **Per-Namespace Parameters**: If a `namespace` is specified for a binding's `paramRef`, parameters are only searched within that namespace.
- If `namespace` is not specified in `ValidatingAdmissionPolicyBinding`, the API server searches for parameters in the namespace of the resource being admitted.
- **Parameter Selector**: A label selector can be used instead of a `name` in `paramRef` to select multiple parameter resources matching the selector.
- If multiple parameters match the selector, policy rules are evaluated for each, and results are ANDed together.
- If `namespace` is provided with a selector, only objects in that namespace are eligible.
- If `namespace` is empty and `paramKind` is namespace-scoped, the request's namespace is used for selection.
```

--------------------------------

### Download Kubelet Binary

Source: https://kubernetes.io/docs/tutorials/cluster-management/_print

Downloads the latest stable release of the kubelet binary for either x86-64 or ARM64 architecture. This step is crucial for setting up the Kubernetes node agent.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubelet"

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubelet"
```

--------------------------------

### Install Bash Completion on Linux

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl

Enables bash completion for kubectl on Linux systems. It requires the 'bash-completion' package to be installed via the distribution's package manager. The completion code is loaded into the current shell using the 'source' command.

```bash
source <(kubectl completion bash)

```

--------------------------------

### hostPath DirectoryOrCreate and FileOrCreate Configuration Example

Source: https://kubernetes.io/docs/concepts/storage/volumes

This Kubernetes Pod manifest demonstrates the use of 'DirectoryOrCreate' and 'FileOrCreate' types for hostPath volumes. It configures mounting a directory and a file, ensuring their creation if they do not exist on the host. This example highlights the caution that 'FileOrCreate' does not create parent directories.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-webserver
spec:
  os: { name: linux }
  nodeSelector:
    kubernetes.io/os: linux
  containers:
  - name: test-webserver
    image: registry.k8s.io/test-webserver:latest
    volumeMounts:
    - mountPath: /var/local/aaa
      name: mydir
    - mountPath: /var/local/aaa/1.txt
      name: myfile
  volumes:
  - name: mydir
    hostPath:
      # Ensure the file directory is created.
      path: /var/local/aaa
      type: DirectoryOrCreate
  - name: myfile
    hostPath:
      path: /var/local/aaa/1.txt
      type: FileOrCreate

```

--------------------------------

### Get StorageVersionMigration Status (HTTP Request)

Source: https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/storage-version-migration-v1beta1

This outlines the HTTP GET request to fetch the status of a specific StorageVersionMigration resource. It targets the '/status' subresource of the migration.

```http
GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}/status
```

--------------------------------

### Kubernetes API: Get StorageClass (HTTP)

Source: https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/storage-class-v1

HTTP GET request to retrieve a specific StorageClass by its name. Returns a 200 OK with the StorageClass object or an error code.

```http
GET /apis/storage.k8s.io/v1/storageclasses/{name}
```

--------------------------------

### Apply ResourceQuota and Deploy with kubectl

Source: https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/_print

Applies a ResourceQuota manifest to the 'quota-pod-example' namespace and then applies a Deployment manifest. The Deployment attempts to create 3 replicas, but the ResourceQuota will limit it to 2.

```bash
kubectl apply -f https://k8s.io/examples/admin/resource/quota-pod.yaml --namespace=quota-pod-example
```

```bash
kubectl apply -f https://k8s.io/examples/admin/resource/quota-pod-deployment.yaml --namespace=quota-pod-example
```

--------------------------------

### Loop Test Queries to Demonstrate Load Balancing

Source: https://kubernetes.io/docs/tasks/run-application/run-replicated-stateful-application

Continuously sends test queries to the MySQL read replica service to demonstrate connection distribution across available servers. It selects the server ID and current time.

```bash
kubectl run mysql-client-loop --image=mysql:5.7 -i -t --rm --restart=Never -- \
  bash -ic "while sleep 1; do mysql -h mysql-read -e 'SELECT @@server_id,NOW()'; done"

```

--------------------------------

### Start Containerd Service on Windows

Source: https://kubernetes.io/docs/tasks/administer-cluster/migrating-from-dockershim/_print

These PowerShell commands register containerd as a Windows service and then start the service. This is the final step in setting up containerd on a Windows node.

```powershell
.\containerd.exe --register-service
Start-Service containerd

```

--------------------------------

### Access Hello World Application (curl)

Source: https://kubernetes.io/docs/tutorials/_print

This command uses curl to access the Hello World application via its external IP address and port. Replace '<external-ip>' and '<port>' with the values obtained from the service description.

```bash
curl http://<external-ip>:<port>

```

--------------------------------

### Create Kubernetes Deployment with Command

Source: https://kubernetes.io/docs/reference/kubectl/kubectl-cmds

Shows how to create a Kubernetes deployment and specify a command to run within the container. This allows for custom initialization or execution logic.

```bash
kubectl create deployment my-dep --image=busybox -- date

```

--------------------------------

### Install CNI Plugins

Source: https://kubernetes.io/docs/setup/_print

This snippet downloads and installs the CNI (Container Network Interface) plugins, which are essential for most pod network configurations in Kubernetes. It specifies the version and architecture of the plugins and extracts them to the designated directory.

```bash
CNI_PLUGINS_VERSION="v1.3.0"
ARCH="amd64"
DEST="/opt/cni/bin"
sudo mkdir -p "$DEST"
curl -L "https://github.com/containernetworking/plugins/releases/download/${CNI_PLUGINS_VERSION}/cni-plugins-linux-${ARCH}-${CNI_PLUGINS_VERSION}.tgz" | sudo tar -C "$DEST" -xz
```

--------------------------------

### GET /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Lists or watches all MutatingWebhookConfiguration objects.

```APIDOC
## GET /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations

### Description
Lists or watches objects of kind MutatingWebhookConfiguration.

### Method
GET

### Endpoint
/apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks
- **continue** (string) - Optional - continue
- **fieldSelector** (string) - Optional - fieldSelector
- **labelSelector** (string) - Optional - labelSelector
- **limit** (integer) - Optional - limit
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be returned from the server's renderers rather than the data itself.
- **resourceVersion** (string) - Optional - resourceVersion
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents
- **timeoutSeconds** (integer) - Optional - timeoutSeconds
- **watch** (boolean) - Optional - watch

### Response
#### Success Response (200)
- **MutatingWebhookConfigurationList** - A list of MutatingWebhookConfiguration objects.

#### Error Response
- **401** - Unauthorized
```

--------------------------------

### Uninstall kubectl using Homebrew

Source: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos

Uninstalls `kubectl` from macOS if it was installed using the Homebrew package manager. This command removes `kubectl` and its associated files managed by Homebrew.

```shell
brew remove kubectl
```

--------------------------------

### Configure Multiple Pod Security Standard Checks

Source: https://kubernetes.io/docs/tutorials/security/_print

Sets up multiple Pod Security Standard checks on a namespace. This example enforces the 'baseline' standard while warning and auditing for the 'restricted' standard, using the latest versions for all policies.

```bash
kubectl label --overwrite ns example \
  pod-security.kubernetes.io/enforce=baseline \
  pod-security.kubernetes.io/enforce-version=latest \
  pod-security.kubernetes.io/warn=restricted \
  pod-security.kubernetes.io/warn-version=latest \
  pod-security.kubernetes.io/audit=restricted \
  pod-security.kubernetes.io/audit-version=latest

```

--------------------------------

### GET /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations

Source: https://kubernetes.io/docs/reference/kubernetes-api/extend-resources/mutating-webhook-configuration-v1

Lists or watches all MutatingWebhookConfiguration objects.

```APIDOC
## GET /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations

### Description
Lists or watches objects of kind MutatingWebhookConfiguration.

### Method
GET

### Endpoint
/apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks
- **continue** (string) - Optional - continue
- **fieldSelector** (string) - Optional - fieldSelector
- **labelSelector** (string) - Optional - labelSelector
- **limit** (integer) - Optional - limit
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and paginated.
- **resourceVersion** (string) - Optional - resourceVersion
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents
- **timeoutSeconds** (integer) - Optional - timeoutSeconds
- **watch** (boolean) - Optional - Watch for changes to the requested object.

### Response
#### Success Response (200)
- **MutatingWebhookConfigurationList** - A list of MutatingWebhookConfiguration objects.

#### Response Example
```json
{
  "apiVersion": "admissionregistration.k8s.io/v1",
  "kind": "MutatingWebhookConfigurationList",
  "items": [
    {
      "apiVersion": "admissionregistration.k8s.io/v1",
      "kind": "MutatingWebhookConfiguration",
      "metadata": {
        "name": "example-webhook-1"
      },
      "webhooks": [
        {
          "name": "mutate.example.com",
          "clientConfig": {
            "service": {
              "name": "mutating-svc",
              "namespace": "default",
              "path": "/mutate"
            }
          },
          "rules": [
            {
              "operations": ["CREATE"],
              "apiGroups": ["*"],
              "apiVersions": ["*"],
              "resources": ["pods"],
              "scope": "*"
            }
          ],
          "timeoutSeconds": 10
        }
      ]
    }
  ]
}
```
```

--------------------------------

### Example Request with Authenticating Proxy Headers

Source: https://kubernetes.io/docs/reference/access-authn-authz/authentication

An example HTTP request demonstrating how headers are sent to an API server configured with an authenticating reverse proxy. These headers provide user identity and group information to the API server.

```http
GET / HTTP/1.1
X-Remote-User: fido
X-Remote-Group: dogs
X-Remote-Group: dachshunds
X-Remote-Extra-Acme.com%2Fproject: some-project
X-Remote-Extra-Scopes: openid
X-Remote-Extra-Scopes: profile

```

--------------------------------

### Prepare CA and Service Account Files

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Initializes the necessary Certificate Authority (CA) and service account key pairs for a Kubernetes control plane node using kubeadm. These commands populate the default certificate directories.

```bash
sudo kubeadm init phase certs ca
sudo kubeadm init phase certs etcd-ca
sudo kubeadm init phase certs front-proxy-ca
sudo kubeadm init phase certs sa
```

--------------------------------

### Reset kubeadm Installation (kubeadm)

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

This command resets the state installed by kubeadm on a node. It cleans up most Kubernetes components but does not reset iptables or IPVS rules. This is a crucial step before removing a node or reinitializing the cluster.

```bash
kubeadm reset
```

--------------------------------

### Apply Pod Security Policy to Namespace

Source: https://kubernetes.io/docs/tutorials/security/_print

Applies a Pod Security Standards configuration to a specific namespace using 'kubectl'. This example demonstrates enforcing the 'baseline' Pod Security Standard within the 'example' namespace. It requires 'kubectl' and a pre-configured namespace.

```bash
kubectl create ns example
```

--------------------------------

### Kubernetes API ServiceList Response Example

Source: https://kubernetes.io/docs/reference/using-api/_print

This example demonstrates the structure of a typical Kubernetes API response when listing Services. The 'kind' is 'ServiceList', and the 'items' array contains individual Service objects. This is the standard API representation for collections of a specific resource type.

```json
{
  "kind": "ServiceList",
  "apiVersion": "v1",
  "metadata": {
    "resourceVersion": "2947301"
  },
  "items": [
    {
      "metadata": {
        "name": "kubernetes",
        "namespace": "default",
...
      },
      "metadata": {
        "name": "kube-dns",
        "namespace": "kube-system",
...
    }
  ]
}
```

--------------------------------

### List Kubernetes Resources with Kubectl Get

Source: https://kubernetes.io/docs/reference/kubectl/kubectl-cmds

Retrieves and displays information about Kubernetes resources. Supports various output formats (ps, wide, json, yaml, custom-columns, template) and filtering by name, label, or file.

```bash
kubectl get pods
```

```bash
kubectl get pods -o wide
```

```bash
kubectl get replicationcontroller web
```

```bash
kubectl get deployments.v1.apps -o json
```

```bash
kubectl get -o json pod web-pod-13je7
```

```bash
kubectl get -f pod.yaml -o json
```

```bash
kubectl get -k dir/
```

```bash
kubectl get -o template pod/web-pod-13je7 --template={{.status.phase}}
```

```bash
kubectl get pod test-pod -o custom-columns=CONTAINER:.spec.containers[0].name,IMAGE:.spec.containers[0].image
```

```bash
kubectl get rc,services
```

```bash
kubectl get rc/web service/frontend pods/web-pod-13je7
```

```bash
kubectl get pod web-pod-13je7 --subresource status
```

--------------------------------

### Write Data to Volume and Install Packages (Bash)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-volume-storage

These commands are executed within a Pod's container. The first command writes the string 'Hello' to a file named 'test-file' in the '/data/redis' directory, demonstrating data writing to the mounted volume. The subsequent commands update package lists and install the 'procps' package to enable the 'ps aux' command for process inspection.

```bash
cd /data/redis/
echo Hello > test-file

apt-get update
apt-get install procps
ps aux
```

--------------------------------

### Probe Configuration Fields

Source: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes

An in-depth explanation of the fields available for configuring startup, liveness, and readiness probes, including their default values, minimum values, and impact on probe behavior.

```APIDOC
## Probe Configuration Fields

Probes offer several fields for fine-grained control over checks:

### `initialDelaySeconds`
- **Description**: Number of seconds after the container starts before probes are initiated. If a startup probe is defined, liveness and readiness probe delays begin only after the startup probe succeeds. Defaults to 0. Minimum value is 0.

### `periodSeconds`
- **Description**: How often (in seconds) to perform the probe. Defaults to 10 seconds. Minimum value is 1. The `ReadinessProbe` may execute more frequently than `periodSeconds` while a container is not Ready, to expedite readiness.

### `timeoutSeconds`
- **Description**: Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1.

### `successThreshold`
- **Description**: Minimum consecutive successes for the probe to be considered successful after failing. Defaults to 1. Must be 1 for liveness and startup probes. Minimum value is 1.

### `failureThreshold`
- **Description**: After a probe fails `failureThreshold` times consecutively, Kubernetes considers the check failed. Defaults to 3. Minimum value is 1.
  - For startup or liveness probes, failure triggers a container restart, respecting `terminationGracePeriodSeconds`.
  - For readiness probes, failure sets the Pod's `Ready` condition to `false` but the container continues running and probes are still executed.
```

--------------------------------

### Check MAC Address

Source: https://kubernetes.io/docs/setup/production-environment/_print

These commands display the MAC addresses of network interfaces on a system. Unique MAC addresses are vital for Kubernetes to identify nodes correctly during installation. If not unique, the installation may fail.

```bash
ip link
```

```bash
ifconfig -a
```

--------------------------------

### Enable Signed Kubelet Serving Certificates with Kubeadm Init

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

This configuration snippet is used with `kubeadm init` to enable the bootstrap of kubelet serving certificates. It requires setting `serverTLSBootstrap: true` in both `ClusterConfiguration` and `KubeletConfiguration`.

```yaml
apiVersion: kubeadm.k8s.io/v1beta4
kind: ClusterConfiguration
---
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
serverTLSBootstrap: true

```

--------------------------------

### PersistentVolumeClaim Manifest Example

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

An example YAML manifest for a PersistentVolumeClaim (PVC) named 'cat-pictures-pvc'. It specifies the access mode as 'ReadWriteOnce' and requests 1Gi of storage. This manifest is used in the context of migrating PersistentVolumes to 'ReadWriteOncePod'.

```yaml
# cat-pictures-pvc.yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: cat-pictures-pvc
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi

```

--------------------------------

### Create Kubernetes PriorityClass

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

Demonstrates how to create a Kubernetes PriorityClass with specified name, value, global default status, and description. It also shows how to control preemption policy and dry-run behavior.

```bash
kubectl create priorityclass high-priority --value=1000 --description="high priority"

```

```bash
kubectl create priorityclass default-priority --value=1000 --global-default=true --description="default priority"

```

```bash
kubectl create priorityclass high-priority --value=1000 --description="high priority" --preemption-policy="Never"

```

--------------------------------

### HPA CPU Initialization and Readiness Delay Configuration

Source: https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale

Explains the command line options for configuring CPU metrics collection during Pod startup for the Horizontal Pod Autoscaler (HPA).

```APIDOC
## HPA Configuration Options

### Description
These command line options influence how CPU metrics are collected from Pods during startup for the Horizontal Pod Autoscaler (HPA) controller.

### Method
Cluster-wide configuration via command line flags.

### Endpoint
N/A (Cluster-wide configuration)

### Parameters
#### Command Line Options
- **`--horizontal-pod-autoscaler-cpu-initialization-period`** (duration, default: 5 minutes) - Defines the time window after a Pod starts during which its CPU usage is ignored unless the Pod is in a `Ready` state and the metric sample was taken entirely during the period it was `Ready`. This helps exclude misleading high CPU usage from initializing Pods (e.g., Java apps warming up) in HPA scaling decisions.
- **`--horizontal-pod-autoscaler-initial-readiness-delay`** (duration, default: 30 seconds) - Defines a short delay period after a Pod starts during which the HPA controller treats Pods that are currently `Unready` as still initializing, even if they have previously transitioned to `Ready` briefly. This avoids including Pods that rapidly fluctuate between `Ready` and `Unready` during startup and ensures stability in the initial readiness signal before HPA considers their metrics valid.

### Request Example
```bash
kube-controller-manager --horizontal-pod-autoscaler-cpu-initialization-period=10m --horizontal-pod-autoscaler-initial-readiness-delay=1m
```

### Response
N/A (Configuration changes are applied to the controller manager.

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Delete DRA Example Job (kubectl)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

This command deletes the example DRA Job that was previously applied to the Kubernetes cluster. It uses the same URL to identify the Job to be removed.

```bash
kubectl delete -f https://k8s.io/examples/dra/dra-example-job.yaml

```

--------------------------------

### Node Labels Example

Source: https://kubernetes.io/docs/concepts/scheduling-eviction/_print

Demonstrates how nodes can be labeled to define topology domains like region and zone. It highlights the use of well-known labels versus private labels.

```yaml
region: us-east-1
zone: us-east-1a
```

--------------------------------

### Initializing Dual-Stack Control Plane Node with Kubeadm Config File

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

Command to initiate the dual-stack control plane node using kubeadm, referencing a previously defined configuration file.

```shell
kubeadm init --config=kubeadm-config.yaml
```

--------------------------------

### Kubernetes Memory Resource Units Example

Source: https://kubernetes.io/docs/concepts/configuration/_print

Demonstrates various ways to express memory resource quantities in Kubernetes, including plain integers, fixed-point numbers with suffixes (E, P, T, G, M, k), and power-of-two equivalents (Ei, Pi, Ti, Gi, Mi, Ki). It highlights the importance of case sensitivity for suffixes, as 'm' denotes millibytes while 'M' denotes megabytes.

```text
128974848, 129e6, 129M,  128974848000m, 123Mi
```

--------------------------------

### Configure Kubelet Service

Source: https://kubernetes.io/docs/tutorials/cluster-management/_print

Sets up the kubelet configuration file and creates a systemd service unit file for the kubelet. This configures the kubelet to run in standalone mode, connecting to the CRI-O runtime.

```bash
sudo mkdir -p /etc/kubernetes/manifests
sudo tee /etc/kubernetes/kubelet.yaml <<EOF
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
authentication:
  webhook:
    enabled: false # Do NOT use in production clusters!
authorization:
  mode: AlwaysAllow # Do NOT use in production clusters!
enableServer: false
logging:
  format: text
address: 127.0.0.1 # Restrict access to localhost
readOnlyPort: 10255 # Do NOT use in production clusters!
staticPodPath: /etc/kubernetes/manifests
containerRuntimeEndpoint: unix:///var/run/crio/crio.sock
EOF

chmod +x kubelet
sudo cp kubelet /usr/bin/
sudo tee /etc/systemd/system/kubelet.service <<EOF
[Unit]
Description=Kubelet

[Service]
ExecStart=/usr/bin/kubelet \
 --config=/etc/kubernetes/kubelet.yaml
Restart=always

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now kubelet.service
```

--------------------------------

### Server-Side Apply Message Body Example (JSON/YAML)

Source: https://kubernetes.io/docs/reference/using-api/_print

An example of a Server-Side Apply message body representing a 'no-change' update for a ConfigMap. This structure is sent as the body of a patch request with the `application/apply-patch+yaml` Content-Type header.

```json
{
  "apiVersion": "v1",
  "kind": "ConfigMap"
}
```

--------------------------------

### POST /apis/apps/v1/namespaces/{namespace}/replicasets

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/_print

Creates a new ReplicaSet.

```APIDOC
## POST /apis/apps/v1/namespaces/{namespace}/replicasets

### Description
Creates a ReplicaSet.

### Method
POST

### Endpoint
/apis/apps/v1/namespaces/{namespace}/replicasets

### Parameters
#### Path Parameters
- **namespace** (string) - Required - The namespace for the ReplicaSet.

#### Query Parameters
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be returned to the caller as a string.

#### Request Body
- **object** (ReplicaSet) - Required - The ReplicaSet object to create.

### Request Example
```json
{
  "apiVersion": "apps/v1",
  "kind": "ReplicaSet",
  "metadata": {
    "name": "my-new-replicaset",
    "namespace": "default"
  },
  "spec": {
    "replicas": 2,
    "selector": {
      "matchLabels": {
        "app": "my-app"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "my-app"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:latest"
          }
        ]
      }
    }
  }
}
```

### Response
#### Success Response (200 or 201)
- **ReplicaSet** (object) - The created ReplicaSet object.

#### Response Example
```json
{
  "apiVersion": "apps/v1",
  "kind": "ReplicaSet",
  "metadata": {
    "name": "my-new-replicaset",
    "namespace": "default",
    "creationTimestamp": "2023-10-27T10:00:00Z"
  },
  "spec": {
    "replicas": 2,
    "selector": {
      "matchLabels": {
        "app": "my-app"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "my-app"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:latest"
          }
        ]
      }
    }
  },
  "status": {
    "replicas": 0,
    "availableReplicas": 0,
    "readyReplicas": 0
  }
}
```
```

--------------------------------

### Install and List Processes in Pod Shell (bash)

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Updates package lists and installs the 'procps' package within a container's shell, then lists all running processes. This is useful for debugging and understanding the container's runtime environment.

```bash
apt-get update
apt-get install procps
ps aux
```

--------------------------------

### Apply Configuration from Multiple JSON Files

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

Applies configurations from all files ending with '.json' in the current directory. This uses wildcard expansion to apply multiple manifests at once.

```bash
kubectl apply -f '*.json'
```

--------------------------------

### Example: Update All Containers in a Daemonset

Source: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_set/kubectl_set_image

This example updates the image of all containers within the 'abc' daemonset to 'nginx:1.9.1'. The wildcard '*' is used to signify all containers. This is useful for updating all components of a daemonset at once. It requires the 'abc' daemonset to exist.

```bash
kubectl set image daemonset abc *=nginx:1.9.1
```

--------------------------------

### Example Pod Description Snippet (kubectl)

Source: https://kubernetes.io/docs/tasks/debug/_print

This snippet from the `kubectl describe pod` output shows the details of the ephemeral container, including its ID, image, state (Running), and readiness status. It confirms the successful injection of the debugging container.

```text
...
Ephemeral Containers:
  debugger-8xzrl:
    Container ID:   docker://b888f9adfd15bd5739fefaa39e1df4dd3c617b9902082b1cfdc29c4028ffb2eb
    Image:          busybox
    Image ID:       docker-pullable://busybox@sha256:1828edd60c5efd34b2bf5dd3282ec0cc04d47b2ff9caa0b6d4f07a21d1c08084
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 12 Feb 2020 14:25:42 +0100
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:         <none>
...

```

--------------------------------

### Describe Frontend ReplicaSet (kubectl)

Source: https://kubernetes.io/docs/concepts/workloads/_print

Provides detailed information about the frontend ReplicaSet, including its selector, labels, replica status, Pod template, and events. Useful for troubleshooting.

```bash
kubectl describe rs/frontend

```

--------------------------------

### SelfSubjectReview Response Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/authentication

This is an example of a successful response from the SelfSubjectReview API. The status field contains userInfo, detailing the username and groups the client belongs to within the cluster.

```json
{
  "apiVersion": "authentication.k8s.io/v1",
  "kind": "SelfSubjectReview",
  "status": {
    "userInfo": {
      "username": "janedoe@example.com",
      "groups": [
        "viewers",
        "editors",
        "system:authenticated"
      ]
    }
  }
}
```

--------------------------------

### Attach to a Running Container with Docker and Pod with kubectl

Source: https://kubernetes.io/docs/reference/kubectl/_print

Demonstrates how to attach to a running container using 'docker attach' and a running pod using 'kubectl attach'. Detach using Ctrl+P then Ctrl+Q.

```bash
docker ps
docker attach 55c103fa1296
...
```

```bash
kubectl get pods
kubectl attach -it nginx-app-5jyvm
...
```

--------------------------------

### Manage Kubectl Configuration and Contexts

Source: https://kubernetes.io/docs/reference/kubectl/quick-reference

Commands for viewing, setting, and managing kubectl configuration, including contexts, users, and namespaces. Supports merging multiple kubeconfig files and viewing raw configuration data. Can be used to set cluster URLs, credentials, and default namespaces.

```bash
kubectl config view # Show Merged kubeconfig settings.

# use multiple kubeconfig files at the same time and view merged config
KUBECONFIG=~/.kube/config:~/.kube/kubconfig2

kubectl config view

# Show merged kubeconfig settings and raw certificate data and exposed secrets
kubectl config view --raw 

# get the password for the e2e user
kubectl config view -o jsonpath='{.users[?(@.name == "e2e")].user.password}'

# get the certificate for the e2e user
kubectl config view --raw -o jsonpath='{.users[?(.name == "e2e")].user.client-certificate-data}' | base64 -d

kubectl config view -o jsonpath='{.users[].name}'    # display the first user
kubectl config view -o jsonpath='{.users[*].name}'   # get a list of users
kubectl config get-contexts                          # display list of contexts
kubectl config get-contexts -o name                  # get all context names
kubectl config current-context                       # display the current-context
kubectl config use-context my-cluster-name           # set the default context to my-cluster-name

kubectl config set-cluster my-cluster-name           # set a cluster entry in the kubeconfig

# configure the URL to a proxy server to use for requests made by this client in the kubeconfig
kubectl config set-cluster my-cluster-name --proxy-url=my-proxy-url

# add a new user to your kubeconf that supports basic auth
kubectl config set-credentials kubeuser/foo.kubernetes.com --username=kubeuser --password=kubepassword

# permanently save the namespace for all subsequent kubectl commands in that context.
kubectl config set-context --current --namespace=ggckad-s2

# set a context utilizing a specific username and namespace.
kubectl config set-context gce --user=cluster-admin --namespace=foo \
  && kubectl config use-context gce

kubectl config unset users.foo                       # delete user foo

# short alias to set/show context/namespace (only works for bash and bash-compatible shells, current context to be set before using kn to set namespace)
alias kx='f() { [ "$1" ] && kubectl config use-context $1 || kubectl config current-context ; } ; f'
alias kn='f() { [ "$1" ] && kubectl config set-context --current --namespace $1 || kubectl config view --minify | grep namespace | cut -d" " -f6 ; } ; f'
```

--------------------------------

### Kubernetes ConversionReview Object Example (v1beta1)

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/_print

This JSON object demonstrates a ConversionReview request for the deprecated apiextensions.k8s.io/v1beta1 API version. It mirrors the structure of the v1 example, containing a UID, the target API version, and the objects to be converted. This is relevant for older Kubernetes versions or specific conversion scenarios.

```json
{
  "apiVersion": "apiextensions.k8s.io/v1beta1",
  "kind": "ConversionReview",
  "request": {
    "uid": "705ab4f5-6393-11e8-b7cc-42010a800002",
    "desiredAPIVersion": "example.com/v1",
    "objects": [
      {
        "kind": "CronTab",
        "apiVersion": "example.com/v1beta1",
        "metadata": {
          "creationTimestamp": "2019-09-04T14:03:02Z",
          "name": "local-crontab",
          "namespace": "default",
          "resourceVersion": "143",
          "uid": "3415a7fc-162b-4300-b5da-fd6083580d66"
        },
        "hostPort": "localhost:1234"
      },
      {
        "kind": "CronTab",
        "apiVersion": "example.com/v1beta1",
        "metadata": {
          "creationTimestamp": "2019-09-03T13:02:01Z",
          "name": "remote-crontab",
          "resourceVersion": "12893",
          "uid": "359a83ec-b575-460d-b553-d859cedde8a0"
        },
        "hostPort": "example.com:2345"
      }
    ]
  }
}
```

--------------------------------

### Add Resources to kustomization.yaml

Source: https://kubernetes.io/docs/tutorials/_print

This command appends resource definitions for the MySQL and WordPress deployment YAML files to a `kustomization.yaml` file. This is a common pattern in Kubernetes for managing configurations with Kustomize, allowing for declarative management of multiple resources.

```bash
cat <<EOF >>./kustomization.yaml
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
EOF

```

--------------------------------

### Example Bearer Token Authentication Header

Source: https://kubernetes.io/docs/reference/access-authn-authz/bootstrap-tokens

An example of an Authorization header using a bootstrap token as a bearer token for API server authentication. The token format is 'token-id.token-secret'.

```http
Authorization: Bearer 07401b.f395accd246ae52d
```

--------------------------------

### GET /apis/networking.k8s.io/v1/ipaddresses

Source: https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/ip-address-v1

Lists all IPAddress resources or watches for changes.

```APIDOC
## GET /apis/networking.k8s.io/v1/ipaddresses

### Description
Lists or watches objects of kind IPAddress.

### Method
GET

### Endpoint
/apis/networking.k8s.io/v1/ipaddresses

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks
- **continue** (string) - Optional - continue
- **fieldSelector** (string) - Optional - fieldSelector
- **labelSelector** (string) - Optional - labelSelector
- **limit** (integer) - Optional - limit
- **pretty** (string) - Optional - pretty
- **resourceVersion** (string) - Optional - resourceVersion
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents
- **timeoutSeconds** (integer) - Optional - timeoutSeconds
- **watch** (boolean) - Optional - watch

### Response
#### Success Response (200)
- **IPAddressList** (object) - A list of IPAddress resources.

#### Error Response
- **401** - Unauthorized
```

--------------------------------

### Apply Kubernetes Resources

Source: https://kubernetes.io/docs/tutorials/_print

This command applies the Kubernetes configuration defined in the 'web.yaml' file. It creates the specified Service and StatefulSet resources within the cluster.

```bash
kubectl apply -f https://k8s.io/examples/application/web/web.yaml

```

--------------------------------

### Print Kubeadm Init Defaults for KubeletConfiguration

Source: https://kubernetes.io/docs/setup/production-environment/tools/_print

This command prints the default values for the KubeletConfiguration component when initializing a cluster with kubeadm. It helps in understanding the available configuration options.

```bash
kubeadm config print init-defaults --component-configs KubeletConfiguration

```

--------------------------------

### Create a Kubernetes Role with specific permissions

Source: https://kubernetes.io/docs/reference/access-authn-authz/_print

These examples show how to use the `kubectl create role` command to define granular permissions for a Role within a specific namespace. It covers creating roles with basic verbs and resources, specifying resource names, including specific API groups, and granting subresource permissions.

```bash
kubectl create role pod-reader --verb=get --verb=list --verb=watch --resource=pods

```

```bash
kubectl create role pod-reader --verb=get --resource=pods --resource-name=readablepod --resource-name=anotherpod

```

```bash
kubectl create role foo --verb=get,list,watch --resource=replicasets.apps

```

```bash
kubectl create role foo --verb=get,list,watch --resource=pods,pods/status

```

```bash
kubectl create role my-component-lease-holder --verb=get,list,watch,update --resource=lease --resource-name=my-component

```

--------------------------------

### Kubernetes ReplicaSet GET API Request

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/replica-set-v1

Demonstrates an HTTP GET request to retrieve a specific ReplicaSet from a given namespace. This operation is used to read the current state of a ReplicaSet.

```http
GET /apis/apps/v1/namespaces/{namespace}/replicasets/{name}
```

--------------------------------

### GET /apis/apps/v1/deployments

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Lists or watches all Deployments across all namespaces.

```APIDOC
## GET /apis/apps/v1/deployments

### Description
Lists or watches objects of kind Deployment across all namespaces.

### Method
GET

### Endpoint
/apis/apps/v1/deployments

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks requests watch events with a time limit.
- **continue** (string) - Optional - continue may be set to the last token returned by the server in order to resume a stalled list call.
- **fieldSelector** (string) - Optional - A selector to restrict the list of returned objects by their fields. Supported fields are: `metadata.name` and `metadata.namespace`.
- **labelSelector** (string) - Optional - A selector to restrict the list of returned objects by their labels. Supported operators are `=`, `==`, `!=`, `<>`, `<=`, `>=`. Label keys and values are case-insensitive. A label query format is `key1=value1,key2=value2`.
- **limit** (integer) - Optional - limit is the maximum number of resources to be returned.
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be returned to the caller.
- **resourceVersion** (string) - Optional - resourceVersion sets the identity of a specific version of a resource that this client is looking for.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines how resourceVersion is matched against the server's version of the resource. Possible values are `"exact"` and `"ignore"`.
- **sendInitialEvents** (boolean) - Optional - `sendInitialEvents=true` with a listิว `watch=true` option will send initial events in* a single list call to the client. After the initial list, subsequent `watch` events will be sent.
- **timeoutSeconds** (integer) - Optional - timeoutSeconds long-running requests should be cancelled after this period of time.
- **watch** (boolean) - Optional - Watch for changes to the requested objects.

### Response
#### Success Response (200)
- **DeploymentList** (object) - OK

#### Response Example
```json
{
  "apiVersion": "apps/v1",
  "kind": "DeploymentList",
  "metadata": {
    "selfLink": "/apis/apps/v1/deployments",
    "resourceVersion": "12345"
  },
  "items": [
    {
      "apiVersion": "apps/v1",
      "kind": "Deployment",
      "metadata": {
        "name": "my-deployment-global-1",
        "namespace": "kube-system"
      },
      "spec": {
        "replicas": 1
      },
      "status": {
        "availableReplicas": 1
      }
    }
  ]
}
```
```

--------------------------------

### Get StorageVersionMigration by Name (HTTP Request)

Source: https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/storage-version-migration-v1beta1

This describes the HTTP GET request to retrieve a specific StorageVersionMigration resource by its name. It includes path parameters and potential responses.

```http
GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}
```

--------------------------------

### Download Kubelet Binary (arm64)

Source: https://kubernetes.io/docs/tutorials/_print

This command downloads the latest stable version of the Kubelet binary for the arm64 architecture. It uses `curl` to fetch the binary from the official Kubernetes release repository.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubelet"

```

--------------------------------

### Start kubectl Proxy for API Access

Source: https://kubernetes.io/docs/tasks/administer-cluster/_print

Starts `kubectl` in proxy mode, acting as a reverse proxy to the API server. This method handles API server location and authentication, recommended for secure access. It enables exploration of the API using tools like `curl` or a browser.

```bash
kubectl proxy --port=8080 &

```

--------------------------------

### Get ComponentStatus (Kubernetes API)

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Read the status of a specified ComponentStatus in Kubernetes. This operation uses an HTTP GET request and requires the ComponentStatus name. The 'pretty' query parameter can be used for formatted output.

```http
GET /api/v1/componentstatuses/{name}
```

--------------------------------

### GET /apis/apps/v1/statefulsets

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/_print

Lists or watches all StatefulSets across all namespaces.

```APIDOC
## GET /apis/apps/v1/statefulsets

### Description
Lists or watches all StatefulSets across all namespaces.

### Method
GET

### Endpoint
/apis/apps/v1/statefulsets

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks requests watch events with a time limit.
- **continue** (string) - Optional - continue may be set to the last token returned by the server in order to resume a stalled list call.
- **fieldSelector** (string) - Optional - A selector to restrict the list of returned objects by their fields. Supported fields are: metadata.name, metadata.namespace, metadata.labels, spec.selector, status.phase.
- **labelSelector** (string) - Optional - A selector to restrict the list of returned objects by their labels. Supports '=', '==', and '!='.
- **limit** (integer) - Optional - limit is a maximum number of responses to return for a list call. If more items exist, the server will set the continue token to be used for retrieving the next page.
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and serialized, and should be      returned from the server with no further processing. 
- **resourceVersion** (string) - Optional - resourceVersion sets a version number for to only get objects created after that version.  Only both especified.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines how resourceVersion values are compared, i.e. Exact or NotOlderThan.
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents makes aShortlyAfter or EndList event for the watch. 
- **timeoutSeconds** (integer) - Optional - timeoutSeconds specifies the server timeout for this operation.
- **watch** (boolean) - Optional - Watch for changes to the specified resource.

### Response
#### Success Response (200)
- **StatefulSetList** (object) - OK. A list of StatefulSet objects.

#### Error Response
- **401** - Unauthorized
```

--------------------------------

### Kubernetes RawExtension for External/Internal Struct Conversion (Go)

Source: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/resource-claim-v1

Demonstrates how to use RawExtension for handling arbitrary data between internal and external API versions in Kubernetes. It shows the structure of internal and external objects and how data is serialized and deserialized.

```Go
package main

import (
	"encoding/json"
	runtime "k8s.io/apimachinery/pkg/runtime"
)

// Internal package:
type MyAPIObjectInternal struct {
	runtime.TypeMeta `json:",inline"
	MyPlugin runtime.Object `json:"myPlugin"`
}

type PluginAInternal struct {
	AOption string `json:"aOption"`
}

// External package:
type MyAPIObjectExternal struct {
	runtime.TypeMeta `json:",inline"
	MyPlugin runtime.RawExtension `json:"myPlugin"`
}

type PluginAExternal struct {
	AOption string `json:"aOption"`
}

func main() {
	// Example of serialized JSON on the wire
	jsonString := `{
		"kind":"MyAPIObject",
		"apiVersion":"v1",
		"myPlugin": {
			"kind":"PluginA",
			"aOption":"foo"
		}
	}`

	var externalObject MyAPIObjectExternal
	json.Unmarshal([]byte(jsonString), &externalObject)

	// In a real scenario, you would then copy this to an internal object
	// using pkg/conversion, which would unpack the RawExtension.

	// For demonstration, let's simulate unpacking (this is simplified)
	var pluginAData PluginAExternal
	json.Unmarshal(externalObject.MyPlugin.Raw, &pluginAData)

	internalObject := MyAPIObjectInternal{
		TypeMeta: externalObject.TypeMeta,
		MyPlugin: &PluginAInternal{
			AOption: pluginAData.AOption,
		},
	}

	// Now internalObject.MyPlugin is of type runtime.Object (specifically *PluginAInternal)
	_ = internalObject
}

```

--------------------------------

### Get CertificateSigningRequest API Request

Source: https://kubernetes.io/docs/reference/kubernetes-api/authentication-resources/certificate-signing-request-v1

Retrieves a specific CertificateSigningRequest by its name. This operation uses an HTTP GET request and requires the 'name' parameter in the path. An optional 'pretty' parameter can be used for formatted output.

```http
GET /apis/certificates.k8s.io/v1/certificatesigningrequests/{name} HTTP/1.1
Host: your-kubernetes-api-host


```

--------------------------------

### Start a Busybox pod with no restart policy using kubectl run

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

This command starts a Busybox pod in the foreground and prevents it from restarting if it exits. The '--restart=Never' option is suitable for one-off tasks or debugging.

```bash
kubectl run -i -t busybox --image=busybox --restart=Never
```

--------------------------------

### Kubectl Get: Viewing and Finding Resources

Source: https://kubernetes.io/docs/reference/kubectl/_print

Commands for retrieving and inspecting Kubernetes resources. This includes listing services, pods, deployments, and obtaining detailed information in various formats like YAML or wide output. It also covers sorting and filtering resources.

```bash
kubectl get services                          # List all services in the namespace
kubectl get pods --all-namespaces             # List all pods in all namespaces
kubectl get pods -o wide                      # List all pods in the current namespace, with more details
kubectl get deployment my-dep                 # List a particular deployment
kubectl get pods                              # List all pods in the namespace
kubectl get pod my-pod -o yaml                # Get a pod's YAML
kubectl describe nodes my-node
kubectl describe pods my-pod
kubectl get services --sort-by=.metadata.name
kubectl get pods --sort-by='.status.containerStatuses[0].restartCount'
kubectl get pv --sort-by=.spec.capacity.storage
kubectl get pods --selector=app=cassandra -o 
  jsonpath='{.items[*].metadata.labels.version}'
kubectl get configmap myconfig \
  -o jsonpath='{.data.ca\.crt}'
```

--------------------------------

### Kubelet Configuration Parameters

Source: https://kubernetes.io/docs/reference/config-api/_print

This section details various configuration parameters for the Kubelet, covering aspects like pod limits, volume management, kernel settings, feature gates, logging, and resource reservations.

```APIDOC
## Kubelet Configuration Parameters

### Description
This document details various configuration parameters for the Kubelet, covering aspects like pod limits, volume management, kernel settings, feature gates, logging, and resource reservations.

### Parameters

#### Kubelet Configuration Fields

- **podsPerCore** (`int32`) - Optional - The maximum number of pods per core. Cannot exceed maxPods. The value must be a non-negative integer. If 0, there is no limit on the number of Pods. Default: 0
- **enableControllerAttachDetach** (`bool`) - Optional - Enables the Attach/Detach controller to manage attachment/detachment of volumes scheduled to this node, and disables kubelet from executing any attach/detach operations. Note: attaching/detaching CSI volumes is not supported by the kubelet, so this option needs to be true for that use case. Default: true
- **protectKernelDefaults** (`bool`) - Optional - If true, causes the Kubelet to error if kernel flags are not as it expects. Otherwise the Kubelet will attempt to modify kernel flags to match its expectation. Default: false
- **makeIPTablesUtilChains** (`bool`) - Optional - If true, causes the Kubelet to create the KUBE-IPTABLES-HINT chain in iptables as a hint to other components about the configuration of iptables on the system. Default: true
- **iptablesMasqueradeBit** (`int32`) - Optional - Formerly controlled the creation of the KUBE-MARK-MASQ chain. Deprecated: no longer has any effect. Default: 14
- **iptablesDropBit** (`int32`) - Optional - Formerly controlled the creation of the KUBE-MARK-DROP chain. Deprecated: no longer has any effect. Default: 15
- **featureGates** (`map[string]bool`) - Optional - A map of feature names to bools that enable or disable experimental features. This field modifies piecemeal the built-in default values from "k8s.io/kubernetes/pkg/features/kube_features.go". Default: nil
- **failSwapOn** (`bool`) - Optional - Tells the Kubelet to fail to start if swap is enabled on the node. Default: true
- **memorySwap** (`MemorySwapConfiguration`) - Optional - Configures swap memory available to container workloads.
- **containerLogMaxSize** (`string`) - Optional - A quantity defining the maximum size of the container log file before it is rotated. For example: "5Mi" or "256Ki". Default: "10Mi"
- **containerLogMaxFiles** (`int32`) - Optional - Specifies the maximum number of container log files that can be present for a container. Default: 5
- **containerLogMaxWorkers** (`int32`) - Optional - Specifies the maximum number of concurrent workers to spawn for performing the log rotate operations. Set this count to 1 for disabling the concurrent log rotation workflows. Default: 1
- **containerLogMonitorInterval** (`meta/v1.Duration`) - Optional - Specifies the duration at which the container logs are monitored for performing the log rotate operation. This defaults to 10 * time.Seconds. But can be customized to a smaller value based on the log generation rate and the size required to be rotated against. Default: 10s
- **configMapAndSecretChangeDetectionStrategy** (`ResourceChangeDetectionStrategy`) - Optional - A mode in which ConfigMap and Secret managers are running. Valid values include: `Get`, `Cache`, `Watch`. Default: "Watch"
- **systemReserved** (`map[string]string`) - Optional - A set of ResourceName=ResourceQuantity (e.g. cpu=200m,memory=150G) pairs that describe resources reserved for non-kubernetes components. Currently only cpu and memory are supported. See https://kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources for more detail. Default: nil
- **kubeReserved** (`map[string]string`) - Optional - A set of ResourceName=ResourceQuantity (e.g. cpu=200m,memory=150G) pairs that describe resources reserved for kubernetes system components. Currently cpu, memory and local storage for root file system are supported. See https://kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources for more details. Default: nil
- **reservedSystemCPUs** (`string`) - Required - The reservedSystemCPUs option specifies the CPU list reserved for the host level system threads and kubernetes related threads. This provide a "static" CPU list rather than the "dynamic" list by systemReserved and kubeReserved. This option does not support systemReservedCgroup or kubeReservedCgroup.
- **showHiddenMetricsForVersion** (`string`) - Optional - The previous version for which you want to show hidden metrics. Only the previous minor version is meaningful, other values will not be allowed. The format is `<major>.<minor>`, e.g.: `1.16`. The purpose of this format is make sure you have the opportunity to notice if the next release hides additional metrics, rather than being surprised when they are permanently removed in the release after that. Default: ""
- **systemReservedCgroup** (`string`) - Optional - Specifies the cgroup for system reserved resources.

### Request Example
```json
{
  "podsPerCore": 0,
  "enableControllerAttachDetach": true,
  "protectKernelDefaults": false,
  "makeIPTablesUtilChains": true,
  "iptablesMasqueradeBit": 14,
  "iptablesDropBit": 15,
  "featureGates": {
    "ExampleFeature": true
  },
  "failSwapOn": true,
  "memorySwap": {},
  "containerLogMaxSize": "10Mi",
  "containerLogMaxFiles": 5,
  "containerLogMaxWorkers": 1,
  "containerLogMonitorInterval": "10s",
  "configMapAndSecretChangeDetectionStrategy": "Watch",
  "systemReserved": {
    "cpu": "100m",
    "memory": "100Mi"
  },
  "kubeReserved": {
    "cpu": "100m",
    "memory": "100Mi"
  },
  "reservedSystemCPUs": "0-1",
  "showHiddenMetricsForVersion": "1.27",
  "systemReservedCgroup": "/system.slice"
}
```

### Response
#### Success Response (200)
- **status** (`string`) - Indicates the success of the operation.

#### Response Example
```json
{
  "status": "success"
}
```
```

--------------------------------

### kubectl apply --server-side Migration

Source: https://kubernetes.io/docs/reference/using-api/server-side-apply

Instructions for migrating from client-side apply to server-side apply using the `kubectl apply --server-side` command.

```APIDOC
## kubectl apply --server-side

### Description
This command facilitates the transition from client-side apply to server-side apply for managing Kubernetes resources.

### Method
kubectl command

### Usage
`kubectl apply --server-side [--dry-run=server]`

### Parameters
- **--server-side** (flag) - Enables server-side apply.
- **--dry-run=server** (flag, optional) - Performs a server-side dry run without persisting changes.
- **--field-manager** (string, optional) - Specifies a custom field manager. Defaults to `kubectl`.

### Migration Notes
- By default, field management transfers to the `kubectl` server-side apply manager.
- Ensure the `last-applied-configuration` annotation is up-to-date to avoid conflicts with fields not managed by client-side apply.
- To opt-out of default field management behavior or use a different manager, specify `--field-manager=my-manager`.
```

--------------------------------

### Update Package List and Install Curl

Source: https://kubernetes.io/docs/tasks/configure-pod-container/_print

Updates the package list on a Debian-based system and installs the curl utility. This is often a prerequisite for fetching resources or testing network connectivity.

```bash
apt update
apt install curl
```

--------------------------------

### Deploy Hello World Application (Kubernetes YAML)

Source: https://kubernetes.io/docs/tutorials/_print

This YAML defines a Kubernetes Deployment for the Hello World application. It specifies the container image, name, and the number of replicas (5). The container listens on port 8080.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app.kubernetes.io/name: load-balancer-example
  name: hello-world
spec:
  replicas: 5
  selector:
    matchLabels:
      app.kubernetes.io/name: load-balancer-example
  template:
    metadata:
      labels:
        app.kubernetes.io/name: load-balancer-example
    spec:
      containers:
      - image: gcr.io/google-samples/hello-app:2.0
        name: hello-world
        ports:
        - containerPort: 8080

```

--------------------------------

### Copy Content for Localization

Source: https://kubernetes.io/docs/contribute/_print

To prepare content for translation, create a subdirectory under the language-specific directory (e.g., `content/de/`) and copy the English source files or directories. This example shows copying the 'kubernetes-basics' tutorial for German localization.

```bash
mkdir -p content/de/docs/tutorials
cp -ra content/en/docs/tutorials/kubernetes-basics/ content/de/docs/tutorials/
```

--------------------------------

### Configure Kubelet Feature Gates for Pod Resources

Source: https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/_print

Provides examples of Kubelet startup flags to enable or disable specific features related to pod resource management. This allows administrators to control the availability of features like KubeletPodResourcesGet and KubeletPodResourcesDynamicResources.

```bash
--feature-gates=KubeletPodResourcesGet=false

```

```bash
--feature-gates=KubeletPodResourcesDynamicResources=false

```

--------------------------------

### Example: Accessing Elasticsearch Cluster Health (HTTPS)

Source: https://kubernetes.io/docs/tasks/access-application-cluster/_print

This example shows how to construct an apiserver proxy URL to retrieve the cluster health information for Elasticsearch using HTTPS. It includes a 'pretty=true' parameter for formatted output.

```http
https://192.0.2.1/api/v1/namespaces/kube-system/services/elasticsearch-logging/proxy/_cluster/health?pretty=true
```

--------------------------------

### Provision Encrypted Swap Space

Source: https://kubernetes.io/docs/tutorials/_print

This script demonstrates how to create and activate an encrypted swap file on a Linux system using cryptsetup, mkswap, and swapon. It allocates 4GiB of space and formats it for secure swap usage.

```bash
# Allocate storage and restrict access
fallocate --length 4GiB /swapfile
chmod 600 /swapfile

# Create an encrypted device backed by the allocated storage
cryptsetup --type plain --cipher aes-xts-plain64 --key-size 256 -d /dev/urandom open /swapfile cryptswap

# Format the swap space
mkswap /dev/mapper/cryptswap

# Activate the swap space for paging
swapon /dev/mapper/cryptswap

```

--------------------------------

### Add Kubernetes YUM Repository and Install Packages (RHEL/CentOS/Fedora)

Source: https://kubernetes.io/docs/setup/production-environment/_print

This snippet adds the Kubernetes YUM repository configuration to the system. It uses a `cat <<EOF` block to define the repository details, including an `exclude` parameter to prevent automatic upgrades of Kubernetes packages. It then installs kubelet, kubeadm, and kubectl, disabling the excludes for these packages.

```bash
# This overwrites any existing configuration in /etc/yum.repos.d/kubernetes.repo
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.35/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF

# Install kubelet, kubeadm and kubectl:
# For systems with DNF:
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

# For systems with DNF5:
sudo yum install -y kubelet kubeadm kubectl --setopt=disable_excludes=kubernetes

# (Optional) Enable the kubelet service before running kubeadm:
sudo systemctl enable --now kubelet
```

--------------------------------

### Example: Accessing Elasticsearch Service Endpoint (HTTP)

Source: https://kubernetes.io/docs/tasks/access-application-cluster/_print

This example demonstrates how to construct an apiserver proxy URL to access a specific endpoint of the Elasticsearch service, including query parameters. It uses HTTP to connect to the service.

```http
http://192.0.2.1/api/v1/namespaces/kube-system/services/elasticsearch-logging/proxy/_search?q=user:kimchy
```

--------------------------------

### Kubernetes Protobuf: List Pods

Source: https://kubernetes.io/docs/reference/using-api/_print

Demonstrates how to request a list of pods from the Kubernetes API in Protobuf format. This involves setting the 'Accept' header to 'application/vnd.kubernetes.protobuf'. The response will be a binary encoded collection of Pods.

```http
GET /api/v1/pods
Accept: application/vnd.kubernetes.protobuf
```

```http
200 OK
Content-Type: application/vnd.kubernetes.protobuf

… binary encoded collection of Pods (PodList object)
```

--------------------------------

### Example ZooKeeper Log Output

Source: https://kubernetes.io/docs/tutorials/stateful-application/zookeeper

This is an example of ZooKeeper log output when configured to log to the console. It shows timestamp, log level, thread information, and the log message, including processing of commands and client connections.

```log
2016-12-06 19:34:16,236 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52740
2016-12-06 19:34:16,237 [myid:1] - INFO  [Thread-1136:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52740 (no session established for client)
2016-12-06 19:34:26,155 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxnFactory@192] - Accepted socket connection from /127.0.0.1:52749
2016-12-06 19:34:26,155 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52749
2016-12-06 19:34:26,156 [myid:1] - INFO  [Thread-1137:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52749 (no session established for client)
2016-12-06 19:34:26,222 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxnFactory@192] - Accepted socket connection from /127.0.0.1:52750
2016-12-06 19:34:26,222 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52750
2016-12-06 19:34:26,226 [myid:1] - INFO  [Thread-1138:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52750 (no session established for client)
2016-12-06 19:34:36,151 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxnFactory@192] - Accepted socket connection from /127.0.0.1:52760
2016-12-06 19:34:36,152 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52760
2016-12-06 19:34:36,152 [myid:1] - INFO  [Thread-1139:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52760 (no session established for client)
2016-12-06 19:34:36,230 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxnFactory@192] - Accepted socket connection from /127.0.0.1:52761
2016-12-06 19:34:36,231 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52761
2016-12-06 19:34:36,231 [myid:1] - INFO  [Thread-1140:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52761 (no session established for client)
2016-12-06 19:34:46,149 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxnFactory@192] - Accepted socket connection from /127.0.0.1:52767
2016-12-06 19:34:46,149 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52767
2016-12-06 19:34:46,149 [myid:1] - INFO  [Thread-1141:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52767 (no session established for client)
2016-12-06 19:34:46,230 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxnFactory@192] - Accepted socket connection from /127.0.0.1:52768
2016-12-06 19:34:46,230 [myid:1] - INFO  [NIOServerCxn.Factory:0.0.0.0/0.0.0.0:2181:NIOServerCnxn@827] - Processing ruok command from /127.0.0.1:52768
2016-12-06 19:34:46,230 [myid:1] - INFO  [Thread-1142:NIOServerCnxn@1008] - Closed socket connection for client /127.0.0.1:52768 (no session established for client)
```

--------------------------------

### Describe Deployment (kubectl)

Source: https://kubernetes.io/docs/tutorials/_print

Provides detailed information about a specific Deployment, including its status, events, and replica set details. This command is useful for troubleshooting and understanding the effects of scaling operations.

```bash
kubectl describe deployments/kubernetes-bootcamp

```

--------------------------------

### Updated ConfigMap Example (YAML)

Source: https://kubernetes.io/docs/tutorials/configuration/updating-configuration-via-a-configmap

This is an example of how the 'color' ConfigMap might look after editing its data. The 'color' key has been changed from 'blue' to 'green', which will be picked up by the sidecar container.

```yaml
apiVersion: v1
data:
  color: green
kind: ConfigMap
# You can leave the existing metadata as they are.
# The values you'll see won't exactly match these.
metadata:
  creationTimestamp: "2024-02-17T12:20:30Z"
  name: color
  namespace: default
  resourceVersion: "1054"
  uid: e40bb34c-58df-4280-8bea-6ed16edccfaa

```

--------------------------------

### Register APIService Object Example

Source: https://kubernetes.io/docs/tasks/extend-kubernetes/configure-aggregation-layer

An example Kubernetes APIService object definition used to dynamically configure which client requests are proxied to extension apiservers. It specifies API group, version, priority, and service details.

```yaml
apiVersion: apiregistration.k8s.io/v1
kind: APIService
metadata:
  name: <name of the registration object>
spec:
  group: <API group name this extension apiserver hosts>
  version: <API version this extension apiserver hosts>
  groupPriorityMinimum: <priority this APIService for this group, see API documentation>
  versionPriority: <prioritizes ordering of this version within a group, see API documentation>
  service:
    namespace: <namespace of the extension apiserver service>
    name: <name of the extension apiserver service>
  caBundle: <pem encoded ca cert that signs the server cert used by the webhook>
```

--------------------------------

### Create Tables with HTML

Source: https://kubernetes.io/docs/test

Provides an example of creating tables using HTML, which is recommended for complex or wide tables that cannot be effectively represented using Markdown. This includes the use of `<thead>`, `<tbody>`, `<tr>`, and `<th>`/`<td>` tags.

```html
<table>
<thead>
  <tr>
    <th>Heading cell 1</th>
    <th>Heading cell 2</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Body cell 1</td>
    <td>Body cell 2</td>
  </tr>
</tbody>
</table>

```

--------------------------------

### Client-side List Kind (kubectl example)

Source: https://kubernetes.io/docs/reference/using-api/_print

Demonstrates the client-side 'List' kind used by tools like kubectl to represent collections that may contain items of different kinds. This is an internal implementation detail and should not be relied upon in automation.

```APIDOC
## Client-side List Kind (kubectl example)

### Description
This section illustrates the `kind: List` structure, which is a client-side representation used by tools like `kubectl` to aggregate results from potentially multiple API list operations. It's important to note that the Kubernetes API itself does not define a `kind: List`.

### Method
N/A (Client-side representation)

### Endpoint
N/A (Client-side representation)

### Parameters
N/A

### Request Example
```bash
kubectl get services -A -o yaml
```

### Response
#### Success Response (Client-side)
- **kind** (string) - Always "List" for this client-side representation.
- **apiVersion** (string) - The API version (e.g., "v1").
- **metadata** (object) - Contains metadata like resourceVersion and selfLink (often empty for client-side lists).
- **items** (array) - An array containing objects of potentially different kinds (e.g., Service objects).

#### Response Example
```json
apiVersion: v1
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
items:
- apiVersion: v1
  kind: Service
  metadata:
    creationTimestamp: "2021-06-03T14:54:12Z"
    labels:
      component: apiserver
      provider: kubernetes
    name: kubernetes
    namespace: default
...
- apiVersion: v1
  kind: Service
  metadata:
    annotations:
      prometheus.io/port: "9153"
      prometheus.io/scrape: "true"
    creationTimestamp: "2021-06-03T14:54:14Z"
    labels:
      k8s-app: kube-dns
      kubernetes.io/cluster-service: "true"
      kubernetes.io/name: CoreDNS
    name: kube-dns
    namespace: kube-system
...
```

#### Note:
`kind: List` is a client-side, internal implementation detail for processing collections that might be of different kinds of object. Avoid depending on `kind: List` in automation or other code.
```

--------------------------------

### JSONPatch Add Object Example (CEL)

Source: https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/_print

Shows how to use CEL to construct a JSON patch that adds an object to the resource. This example adds a 'matchLabels' object to the 'spec.selector' field.

```cel
[
  JSONPatch{
    op: "add",
    path: "/spec/selector",
    value: Object.spec.selector{matchLabels: {"environment": "test"}}
  }
]

```

--------------------------------

### Retrieve snapshot logs from a Kubernetes pod

Source: https://kubernetes.io/docs/reference/generated/kubectl/kubectl

Demonstrates how to get a snapshot of logs from a pod. Covers single-container pods, multi-container pods, and pods selected by labels.

```bash
kubectl logs nginx

```

```bash
kubectl logs nginx --all-containers=true

```

```bash
kubectl logs -l app=nginx --all-containers=true

```

```bash
kubectl logs job/hello

```

```bash
kubectl logs deployment/nginx -c nginx-1

```

--------------------------------

### Start kubectl proxy

Source: https://kubernetes.io/docs/tasks/administer-cluster/kubelet-config-file

Initiates a proxy server to access Kubernetes API endpoints. This command needs to be run in a terminal and provides an output indicating the address and port it's serving on.

```bash
kubectl proxy
```

--------------------------------

### Kubernetes Label Selector Example for Namespace Inclusion

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Illustrates using `namespaceSelector` to target specific namespaces for admission policy application. This example selects namespaces associated with the 'environment' label having values 'prod' or 'staging'.

```yaml
namespaceSelector:
  matchExpressions:
    - key: environment
      operator: In
      values:
        - "prod"
        - "staging"
```

--------------------------------

### Example Audit Annotation for Validation Failure

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

This example demonstrates the format of the audit annotation used to report validation failures. It includes details about the message, policy, binding, expression index, and validation actions taken.

```json
"validation.policy.admission.k8s.io/validation_failure": "[{\"message\": \"Invalid value\", {\"policy\": \"policy.example.com\", {\"binding\": \"policybinding.example.com\", {\"expressionIndex\": \"1\", {\"validationActions\": [\"Audit\"]}}]"
```

--------------------------------

### Dual-Stack Cluster Configuration with Kubeadm (YAML)

Source: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/_print

Example kubeadm configuration file (`kubeadm-config.yaml`) for initializing a dual-stack control plane node. It defines networking CIDRs and Kubelet extra arguments for dual-stack node IP assignment.

```yaml
---
apiVersion: kubeadm.k8s.io/v1beta4
kind: ClusterConfiguration
networking:
  podSubnet: 10.244.0.0/16,2001:db8:42:0::/56
  serviceSubnet: 10.96.0.0/16,2001:db8:42:1::/112
---
apiVersion: kubeadm.k8s.io/v1beta4
kind: InitConfiguration
localAPIEndpoint:
  advertiseAddress: "10.100.0.1"
  bindPort: 6443
nodeRegistration:
  kubeletExtraArgs:
  - name: "node-ip"
    value: "10.100.0.2,fd00:1:2:3::2"
```

--------------------------------

### Eviction via curl

Source: https://kubernetes.io/docs/concepts/scheduling-eviction/_print

Example of how to initiate a pod eviction using curl, sending an Eviction object in JSON format.

```APIDOC
## Eviction via curl

### Description
Example of how to initiate a pod eviction using curl, sending an Eviction object in JSON format.

### Method
POST

### Endpoint
`https://your-cluster-api-endpoint.example/api/v1/namespaces/{namespace}/pods/{name}/eviction`

### Parameters
#### Path Parameters
- **namespace** (string) - Required - The namespace of the pod.
- **name** (string) - Required - The name of the pod to evict.

#### Query Parameters
None

#### Request Body
Requires a JSON file (e.g., `eviction.json`) containing the Eviction object, similar to the examples provided for the API calls.

### Request Example
```bash
curl -v -H 'Content-type: application/json' https://your-cluster-api-endpoint.example/api/v1/namespaces/default/pods/quux/eviction -d @eviction.json
```

### Response
#### Success Response (200 OK)
- **Eviction** (object) - Indicates the eviction was allowed and the `Eviction` subresource was created, leading to pod termination.

#### Response Example
(A successful eviction typically returns a 200 OK status code with no specific JSON body, similar to a DELETE operation. The actual pod termination process is asynchronous.)

#### Error Responses
- **429 Too Many Requests**: The eviction is not currently allowed due to PodDisruptionBudget or API rate limiting.
- **500 Internal Server Error**: The eviction is not allowed due to a misconfiguration.
```

--------------------------------

### kubectl command to list all Services as a List kind

Source: https://kubernetes.io/docs/reference/using-api/api-concepts

Shows how to use kubectl to get all services across all namespaces, outputting them as a single List object. This 'List' kind is a client-side representation and not directly available in the Kubernetes API.

```bash
kubectl get services -A -o yaml

```

```yaml
apiVersion: v1
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
items:
- apiVersion: v1
  kind: Service
  metadata:
    creationTimestamp: "2021-06-03T14:54:12Z"
    labels:
      component: apiserver
      provider: kubernetes
    name: kubernetes
    namespace: default
...
- apiVersion: v1
  kind: Service
  metadata:
    annotations:
      prometheus.io/port: "9153"
      prometheus.io/scrape: "true"
    creationTimestamp: "2021-06-03T14:54:14Z"
    labels:
      k8s-app: kube-dns
      kubernetes.io/cluster-service: "true"
      kubernetes.io/name: CoreDNS
    name: kube-dns
    namespace: kube-system


```

--------------------------------

### Kubernetes Deployment for Stateless Service with Labels

Source: https://kubernetes.io/docs/concepts/overview/_print

Illustrates a Kubernetes Deployment resource for a stateless service, showcasing the use of `app.kubernetes.io/name` and `app.kubernetes.io/instance` labels. These labels are crucial for identifying the application and its specific instance.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app.kubernetes.io/name: myservice
    app.kubernetes.io/instance: myservice-abcxyz
...

```

--------------------------------

### API-based Signer: Certificate Structure Example

Source: https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests

This snippet shows an example of a PEM-encoded certificate that can be used with API-based signers. The certificate must be BER-encoded ASN.1, and all PEM blocks must have the "CERTIFICATE" label.

```text
-----BEGIN CERTIFICATE-----
MIIDgjCCAmqgAwIBAgIUC1N1EJ4Qnsd322BhDPRwmg3b/oAwDQYJKoZIhvcNAQEL
BQAwXDELMAkGA1UEBhMCeHgxCjAIBgNVBAgMAXgxCjAIBgNVBAcMAXgxCjAIBgNV
BAoMAXgxCjAIBgNVBAsMAXgxCzAJBgNVBAMMAmNhMRAwDgYJKoZIhvcNAQkBFgF4
MB4XDTIwMDcwNjIyMDcwMFoXDTI1MDcwNTIyMDcwMFowNzEVMBMGA1UEChMMc3lz
dGVtOm5vZGVzMR4wHAYDVQQDExVzeXN0ZW06bm9kZToxMjcuMC4wLjEwggEiMA0G
CSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDne5X2eQ1JcLZkKvhzCR4Hxl9+ZmU3
+e1zfOywLdoQxrPi+o4hVsUH3q0y52BMa7u1yehHDRSaq9u62cmi5ekgXhXHzGmm
kmW5n0itRECv3SFsSm2DSghRKf0mm6iTYHWDHzUXKdm9lPPWoSOxoR5oqOsm3JEh
Q7Et13wrvTJqBMJo1GTwQuF+HYOku0NF/DLqbZIcpI08yQKyrBgYz2uO51/oNp8a
sTCsV4OUfyHhx2BBLUo4g4SptHFySTBwlpRWBnSjZPOhmN74JcpTLB4J5f4iEeA7
2QytZfADckG4wVkhH3C2EJUmRtFIBVirwDn39GXkSGlnvnMgF3uLZ6zNAgMBAAGj
YTBfMA4GA1UdDwEB/wQEAwIFoDATBgNVHSUEDDAKBggrBgEFBQcDAjAMBgNVHRMB
Af8EAjAAMB0GA1UdDgQWBBTREl2hW54lkQBDeVCcd2f2VSlB1DALBgNVHREEBDAC
ggAwDQYJKoZIhvcNAQELBQADggEBABpZjuIKTq8pCaX8dMEGPWtAykgLsTcD2jYr
L0/TCrqmuaaliUa42jQTt2OVsVP/L8ofFunj/KjpQU0bvKJPLMRKtmxbhXuQCQi1
qCRkp8o93mHvEz3mTUN+D1cfQ2fpsBENLnpS0F4G/JyY2Vrh19/X8+mImMEK5eOy
o0BMby7byUj98WmcUvNCiXbC6F45QTmkwEhMqWns0JZQY+/XeDhEcg+lJvz9Eyo2
aGgPsye1o3DpyXnyfJWAWMhOz7cikS5X2adesbgI86PhEHBXPIJ1v13ZdfCExmdd
M1fLPhLyR54fGaY+7/X8P9AZzPefAkwizeXwe9ii6/a08vWoiE4=
-----END CERTIFICATE-----
```

--------------------------------

### Create Kubernetes Namespace

Source: https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin

Creates a new Kubernetes namespace named 'examplens'. This is a prerequisite for some of the following examples.

```bash
kubectl create namespace examplens

```

--------------------------------

### GET /apis/apps/v1/daemonsets

Source: https://kubernetes.io/docs/reference/kubernetes-api/_print

Lists or watches all DaemonSets across all namespaces.

```APIDOC
## GET /apis/apps/v1/daemonsets

### Description
Lists or watches all DaemonSets across all namespaces.

### Method
GET

### Endpoint
/apis/apps/v1/daemonsets

### Parameters
#### Query Parameters
- **allowWatchBookmarks** (boolean) - Optional - allowWatchBookmarks requests watch events with a stream of metadata, containing only the object name and uid.
- **continue** (string) - Optional - continue may be set to the last token returned by the server in order to request the next page of results.
- **fieldSelector** (string) - Optional - A selector to restrict the list of returned objects by their fields. Supported fields are:
  - `.metadata.name`
- **labelSelector** (string) - Optional - A selector to restrict the list of returned objects by their labels.
- **limit** (integer) - Optional - limit is the maximum number of results to return.
- **pretty** (string) - Optional - If 'true', then the output is pretty printed and contains the status of the resource.
- **resourceVersion** (string) - Optional - resourceVersion sets the identity of a resource instance that the server must return or the server will fail to return any updated objects.
- **resourceVersionMatch** (string) - Optional - resourceVersionMatch determines how resourceVersion is matched against the server's version of the object.
- **sendInitialEvents** (boolean) - Optional - sendInitialEvents if true, then the API server will send events for all matching objects at the time the watch is opened.
- **timeoutSeconds** (integer) - Optional - timeoutSeconds long-running requests should be provided with a timeout.
- **watch** (boolean) - Optional - Watch for changes to the specified resource.

### Response
#### Success Response (200)
- **DaemonSetList** (object) - A list of DaemonSet objects across all namespaces.

#### Response Example
{
  "apiVersion": "apps/v1",
  "kind": "DaemonSetList",
  "metadata": {
    "selfLink": "/apis/apps/v1/daemonsets",
    "resourceVersion": "12345"
  },
  "items": [
    {
      "apiVersion": "apps/v1",
      "kind": "DaemonSet",
      "metadata": {
        "name": "example-daemonset-kube-system",
        "namespace": "kube-system"
      },
      "spec": {
        "selector": {
          "matchLabels": {
            "app": "my-app-kube-system"
          }
        },
        "template": {
          "metadata": {
            "labels": {
              "app": "my-app-kube-system"
            }
          },
          "spec": {
            "containers": [
              {
                "name": "kube-proxy",
                "image": "k8s.gcr.io/kube-proxy:v1.20.0"
              }
            ]
          }
        }
      }
    }
  ]
}
```