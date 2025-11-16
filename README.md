# TTest of CI/CD with GitHub Actions and Argo CD

## CI
1. When a tag is applied, GitHub Actions are triggered to build a Docker image using the `Dockerfile` located in the `app` directory.
2. `image` in the `deployment.yaml` file under `manifest/base` is updated with the information of the created Docker image. Simultaneously, the version information in the `versions.txt` files under `manifest/overlays/dev` and `manifest/overlays/prod` are also updated.

## CD
1. Create a `test-dev` application within Argo CD that monitors `manifest/overlays/dev` and automatically syncs when updates occur. This triggers automatic Deployment rebuilds based on version.txt updates.
2. SSimilarly, creating a `test-prod` application within Argo CD that monitors `manifest/overlays/prod` but sets Sync to manual will detect an Out of Sync state triggered by updates to version.txt. Since `test-prod` does not rebuild automatically, safe operations are possible.
