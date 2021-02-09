# Digital Ocean

## Digital Ocean private registry Usage

From `https://www.digitalocean.com/docs/container-registry/how-to/use-registry-docker-kubernetes/`.

```
doctl registry kubernetes-manifest > do-registry-image-pull-secret.yaml
kubectl apply -f ./do-registry-image-pull-secret.yaml
```

Remember to add the corresponding `namespace: <NAMESPACE>` (below `metadata`) for the Secret. It must be created in each Namespace where the images from the private registry are desired.

Remember to change the name if wanted.

In the deployment yaml file `image` part:

- Set `repository` to `registry.digitalocean.com/neoxelox/shortr`.
- Add `image pull Secret`:
  ```
  pullSecrets:
    - name: <REGISTRY SECRET NAME>
  ```

## NGINX ingress controller Installation

From `https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes#step-2-%E2%80%94-setting-up-the-kubernetes-nginx-ingress-controller` and `https://kubernetes.github.io/ingress-nginx/deploy/#digital-ocean` and `https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.44.0/deploy/static/provider/do/deploy.yaml`.

It is installed as a Deployment instead of a DaemonSet, because with a DaemonSet we have always one Pod per Node, each one accessing the Kubernetes API which may affect the Kubernetes Manager, and surely we won't need so many Ingress Controllers. We can manage the exact number of replicas in each Node with anty-affinity in the Deployment.

Run `kubectl apply -f ./do-nginx-ingress-controller.yaml`.

Remember to change parameters as desired:

Controller Service:

- `Annotations`:
  - `service.beta.kubernetes.io/do-loadbalancer-enable-proxy-protocol: 'true'`
  - `service.beta.kubernetes.io/do-loadbalancer-size-slug: 'lb-small'`

Controller Deployment:

- `replicas`
- `resources`

Controller HPA:

- `minReplicas`
- `maxReplicas`
- `targetAverageUtilization`
- `targetAverageUtilization`

## Errors

## Documentation

---

- https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-on-digitalocean-kubernetes-using-helm
- https://github.com/kubernetes/ingress-nginx/tree/master/charts/ingress-nginx
- https://www.digitalocean.com/docs/kubernetes/how-to/configure-load-balancers/#slug-size-annotation
