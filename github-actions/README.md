# Github Actions

## Errors

> **Creating a file or executing a command results in permission denied.**

Try to use that command with `sudo`. This will work in the Github Actions as they run with passwordless sudo.
For example the `Golang-Ci` tool must be installed with sudo: `curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sudo sh -s -- -b $(GOPATH)/bin v1.24.0`

> **Script that ends in error does not stop and fail the Github Action.**

It must end with the proper errno code, add `set -e` at the beggining of the script.

> **Environtment variable set in one step does not propagate to other steps.**

For example things like `export FOO=BAR` and using `${FOO}` in another step won't work, that's a current limitation of Github Actions.

## Documentation

> **Cache Docker Build or Docker Compose steps.**

From `https://github.com/marketplace/actions/build-and-push-docker-images#leverage-github-cache` and `https://github.com/marketplace/actions/docker-layer-caching`.

Add this step before the Docker Build or Docker-Compose:

```yaml
- name: Get Cache 📦
        uses: satackey/action-docker-layer-caching@v0.0.11
        continue-on-error: true
```

For fast builds or not good Dockerfiles that may always invalidate almost all the layers, it is faster not to use the cache.

> **Create tag of current commit and push it along.**

Run:

```
git tag -a v1.0.0 -m "First version"
git push --follow-tags
```

---

- https://github.com/actions/cache
