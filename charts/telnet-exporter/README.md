# telnet-exporter

Exposes metrics from remote hosts for Prometheus via Telnet

## Chart Repo

Add the following repo to use the chart:

```console
helm repo add andreziviani https://andreziviani.github.io/helm-charts
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| annotations | object | `{}` |  |
| args | list | `[]` |  |
| containerSecurityContext.privileged | bool | `false` |  |
| containerSecurityContext.runAsUser | int | `1000` |  |
| fullnameOverride | string | `nil` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.registry | string | `"docker.io"` |  |
| image.repository | string | `"andreziviani/telnet-exporter"` |  |
| image.tag | string | `nil` | Overrides the image tag whose default is the chart's appVersion |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `nil` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podPortName | string | `"http-metrics"` |  |
| podSecurityContext | object | `{}` |  |
| resources.requests.cpu | string | `"50m"` |  |
| resources.requests.memory | string | `"128Mi"` |  |
| service.annotations | object | `{}` |  |
| service.enabled | bool | `true` |  |
| service.labels | object | `{}` |  |
| service.port | int | `80` |  |
| service.portName | string | `"http-metrics"` |  |
| service.targetPort | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.labels | object | `{}` |  |
| serviceAccount.name | string | `nil` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `"30s"` |  |
| serviceMonitor.labels | object | `{}` |  |
| serviceMonitor.path | string | `"/metrics"` |  |
| serviceMonitor.relabelings | list | `[]` |  |
| serviceMonitor.scheme | string | `"http"` |  |
| serviceMonitor.scrapeTimeout | string | `"30s"` |  |
| serviceMonitor.tlsConfig | object | `{}` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
