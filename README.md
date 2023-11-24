# buildkite-agent-with-agent-hooks-demo

## About

Demonstration of creating a Buildkite Agent Container image and including Agent Hooks for use on Kubernetes.

## Example

Manually running a Pod with the pre-built container image from this repository with agent plugins. Recommended approached for Buildkite Agent Token is to use Secrets.

```bash
kubectl run k8s-agent-with-hooks -i --tty --image ghcr.io/tomowatt/buildkite-agent-with-agent-hooks-demo:main -- start --token "{AGENT TOKEN}" --tags "queue=k8s-agent-with-hooks"
```

Then using a Pipeline configuration like below to show Agent Plugins being used.

```yaml
steps:
  - label: ":tada:"
    command: echo "hello from k8s agent"
    agents:
      queue: "k8s-agent-with-hooks"
```

To clean up.

```bash
kubectl delete pod k8s-agent-with-hooks
```
