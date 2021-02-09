# Helm

## Installation

From `https://helm.sh/docs/intro/install/`.

```
sudo curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
chmod g-r ~/.kube/config
chmod o-r ~/.kube/config
```

## Commands

- `helm create <NAME>`
- `helm list`
- `helm history <NAME>`
- `helm rollback <NAME>`
- `helm lint <PATH TO CHART>`
- `helm upgrade --install --atomic --wait --timeout 60s <NAME> <PATH TO CHART> -f <PATH TO VALUES> --namespace <NAMESPACE> --set=image.tag=<IMAGE TAG>`
  It will wait until the new pods have started, otherwise, at 60s, it will rollback any changes made.
- `helm uninstall <NAME> --namespace <NAMESPACE>`

## Errors

> **Helm cannot install or upgrade a chart because the subcharts are not present.**

Run `helm dependency update`.

## Documentation

> **Hosts of other applications of the cluster.**

Example: `postgres-postgresql.applications.svc.cluster.local.`
The final dot is important as it will require less DNS calls to resolve the hostname.

> **Upgrading container images.**

Set `pullPolicy` to `IfNotPresent` to enhance pod startup.
Run Helm upgrade in the CI with `--set=image.tag=<COMMIT SHA>`, the image has previously been built and pushed to the private registry also tagged with the `COMMIT SHA` of that pull request.

> **Install Postgres Chart.**

Values: `https://github.com/bitnami/charts/tree/master/bitnami/postgresql/#parameters`

Run:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install postgres bitnami/postgresql -f <PATH TO VALUES> --namespace <NAMESPACE>
```
