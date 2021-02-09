# Kubernetes

## Local Installation

From `https://ubuntu.com/kubernetes/install#single-node`.

```
sudo apt update
sudo apt install snapd
sudo snap install microk8s --classic
sudo usermod -a -G microk8s alex
sudo chown -f -R alex ~/.kube
newgrp microk8s
microk8s.status --wait-ready
microk8s.kubectl config view --raw > $HOME/.kube/config
microk8s.enable dns
```

## DOKS Installation

- Get kubectl config `doctl kubernetes clusters kubeconfig save <CLUSTER>`.
- Create namespace `applications` for own services.
- Add Digital Ocean private registry Secret.
- Install Metrics Server.
- Install NGINX Ingress Controller.
- Add an `A` record in the domain DNS pointing to the created load balancer IP.
- Deploy an example chart and test http connection.
- Install Cert Manager and LetsEncrypt ClusterIssuers.
- Update example chart with ingress tls activated and Test https connection.

## Errors

> **Kubectl does not work because of microk8s certificates error.**

Run `sudo microk8s.refresh-certs`.

> **Microk8s DNS Pods not working.**

Run `sudo iptables -P FORWARD ACCEPT`.
See the changes with `sudo iptables -L FORWARD`.
Revert with `sudo iptables -P FORWARD DROP`.

> **HPA not working because cannot compute target metrics.**

Set `requests` and `limits` resources for the Container.
Install `Metrics-Server`.

## Documentation

> **Modify an existing Secret.**

Data is base64 encoded.
Run `KUBE_EDITOR="nano" kubectl edit secret <NAME>`.
The `micro` editor also works if it is installed in the machine.

Decode base64 string `echo dGVzdDEyMw== | base64 -d`.
Encode to base64 string `echo test123 | base64`.

If you re-apply yaml file with an existing secret it will be updated.

> **Create a Namespace from terminal.**

Run `kubectl create namespace <NAME>`

> **See logs of a running Pod.**

Run `kubectl logs <NAME> -f`.
The parameter `--tail=1000` helps if the logs are too old.

> **Access locally a Service deployed as a ClusterIP.**

Run `kubectl port-forward --namespace <NAMESPACE> svc/<NAME> <OUTSIDE PORT>:<INSIDE PORT>`.

Outside ports as `80` may not be allowed.
This command does not work with some applications (as Kubernetes Dashboard).

> **Get a terminal of a running Pod.**

Run `kubectl exec <NAME> -it sh`.
If `bash` is installed inside the container it also works.
The parameter `-c <CONTAINER>` helps if the Pod have more than one container inside.

> **Delete all resources of a Namespace.**

Run `kubectl delete all --all --namespace <NAMESPACE>`.

---

- https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
