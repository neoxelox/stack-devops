# Metrics Server

## Installation

From `https://github.com/kubernetes-sigs/metrics-server` and `https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`.

```
kubectl apply -f ./metrics-server.yaml
```

## Errors

> **Metrics Server Pods unable to gather metrics from the Kubernetes API.**

Add `- --kubelet-insecure-tls` to the `metrics-server.yaml` deployment and reinstall Metrics Server.

## Documentation

---
