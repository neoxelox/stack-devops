# Kubernetes Dashboard

Forked from **`https://github.com/kubernetes/dashboard/tree/master/aio/deploy/helm-chart/kubernetes-dashboard`**, the license is kept as is.

## Installation

TODO
`helm install kubernetes-dashboard/kubernetes-dashboard --name my-release`

## Getting Started

**IMPORTANT:** Read the [Access Control](docs/user/access-control/README.md) guide before performing any further steps. The default Dashboard deployment contains a minimal set of RBAC privileges needed to run.

### Access

To access Dashboard from your local workstation you must create a secure channel to your Kubernetes cluster. Run the following command:

```sh
$ kubectl proxy
```

Now access Dashboard at:

[`http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/`](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/).

## Create An Authentication Token (RBAC)

To find out how to create sample user and log in follow [Creating sample user](docs/user/access-control/creating-sample-user.md) guide.

**NOTE:**

- Kubeconfig Authentication method does not support external identity providers or certificate-based authentication.
- [metrics-server](https://github.com/kubernetes-sigs/metrics-server) has to be running in the cluster for the metrics and graphs to be available. Read more about it in [Integrations](docs/user/integrations.md) guide.

## Documentation

Dashboard documentation can be found on [docs](https://github.com/kubernetes/dashboard/tree/master/docs) directory which contains:

## License

[Apache License 2.0](https://github.com/kubernetes/dashboard/blob/master/LICENSE)

---

_Copyright 2019 [The Kubernetes Dashboard Authors](https://github.com/kubernetes/dashboard/graphs/contributors)_

---

## Access control

It is critical for the Kubernetes cluster to correctly setup access control of Kubernetes Dashboard.
See this [guide](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/README.md) for details.

It is highly recommended to use RBAC with minimal privileges needed for Dashboard to run.

## Configuration

The following table lists the configurable parameters of the kubernetes-dashboard chart and their default values.

| Parameter                                 | Description                                                                                                                  | Default                                                                                             |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `image.repository`                        | Repository for container image                                                                                               | `kubernetesui/dashboard`                                                                            |
| `image.tag`                               | Image tag                                                                                                                    | `v2.1.0`                                                                                            |
| `image.pullPolicy`                        | Image pull policy                                                                                                            | `IfNotPresent`                                                                                      |
| `image.pullSecrets`                       | Image pull secrets                                                                                                           | `[]`                                                                                                |
| `replicaCount`                            | Number of replicas                                                                                                           | `1`                                                                                                 |
| `annotations`                             | Annotations for deployment                                                                                                   | `{}`                                                                                                |
| `labels`                                  | Labels for deployment                                                                                                        | `{}`                                                                                                |
| `extraArgs`                               | Additional container arguments                                                                                               | `[]`                                                                                                |
| `extraEnv`                                | Additional container environment variables                                                                                   | `[]`                                                                                                |
| `extraVolumes`                            | Additional volumes                                                                                                           | `[]`                                                                                                |
| `extraVolumeMounts`                       | Additional container volumeMounts                                                                                            | `[]`                                                                                                |
| `podAnnotations`                          | Annotations to be added to pods                                                                                              | `seccomp.security.alpha.kubernetes.io/pod: 'runtime/default'}`                                      |
| `podLabels`                               | Labels to be added to pods                                                                                                   | `{}`                                                                                                |
| `nodeSelector`                            | node labels for pod assignment                                                                                               | `{}`                                                                                                |
| `tolerations`                             | List of node taints to tolerate (requires Kubernetes >= 1.6)                                                                 | `[]`                                                                                                |
| `affinity`                                | Affinity for pod assignment                                                                                                  | `[]`                                                                                                |
| `priorityClassName`                       | Name of Priority Class to assign pods                                                                                        | `nil`                                                                                               |
| `resources`                               | Pod resource requests & limits                                                                                               | `limits: {cpu: 2, memory: 100Mi}, requests: {cpu: 100m, memory: 100Mi}`                             |
| `protocolHttp`                            | Serve application over HTTP without TLS                                                                                      | `false`                                                                                             |
| `service.type`                            | Service type                                                                                                                 | `ClusterIP`                                                                                         |
| `service.externalPort`                    | Dashboard external port                                                                                                      | `443`                                                                                               |
| `service.loadBalancerSourceRanges`        | list of IP CIDRs allowed access to load balancer (if supported)                                                              | `nil`                                                                                               |
| `service.loadBalancerIP`                  | A user-specified IP address for load balancer to use as External IP (if supported)                                           | `nil`                                                                                               |
| `service.clusterServiceLabel.enabled`     | Enable the cluster-service label                                                                                             | `true`                                                                                              |
| `service.clusterServiceLabel.key`         | The cluster-service label key                                                                                                | `kubernetes.io/cluster-service`                                                                     |
| `ingress.annotations`                     | Specify ingress class                                                                                                        | `kubernetes.io/ingress.class: nginx`                                                                |
| `ingress.labels`                          | Add custom labels                                                                                                            | `[]`                                                                                                |
| `ingress.enabled`                         | Enable ingress controller resource                                                                                           | `false`                                                                                             |
| `ingress.paths`                           | Paths to match against incoming requests. Both `/` and `/*` are required to work on gce ingress.                             | `[/]`                                                                                               |
| `ingress.customPaths`                     | Override the default ingress paths                                                                                           | `[]`                                                                                                |
| `ingress.hosts`                           | Dashboard Hostnames                                                                                                          | `nil`                                                                                               |
| `ingress.tls`                             | Ingress TLS configuration                                                                                                    | `[]`                                                                                                |
| `settings`                                | Global dashboard settings                                                                                                    | `{}`                                                                                                |
| `pinnedCRDs`                              | Pinned CRDs that will be displayed in dashboard's menu                                                                       | `[]`                                                                                                |
| `metricsScraper.enabled`                  | Wether to enable dashboard-metrics-scraper                                                                                   | `false`                                                                                             |
| `metricsScraper.image.repository`         | Repository for metrics-scraper image                                                                                         | `kubernetesui/metrics-scraper`                                                                      |
| `metricsScraper.image.tag`                | Repository for metrics-scraper image tag                                                                                     | `v1.0.6`                                                                                            |
| `metricsScraper.containerSecurityContext` | SecurityContext for the kubernetes dashboard metrics scraper container                                                       | `{allowPrivilegeEscalation:false, readOnlyRootFilesystem: true, runAsUser: 1001, runAsGroup: 2001}` |
| `metrics-server.enabled`                  | Wether to enable metrics-server                                                                                              | `false`                                                                                             |
| `rbac.create`                             | Create & use RBAC resources                                                                                                  | `true`                                                                                              |
| `rbac.clusterRoleMetrics`                 | If set, an additional cluster role / role binding will be created to access metrics.                                         | `true`                                                                                              |
| `rbac.clusterReadOnlyRole`                | If set, an additional cluster role / role binding will be created with read only permissions to all resources listed inside. | `false`                                                                                             |
| `serviceAccount.create`                   | Whether a new service account name that the agent will use should be created.                                                | `true`                                                                                              |
| `serviceAccount.name`                     | Service account to be used. If not set and serviceAccount.create is `true` a name is generated using the fullname template.  |
| `livenessProbe.initialDelaySeconds`       | Number of seconds to wait before sending first probe                                                                         | `30`                                                                                                |
| `livenessProbe.timeoutSeconds`            | Number of seconds to wait for probe response                                                                                 | `30`                                                                                                |
| `podDisruptionBudget.enabled`             | Create a PodDisruptionBudget                                                                                                 | `false`                                                                                             |
| `podDisruptionBudget.minAvailable`        | Minimum available instances; ignored if there is no PodDisruptionBudget                                                      |
| `podDisruptionBudget.maxUnavailable`      | Maximum unavailable instances; ignored if there is no PodDisruptionBudget                                                    |
| `securityContext`                         | PodSecurityContext for pod level securityContext                                                                             | `nil`                                                                                               |
| `containerSecurityContext`                | SecurityContext for the kubernetes dashboard container                                                                       | `{allowPrivilegeEscalation:false, readOnlyRootFilesystem: true, runAsUser: 1001, runAsGroup: 2001}` |
| `networkPolicy.enabled`                   | Whether to create a network policy that allows access to the service                                                         | `false`                                                                                             |
| `podSecurityPolicy.enabled`               | Whether to create a pod security policy that allows fine-grained authorization of pod creation and updates                   | `false`                                                                                             |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install kubernetes-dashboard/kubernetes-dashboard --name my-release \
  --set=service.externalPort=8080,resources.limits.cpu=200m
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install kubernetes-dashboard/kubernetes-dashboard --name my-release -f values.yaml
```

> **Tip**: You can use the default [values.yaml](values.yaml), which is used by default, as reference

## Access

For information about how to access, please read the [kubernetes-dashboard manual](https://github.com/kubernetes/dashboard)

### Using the dashboard with 'kubectl proxy'

When running 'kubectl proxy', the address `localhost:8001/ui` automatically expands to:

- `http://localhost:8001/api/v1/namespaces/my-namespace/services/https:kubernetes-dashboard:https/proxy/`

For this to reach the dashboard, the name of the service must be 'kubernetes-dashboard', not any other value as set by Helm.
You can manually specify this using the value 'fullnameOverride':

```
fullnameOverride: 'kubernetes-dashboard'
```
