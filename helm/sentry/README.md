# Sentry 10

Forked from **`https://github.com/sentry-kubernetes/charts`**, the license is kept as is.

## Installation

TODO

## NGINX and/or Ingress

By default, NGINX is enabled to allow sending the incoming requests to [Sentry Relay](https://getsentry.github.io/relay/) or the Django backend depending on the path. When Sentry is meant to be exposed outside of the Kubernetes cluster, it is recommended to disable NGINX and let the Ingress do the same. It's recommended to go with the go to Ingress Controller, [NGINX Ingress](https://kubernetes.github.io/ingress-nginx/) but others should work as well.

Note: if you are using NGINX Ingress, please set this annotation on your ingress : nginx.ingress.kubernetes.io/use-regex: "true"

## Clickhouse warning

Snuba only supports a UTC timezone for Clickhouse. Please keep the initial value!

## PostgresSQL

By default, PostgreSQL is installed as part of the chart. To use an external PostgreSQL server set `postgresql.enabled` to `false` and then set `postgresql.postgresHost` and `postgresql.postgresqlPassword`. The other options (`postgresql.postgresqlDatabase`, `postgresql.postgresqlUsername` and `postgresql.postgresqlPort`) may also want changing from their default values.

To avoid issues when upgrade this chart, provide `postgresql.postgresqlPassword` for subsequent upgrades. This is due to an issue in the PostgreSQL chart where password will be overwritten with randomly generated passwords otherwise. See https://github.com/helm/charts/tree/master/stable/postgresql#upgrade for more detail.

## Persistence

This chart is capable of mounting the sentry-data PV in the Sentry worker and cron pods. This feature is disabled by default, but is needed for some advanced features such as private sourcemaps.

You may enable mounting of the sentry-data PV across worker and cron pods by changing filestore.filesystem.persistence.persistentWorkers to true. If you plan on deploying Sentry containers across multiple nodes, you may need to change your PVC's access mode to ReadWriteMany and check that your PV supports mounting across multiple nodes.

## Configuration

The following table lists the configurable parameters of the Sentry chart and their default values.

| Parameter                                  | Description                                                                                                                                       | Default                        |
| :----------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------- |
| `user.create`                              | if `true`, creates a default admin user defined from `email` and `password`                                                                       | `true`                         |
| `user.email`                               | Admin user email                                                                                                                                  | `admin@sentry.local`           |
| `user.password`                            | Admin user password                                                                                                                               | `aaaa`                         |
| `ingress.enabled`                          | Enabling Ingress                                                                                                                                  | `false`                        |
| `ingress.regexPathStyle`                   | Allows setting the style the regex paths are rendered in the ingress for the ingress controller in use. Possible values are `nginx` and `traefik` | `nginx`                        |
| `nginx.enabled`                            | Enabling NGINX                                                                                                                                    | `true`                         |
| `metrics.enabled`                          | if `true`, enable Prometheus metrics                                                                                                              | `false`                        |
| `metrics.image.repository`                 | Metrics exporter image repository                                                                                                                 | `prom/statsd-exporter`         |
| `metrics.image.tag`                        | Metrics exporter image tag                                                                                                                        | `v0.10.5`                      |
| `metrics.image.PullPolicy`                 | Metrics exporter image pull policy                                                                                                                | `IfNotPresent`                 |
| `metrics.nodeSelector`                     | Node labels for metrics pod assignment                                                                                                            | `{}`                           |
| `metrics.tolerations`                      | Toleration labels for metrics pod assignment                                                                                                      | `[]`                           |
| `metrics.affinity`                         | Affinity settings for metrics                                                                                                                     | `{}`                           |
| `metrics.resources`                        | Metrics resource requests/limit                                                                                                                   | `{}`                           |
| `metrics.service.annotations`              | annotations for Prometheus metrics service                                                                                                        | `{}`                           |
| `metrics.service.clusterIP`                | cluster IP address to assign to service (set to `"-"` to pass an empty value)                                                                     | `nil`                          |
| `metrics.service.omitClusterIP`            | (Deprecated) To omit the `clusterIP` from the metrics service                                                                                     | `false`                        |
| `metrics.service.externalIPs`              | Prometheus metrics service external IP addresses                                                                                                  | `[]`                           |
| `metrics.service.additionalLabels`         | labels for metrics service                                                                                                                        | `{}`                           |
| `metrics.service.loadBalancerIP`           | IP address to assign to load balancer (if supported)                                                                                              | `""`                           |
| `metrics.service.loadBalancerSourceRanges` | list of IP CIDRs allowed access to load balancer (if supported)                                                                                   | `[]`                           |
| `metrics.service.servicePort`              | Prometheus metrics service port                                                                                                                   | `9913`                         |
| `metrics.service.type`                     | type of Prometheus metrics service to create                                                                                                      | `ClusterIP`                    |
| `metrics.serviceMonitor.enabled`           | Set this to `true` to create ServiceMonitor for Prometheus operator                                                                               | `false`                        |
| `metrics.serviceMonitor.additionalLabels`  | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus                                                             | `{}`                           |
| `metrics.serviceMonitor.honorLabels`       | honorLabels chooses the metric's labels on collisions with target labels.                                                                         | `false`                        |
| `metrics.serviceMonitor.namespace`         | namespace where servicemonitor resource should be created                                                                                         | `the same namespace as sentry` |
| `metrics.serviceMonitor.scrapeInterval`    | interval between Prometheus scraping                                                                                                              | `30s`                          |
| `system.secretKey`                         | secret key for the session cookie ([documentation](https://develop.sentry.dev/config/#general))                                                   | `nil`                          |

## Sentry secret key

For your security, the [`system.secret-key`](https://develop.sentry.dev/config/#general) is generated for you on the first installation. Another one will be regenerated on each upgrade invalidating all the current sessions unless it's been provided. The value is stored in the `sentry-sentry` configmap.

```
helm upgrade ... --set system.secretKey=xx
```
