# stack-devops

**`My Full DevOps Stack.`**

_`Note: almost all things are forked resources, and thus, they do keep the original licenses.`_

## `Development`

#### `Docker`

- [**`Resources`**](docker#Docker)
  - [**`Errors`**](docker#Errors)
- [**`Images`**](docker/images)
  - [**`Go`**](docker/images/go)
  - [**`Python`**](docker/images/python)

#### `Docker-Compose`

- [**`Resources`**](docker#Docker-Compose)
- [**`Composables`**](docker/composables)

## `Infrastructure`

#### `Digital Ocean`

- [**`Resources`**](platforms/digital-ocean/README.md)
  - [**`Install Doctl`**](platforms/digital-ocean#Install-Doctl)
- [**`App Platform`**](platforms/digital-ocean/app-platform/README.md)
- [**`Managed PostgreSQL`**](platforms/digital-ocean/postgresql/README.md)
- [**`Spaces`**](platforms/digital-ocean/spaces/README.md)

#### `Terraform`

- [**`Resources`**](terraform/README.md)
- [**`Digital Ocean`**](terraform/digital-ocean/README.md)

#### `Kubernetes`

- [**`Resources`**](kubernetes/README.md)
  - [**`Local Installation`**](kubernetes#Local-Installation)
  - [**`DOKS Installation`**](kubernetes#DOKS-Installation)
  - [**`Errors`**](kubernetes#Errors)
- [**`Miscellaneous`**](kubernetes/miscellaneous)
- [**`Fluentd`**](kubernetes/fluentd)
- [**`Metrics-Server`**](kubernetes/metrics-server)
- [**`Cert-Manager`**](kubernetes/cert-manager)
- [**`Digital Ocean`**](kubernetes/digital-ocean)
  - [**`Private Registry`**](kubernetes/digital-ocean)
  - [**`Nginx Controller`**](kubernetes/digital-ocean)

## `Integration & Deployment`

#### `Github Actions`

- [**`Resources`**](github-actions/README.md)
- [**`Go`**](github-actions/go)
  - [**`Module`**](github-actions/go/module)
  - [**`Integration`**](github-actions/go/integration)
  - [**`Deployment`**](github-actions/go/deployment)
- [**`Python`**](github-actions/python)
  - [**`Package`**](github-actions/python/package)
  - [**`Integration`**](github-actions/python/integration)
  - [**`Deployment`**](github-actions/python/deployment)

#### `Helm`

- [**`Resources`**](helm/README.md)
  - [**`Installation`**](helm#Installation)
  - [**`Errors`**](helm#Errors)
  - [**`Example`**](helm/shortr)
- [**`Charts`**](helm)
  - [**`Elasticsearch`**](helm/elasticsearch)
  - [**`Kibana`**](helm/kibana)
  - [**`APM-Server`**](helm/apm-server)
  - [**`Kubernetes Dashboard`**](helm/kubernetes-dashboard)
  - [**`Sentry`**](helm/sentry)
