# Example Chart

## Installation

`helm upgrade --install --atomic --wait --timeout 60s shortr . -f ./values.yaml --namespace applications --set=image.tag=latest`

## Documentation

> **Access Shortr frontend deployed as a ClusterIP service.**

Run `kubectl port-forward --namespace applications svc/shortr 8080:80`.
Go to `localhost:8080`
