# Docker

## Errors

> **Requests from inside of the container to external servers via https do not work.**

The ca certifcates have not been installed in the container.

- For alpine add: `RUN apk add ca-certificates`

## Documentation

> **Build, tag and push image to Digital Ocean private registry.**

Install `doctl`.
Run `doctl registry login`.
Build and tag image `docker build -f <PATH TO DOCKERFILE> <PATH TO CONTEXT> -t registry.digitalocean.com/<REGISTRY>/<IMAGE>:<TAG>`.
Push `docker push registry.digitalocean.com/<REGISTRY>/<IMAGE>:<TAG>`.

# Docker-Compose
