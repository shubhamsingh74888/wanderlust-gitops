# wanderlust-gitops

ArgoCD GitOps repository for the Wanderlust application — Kubernetes manifests 
watched and synced automatically by ArgoCD on the EKS cluster.

## What's here

| Folder | Purpose |
|---|---|
| `kubernetes/production/` | Deployment, Service, Ingress manifests — updated by Jenkins CI on every build |
| `argocd/` | ArgoCD Application definition |
| `monitoring.yaml` | Prometheus + Grafana stack config |

## How it works

1. Jenkins CI builds and pushes a new Docker image (`shubham74888/wanderlust:b<build>`)
2. Jenkins updates the image tag in `kubernetes/production/` and commits as `Wanderlust Jenkins Bot`
3. ArgoCD detects the change and syncs to the EKS cluster automatically — no manual `kubectl apply`

## Related Repos

| Repo | Role |
|---|---|
| [Wanderlust-Mega-Project](https://github.com/shubhamsingh74888/Wanderlust-Mega-Project) | App code + CI Jenkinsfile |
| [wanderlust-infra](https://github.com/shubhamsingh74888/wanderlust-infra) | Terraform infra + Packer AMI |
| [wanderlust-shared-lib](https://github.com/shubhamsingh74888/wanderlust-shared-lib) | Jenkins Shared Library |
| **wanderlust-gitops** | This repo — K8s manifests + ArgoCD |
