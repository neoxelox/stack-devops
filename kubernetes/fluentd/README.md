# Fluentd

Forked from **`https://github.com/fluent/fluentd-kubernetes-daemonset/blob/master/fluentd-daemonset-elasticsearch-rbac.yaml `**, the license is kept as is.

## Installation

TODO

## Settings

### Use your configuration

These images have default configuration and support some environment variables for parameters
but it sometimes doesn't fit your case. If you want to use your configuration, use ConfigMap feature.

Each image has following configurations:

- fluent.conf: Destination setting, Elaticsearch, kafka and etc.
- kubernetes.conf: k8s specific setting. `tail` input for log files and `kubernetes_metadata` filter
- prometheus.conf: prometheus plugin for fluentd monitoring
- systemd.conf: systemd plugin for collecting systemd-journal log. See also "Disable systemd input" section.

Overwrite conf file via ConfigMap. See also several examples:

- [Cluster-level Logging in Kubernetes with Fluentd](https://medium.com/kubernetes-tutorials/cluster-level-logging-in-kubernetes-with-fluentd-e59aa2b6093a)
- https://github.com/fluent/fluentd-kubernetes-daemonset/pull/349#issuecomment-579097659

### Use FLUENT_CONTAINER_TAIL_EXCLUDE_PATH to exclude specific container logs

Since v1.9.3 or later images.

You can exclude container logs from `/var/log/containers/` with `FLUENT_CONTAINER_TAIL_EXCLUDE_PATH`.
If you have a trouble with specific log, use this envvar, e.g. `["/var/log/containers/logname-*"]`.

- `exclude_path` parameter document: https://docs.fluentd.org/input/tail#exclude_path
- Fluentd log issue with backslash: https://github.com/fluent/fluentd/issues/2545

### Disable systemd input

If you don't setup systemd in the container, fluentd shows following messages by default configuration.

```
[warn]: #0 [in_systemd_bootkube] Systemd::JournalError: No such file or directory retrying in 1s
[warn]: #0 [in_systemd_kubelet] Systemd::JournalError: No such file or directory retrying in 1s
[warn]: #0 [in_systemd_docker] Systemd::JournalError: No such file or directory retrying in 1s
```

You can suppress these messages by setting `disable` to `FLUENTD_SYSTEMD_CONF` environment variable in your kubernetes configuration.

### Disable prometheus input plugins

By default, latest images launch `prometheus` plugins to monitor fluentd.
You can disable prometheus input plugin by setting `disable` to `FLUENTD_PROMETHEUS_CONF` environment variable in your kubernetes configuration.

### Disable sed execution on elasticsearch image

This is for older images. Latest elasticsearch images don't use sed.

By historical reason, elasaticsearch image executes `sed` command during startup phase when `FLUENT_ELASTICSEARCH_USER` or `FLUENT_ELASTICSEARCH_PASSWORD` is specified. This sometimes causes a problem with read only mount.
To avoid this problem, set "true" to `FLUENT_ELASTICSEARCH_SED_DISABLE` environment variable in your kubernetes configuration.
