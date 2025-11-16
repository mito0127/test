# TTest of CI/CD with GitHub Actions and Argo CD

## CI
1. When a tag is applied, GitHub Actions are triggered to build a Docker image using the `Dockerfile` located in the `app` directory.
2. `image` in the `deployment.yaml` file under `manifest/base` is updated with the information of the created Docker image. Simultaneously, the version information in the `versions.txt` files under `manifest/overlays/dev` and `manifest/overlays/prod` are also updated.

## CD
1. Create `test-dev` application within Argo CD that monitors `manifest/overlays/dev` and enable Auto-Sync when updates occur. Updates of `version.txt` (in the CI process) trigger automatic Deployment rebuilds in the Kubernetes Cluster.
2. Similarly, create `test-prod` application within Argo CD that monitors `manifest/overlays/prod` and disable Auto-Sync. Updates of `version.txt` (in the CI process) lead to Out of Sync status of `test-prod`. To sync `test-prod`, manual sync process is required.
