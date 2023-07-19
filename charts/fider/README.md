# fider

![Version: 0.0.3](https://img.shields.io/badge/Version-0.0.3-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.21.1](https://img.shields.io/badge/AppVersion-0.21.1-informational?style=flat-square)

An open platform to collect and prioritize feedback

## Installation

### Add Helm repository

```bash
helm repo add fider https://getfider.github.io/helm
helm repo update
```

## Configuration

The following table lists the configurable parameters of the chart and the default values.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Defines rules for pod scheduling based on node or pod properties, allowing for affinity (preferred) or anti-affinity (avoidance) relationships between pods and nodes |
| autoscaling | object | `{"enabled":false,"maxReplicas":100,"minReplicas":1,"targetCPUUtilizationPercentage":80}` | Automatically adjusts the number of replicas of a deployment or a replica set based on predefined metrics or custom rules to handle varying workload demands |
| autoscaling.enabled | bool | `false` | Create a HPA for the server deployment |
| dbchecker.enabled | bool | `true` | Enable an init container that validates the database connection |
| dbchecker.image.pullPolicy | string | `"IfNotPresent"` | Image pull policy for the dbchecker image |
| dbchecker.image.repository | string | `"docker.io/atkrad/wait4x"` | Container image used to check Database readiness at startup |
| dbchecker.image.tag | string | `"2.13.0"` | Image tag for the dbchecker image |
| dbchecker.resources | object | `{"limits":{"cpu":"20m","memory":"32Mi"},"requests":{"cpu":"20m","memory":"32Mi"}}` | Resource requests and limits for the dbchecker container |
| dbchecker.securityContext | object | `{"allowPrivilegeEscalation":false,"readOnlyRootFilesystem":true,"runAsGroup":65534,"runAsNonRoot":true,"runAsUser":65534}` | SecurityContext for the dbchecker container |
| fider.env[0] | object | `{"name":"BASE_URL","value":"https://feedback.yourdomain.com"}` | Public Host Name |
| fider.env[1].name | string | `"EMAIL_NOREPLY"` |  |
| fider.env[1].value | string | `"noreply@yourdomain.com"` |  |
| fider.env[2].name | string | `"EMAIL_SMTP_HOST"` |  |
| fider.env[2].value | string | `"smtp.yourdomain.com"` |  |
| fider.env[3].name | string | `"EMAIL_SMTP_PORT"` |  |
| fider.env[3].value | int | `587` |  |
| fider.legalPages | object | `{"enabled":false,"privacy":"bar","terms":"foo"}` | https://fider.io/docs/how-to-show-legal-pages |
| fider.legalPages.enabled | bool | `false` | Enables legal pages |
| fider.legalPages.privacy | string | `"bar"` | Write your own Privacy Policy in Markdown here |
| fider.legalPages.terms | string | `"foo"` | Write your own Terms of Service in Markdown here |
| fider.secretEnv | object | `{"DATABASE_URL":"postgres://fider:s0m3g00dp4ssw0rd@postgresql-service:5432/fider?sslmode=disable","JWT_SECRET":"VERY_STRONG_SECRET_SHOULD_BE_USED_HERE"}` | These environment variables are stored in a Kubernetes secret |
| fider.secretEnv.DATABASE_URL | string | `"postgres://fider:s0m3g00dp4ssw0rd@postgresql-service:5432/fider?sslmode=disable"` | Connection string to the PostgreSQL database |
| fider.secretEnv.JWT_SECRET | string | `"VERY_STRONG_SECRET_SHOULD_BE_USED_HERE"` | Use a 512-bit secret here |
| fullnameOverride | string | `nil` | Override the fully qualified app name |
| image.pullPolicy | string | `"IfNotPresent"` | "IfNotPresent" to pull the image if no image with the specified tag exists on the node, "Always" to always pull the image or "Never" to try and use pre-pulled images |
| image.repository | string | `"getfider/fider"` | Repository to pull fider image from |
| imagePullSecrets | list | `[]` | Names of the Kubernetes secrets for imagePullSecrets |
| ingress.annotations | object | `{}` | Ingress annotations |
| ingress.className | string | `""` | The name of the Ingress Class associated with the ingress |
| ingress.enabled | bool | `false` | If `true`, an Ingress is created |
| ingress.hosts | list | `[{"host":"fider.local","paths":[{"path":"/","pathType":"prefix"}]}]` | Domain name Kubernetes Ingress rule looks for. Set it to the domain Fider will be hosted on |
| ingress.hosts[0] | object | `{"host":"fider.local","paths":[{"path":"/","pathType":"prefix"}]}` | List of domain names Kubernetes Ingress rule looks for. Set it to the domains in which Fider will be hosted on |
| ingress.hosts[0].paths | list | `[{"path":"/","pathType":"prefix"}]` | List of paths to use in Kubernetes Ingress rules |
| ingress.hosts[0].paths[0] | object | `{"path":"/","pathType":"prefix"}` | Path to use in the Ingress |
| ingress.hosts[0].paths[0].pathType | string | `"prefix"` | Ingress path type |
| ingress.tls | list | `[]` | Ingress TLS settings |
| kubeVersionOverride | string | `nil` | Override the version of Kubernetes being used in a cluster |
| nameOverride | string | `nil` | Override the name of the chart |
| nodeSelector | object | `{}` | Selects the nodes where a pod can be scheduled based on node labels |
| podAnnotations | object | `{}` | Key-value metadata for individual pods |
| podSecurityContext | object | `{}` | Defines the security settings and privileges for a pod |
| postgresOperator.MasterLoadBalancer | bool | `false` |  |
| postgresOperator.ReplicaLoadBalancer | bool | `false` |  |
| postgresOperator.connectionPooler.enabled | bool | `false` | Enable the connection pooler |
| postgresOperator.connectionPooler.instanceCount | int | `3` |  |
| postgresOperator.connectionPooler.mode | string | `"session"` | In which mode to run connection pooler, transaction or session. |
| postgresOperator.connectionPooler.resources | object | `{}` | Consumers of this chart can override postgres cluster pod resource limits as follows: |
| postgresOperator.databases.fider | string | `"fider"` |  |
| postgresOperator.enableLogicalBackup | bool | `false` | Consumers of this chart can enable logical backups on a set schedule: |
| postgresOperator.enabled | bool | `false` | Enable the [Postgres Operator](https://postgres-operator.readthedocs.io/)? |
| postgresOperator.instanceCount | int | `1` |  |
| postgresOperator.logicalBackupSchedule | string | `"0 0 * * *"` |  |
| postgresOperator.parameters | object | `{}` | Consumers of this chart can override postgres parameters as follows: |
| postgresOperator.patroni | object | `{"retry_timeout":30,"ttl":70}` | Patroni is a template for high availability (HA) PostgreSQL solutions using Python |
| postgresOperator.podPriorityClassName | string | `""` | Consumers of this chart can set pod priority for postgres pods |
| postgresOperator.resources | object | `{}` |  |
| postgresOperator.tls.enabled | bool | `false` |  |
| postgresOperator.tls.issuer | string | `"cert-manager-issuer-common"` |  |
| postgresOperator.users.fider[0] | string | `"superuser"` |  |
| postgresOperator.users.fider[1] | string | `"createdb"` |  |
| postgresOperator.volumeSize | string | `"8Gi"` |  |
| postgresql.enabled | bool | `false` | Enable the PostgreSQL subchart? |
| postgresql.global.postgresql.auth.database | string | `"fider"` | PostgreSQL database |
| postgresql.global.postgresql.auth.password | string | `"s0m3g00dp4ssw0rd"` | PostgreSQL password |
| postgresql.global.postgresql.auth.username | string | `"fider"` | PostgreSQL username |
| postgresql.global.postgresql.service.ports.postgresql | int | `5432` |  |
| postgresql.primary.persistence.size | string | `"8Gi"` |  |
| replicaCount | int | `1` | The number of replicas to create |
| resources | object | `{}` | Kubernetes resources |
| securityContext | object | `{"allowPrivilegeEscalation":false,"readOnlyRootFilesystem":true,"runAsGroup":65534,"runAsNonRoot":true,"runAsUser":65534}` | Fider Container-level security-context |
| service | object | `{"port":3000,"type":"ClusterIP"}` | Kubernetes service configuration |
| service.port | int | `3000` | The HTTP service port |
| service.type | string | `"ClusterIP"` | The service type |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| serviceMonitor.enabled | bool | `false` | If `true`, a ServiceMonitor resource for the prometheus-operator is created |
| serviceMonitor.interval | string | `""` | Scrape interval. If not set, the Prometheus default scrape interval is used. |
| serviceMonitor.labels | object | `{}` | Labels for the ServiceMonitor |
| serviceMonitor.metricRelabelings | list | `[]` | MetricRelabelConfigs to apply to samples after scraping, but before ingestion. |
| serviceMonitor.relabelings | list | `[]` | RelabelConfigs to apply to samples before scraping |
| tolerations | list | `[]` | Allows a pod to tolerate or ignore specific node taints, enabling it to be scheduled on tainted nodes |
