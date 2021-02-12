# Cert Manager

## Installation

From `https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes#step-4-%E2%80%94-installing-and-configuring-cert-manager` and `https://cert-manager.io/docs/installation/kubernetes/`.

```
kubectl apply -f ./cert-manager.yaml
kubectl apply -f ./staging-issuer.yaml
kubectl apply -f ./production-issuer.yaml
```

Remember to change the email address used for ACME registration accordingly before applying the ClusterIssuers.

**Important**: The error `Cert Manager cannot issue certificates because of Pod reach-validation fails` always happens in DOKS, it may be fixed with the Pod communication through the Load Balancer workaround, see below.

## Errors

> **Cert Manager cannot issue certificates because of Pod reach-validation fails.**

Reinstall Cert Manager again with `kubectl label namespace kube-system certmanager.k8s.io/disable-validation="true"` first, or enable Pod communication through the Load Balancer, see `https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes#step-5-%E2%80%94-enabling-pod-communication-through-the-load-balancer-(optional)` and `https://www.digitalocean.com/docs/kubernetes/how-to/configure-load-balancers/#accessing-by-hostname-annotation`.

Cert-Manager full delete (except for the CRDs):

```
kubectl delete all --all -n cert-manager
kubectl delete pod/cm-acme-http-solver-**** # In the namespace where certificates were desired if any
kubectl delete service/cm-acme-http-solver-**** # In the namespace where certificates were desired if any
kubectl delete certificate **** # In the namespace where certificates were desired if any
kubectl delete ValidatingWebhookConfiguration cert-manager-webhook
```

Pod communication through Load Balancer for DOKS:

- Add an `A` record called `k8s` in the domain DNS pointing to the created load balancer IP and wait until it resolves the hostname.
- Live edit the Ingress Controller Service adding `service.beta.kubernetes.io/do-loadbalancer-hostname: "k8s.neoxelox.com"` to the annotations.
- Install Cert-Manager again.

## Documentation

---

- https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-on-digitalocean-kubernetes-using-helm
- https://www.youtube.com/watch?v=Wi1qEIkoONQ
