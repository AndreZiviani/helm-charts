# node-scaler

Creates a dummy deployment with strict pod anti affinity allowing to force minimum node group size

## Chart Repo

Add the following repo to use the chart:

```console
helm repo add andreziviani https://andreziviani.github.io/node-scaler
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| annotations | object | `{}` |  |
| args[0] | string | `"infinity"` |  |
| command[0] | string | `"sleep"` |  |
| containerSecurityContext.privileged | bool | `false` |  |
| containerSecurityContext.runAsUser | int | `1000` |  |
| fullnameOverride | string | `nil` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.registry | string | `"docker.io"` |  |
| image.repository | string | `"alpine"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `nil` |  |
| nodeSelector | string | `"selector: label\n"` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| priorityClassName | string | `"system-node-critical"` |  |
| resources.requests.cpu | string | `"1m"` |  |
| resources.requests.memory | string | `"10Mi"` |  |
| tolerations | string | `"- effect: NoSchedule\n  operator: Exists\n"` |  |
| topologySpreadConstraints | string | `"- maxSkew: 1\n  topologyKey: kubernetes.io/hostname\n  whenUnsatisfiable: DoNotSchedule\n  labelSelector:\n    matchLabels:\n      app.kubernetes.io/name: {{ include \"node-scaler.name\" . }}\n"` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
