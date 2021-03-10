# 💥 Helm OCI Chart Releaser 💥

🚀 Push Helm Charts to OCI-based registries! 🚀

💡 Store **Helm Charts** with your **Docker images**. No more need to host Helm repositories ♿

📝 More info about secure **OCI-based** hosting https://helm.sh/docs/topics/registries/

## Usage

- Push Helm Chart to **Github Container Registry**

```yaml
# helm chart pull ghcr.io/appany/super-chart:0.1.0
# helm chart export ghcr.io/appany/super-chart:0.1.0

- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v0.1.0
  with:
    image: super-chart
    repository: appany
    tag: 0.1.0
    path: charts/super-chart
    registry: ghcr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}
```

- Push Helm Chart to **Azure Container Registry**
```yaml
# helm chart pull appany.azurecr.io/helm/super-chart:0.1.0
# helm chart export appany.azurecr.io/helm/super-chart:0.1.0

- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v0.1.0
  with:
    image: super-chart
    repository: helm
    tag: 0.1.0
    path: charts/super-chart
    registry: appany.azurecr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}
```

## Inputs

```yaml
# {registry}/{repository}/{image}:{tag}

image:
  required: true
  description: Chart name
repository:
  required: true
  description: Chart repository name
tag:
  required: true
  description: Chart version
path:
  required: false
  description: Chart path
  default: charts
registry:
  required: true
  description: OCI registry
registry_username:
  required: true
  description: OCI registry username
registry_password:
  required: true
  description: OCI registry password
```

## ArgoCD

1. Add container registry and enable OCI support
```yaml
repositories: |
  - url: ghcr.io
    type: helm
    name: appany
    enableOCI: true

repository.credentials: |
  - url: ghcr.io
    passwordSecret: ...
    usernameSecret: ...
```

2. Create an Application
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
...
spec:
  source:
    repoURL: ghcr.io
    targetRevision: 0.1.0
    chart: appany/super-chart
    helm:
      ...
```

## License

This project is distributed under the [MIT license](LICENSE.md).
