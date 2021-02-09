# Digital Ocean

## Install Doctl

From `https://www.digitalocean.com/docs/apis-clis/doctl/how-to/install/`.

```
sudo snap install doctl
sudo snap connect doctl:kube-config
sudo snap connect doctl:ssh-keys :ssh-keys
sudo snap connect doctl:dot-docker
doctl auth init --context <NAME>
doctl auth list
doctl auth switch --context <NAME>
doctl account get
```

## Documentation

- https://www.digitalocean.com/docs/volumes/
- https://www.digitalocean.com/docs/kubernetes/how-to/add-volumes/
- https://www.digitalocean.com/docs/kubernetes/how-to/add-load-balancers/
- https://www.digitalocean.com/docs/container-registry/how-to/use-registry-docker-kubernetes/#create-secret-manually
