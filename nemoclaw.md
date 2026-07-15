### Start OpenShell TUI

Source: https://docs.nvidia.com/nemoclaw/latest/network-policy/approve-network-requests.html

Commands to launch the OpenShell terminal interface for monitoring sandbox activity. Use the standard command for local instances or specify an instance name for remote sandboxes.

```bash
openshell term
nemoclaw term my-gpu-box
```

--------------------------------

### Execute Network Policy Walkthrough

Source: https://docs.nvidia.com/nemoclaw/latest/network-policy/approve-network-requests.html

Runs a script to demonstrate the network request approval flow. This requires tmux and a valid NVIDIA_API_KEY environment variable.

```bash
./scripts/walkthrough.sh
```

--------------------------------

### Switch Inference Provider via OpenShell CLI

Source: https://docs.nvidia.com/nemoclaw/latest/inference/switch-inference-providers.html

Commands to update the active inference provider and model. These commands require a running NemoClaw sandbox and appropriate environment variables or network configurations depending on the provider.

```bash
# Switch to NVIDIA Cloud
openshell inference set --provider nvidia-nim --model nvidia/nemotron-3-super-120b-a12b

# Switch to Local vLLM
openshell inference set --provider vllm-local --model nvidia/nemotron-3-nano-30b-a3b

# Switch to Local NIM
openshell inference set --provider nim-local --model nvidia/nemotron-3-super-120b-a12b
```

--------------------------------

### Test NemoClaw Inference Request

Source: https://docs.nvidia.com/nemoclaw/latest/monitoring/monitor-sandbox-activity.html

Run a test inference request to verify the responsiveness of the inference provider. This involves connecting to an assistant and sending a test message. If the request fails, check sandbox status, logs, and endpoint reachability.

```bash
$ nemoclaw my-assistant connect
$ openclaw agent --agent main --local -m "Test inference" --session-id debug
```

--------------------------------

### Monitor Network Activity in OpenShell TUI

Source: https://docs.nvidia.com/nemoclaw/latest/monitoring/monitor-sandbox-activity.html

Open the OpenShell terminal UI to view live sandbox network activity, including active connections and blocked egress requests awaiting approval. For remote sandboxes, specify the instance name.

```bash
$ openshell term
```

```bash
$ nemoclaw term <instance-name>
```

--------------------------------

### View NemoClaw Blueprint and Sandbox Logs

Source: https://docs.nvidia.com/nemoclaw/latest/monitoring/monitor-sandbox-activity.html

Stream or display log output from the NemoClaw blueprint runner and sandbox. Options include following logs in real-time, displaying a specific number of lines, or viewing logs for a particular blueprint run.

```bash
$ openclaw nemoclaw logs
```

```bash
$ openclaw nemoclaw logs -f
```

```bash
$ openclaw nemoclaw logs -n 100
```

```bash
$ openclaw nemoclaw logs --run-id <id>
```

--------------------------------

### Verify Inference Status

Source: https://docs.nvidia.com/nemoclaw/latest/inference/switch-inference-providers.html

Commands to check the currently active inference provider and model configuration. Supports standard output or machine-readable JSON format.

```bash
# View status in human-readable format
openclaw nemoclaw status

# View status in machine-readable JSON format
openclaw nemoclaw status --json
```

--------------------------------

### Check NemoClaw Sandbox Health

Source: https://docs.nvidia.com/nemoclaw/latest/monitoring/monitor-sandbox-activity.html

View the current state of the NemoClaw sandbox, including blueprint run information and active inference configuration. The `--json` flag provides machine-readable output.

```bash
$ openclaw nemoclaw status
```

```bash
$ openclaw nemoclaw status --json
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.