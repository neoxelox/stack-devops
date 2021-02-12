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
- Add an `A` record in the domain DNS pointing to the created load balancer IP and wait until it resolves the hostname.
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

> **List HTTPS Certificates.**

Run `kubectl get certificates` and `kubectl describe certificates <CERTIFICATE>`.

Important, providers like letsencrypt do rate limit the provision of certificates of around 1 try every hour.
Always test correct provisioning with the staging environtment first!

> **Delete a Kubernetes Cluster from kubectl.**

Run: (The values below can be obtained by viewing the kubeconfig file)

```
kubectl config delete-cluster <CLUSTER>
kubectl config delete-context <CONTEXT>
kubectl config unset users.<USER>
```

> **HPA vs Replicas.**

In both the maximum number of replicas must be the number of Nodes of the cluster, so that each pod gets assigned to a different Node. Other than for redundancy, it does not make sense to have more than one instance running on the same Node.

The resource metric targets for the HPA are always calculated on base the `requests` not the `limits`, and you cannot leave blank the `limits` one. So, if you have a small Kubernetes cluster, it is better to use fixed Replicas in the Deployment without, or pretty high, resource `limits`. Otherwise, the overhead of having so many instances created by the HPA vs the low resource `requests` and `limits` settings, is too high.

---

- https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
