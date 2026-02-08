# resource-scaler

Creates low-priority placeholder pods that reserve cluster resources, acting as a buffer to prevent node flapping caused by autoscaler scale-up/scale-down cycles

## How it works

This chart deploys low-priority placeholder pods that reserve cluster resources (CPU/memory).
When a real workload needs to scale up:

1. The Kubernetes scheduler sees there aren't enough resources on existing nodes
2. Instead of waiting for a new node to be provisioned, it **evicts** the low-priority buffer pod
3. The real workload is immediately scheduled on the freed-up resources
4. The evicted buffer pod becomes Pending, which may trigger the cluster autoscaler to add a new node in the background

This eliminates the delay of waiting for a new node to spin up (which can take minutes on AWS) and reduces instance flapping from rapid scale-up/scale-down cycles.

## Chart Repo

Add the following repo to use the chart:

```console
helm repo add andreziviani https://andreziviani.github.io/helm-charts
```

## Quick Start

```console
helm install resource-buffer andreziviani/resource-scaler \
  --set replicas=2 \
  --set resources.requests.cpu=1 \
  --set resources.requests.memory=1Gi \
  --set nodeSelector=""
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | string | `""` | Pod affinity rules (template string) |
| annotations | object | `{}` | Deployment annotations |
| args | list | `[]` | Container args (not needed for pause image) |
| command | list | `[]` | Container command (not needed for pause image) |
| containerSecurityContext.privileged | bool | `false` |  |
| containerSecurityContext.runAsNonRoot | bool | `true` |  |
| containerSecurityContext.runAsUser | int | `65534` |  |
| fullnameOverride | string | `nil` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.registry | string | `"registry.k8s.io"` |  |
| image.repository | string | `"pause"` |  |
| image.tag | string | `"3.9"` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `nil` |  |
| nodeSelector | string | `"selector: label\n"` | Node selector (template string) |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| priorityClass.create | bool | `true` | Create PriorityClass resource |
| priorityClass.description | string | `"Low-priority class for resource buffer placeholder pods..."` |  |
| priorityClass.globalDefault | bool | `false` | Whether this is the global default PriorityClass |
| priorityClass.name | string | `""` | Name override for the PriorityClass |
| priorityClass.preemptionPolicy | string | `"Never"` | Prevents buffer pods from preempting real workloads |
| priorityClass.value | int | `-1` | Priority value (lower = evicted first, default for real pods is 0) |
| replicas | int | `1` | Number of buffer pods |
| resources.requests.cpu | string | `"1"` | CPU buffer per pod |
| resources.requests.memory | string | `"1Gi"` | Memory buffer per pod |
| tolerations | string | `"- effect: NoSchedule\n  operator: Exists\n"` | Tolerations (template string) |
| topologySpreadConstraints | string | `""` | Topology spread constraints (template string) |
| updateStrategy.type | string | `"RollingUpdate"` |  |
