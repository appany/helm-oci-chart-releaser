# 💥 Helm OCI Chart Releaser 💥

🚀 Push Helm Charts to OCI-based (Docker) registries! 🚀

💡 Store **Helm Charts** with your **Docker images**. No more need to host Helm repositories ♿

📝 More info about secure **OCI-based** hosting https://helm.sh/docs/topics/registries/

## Usage

- Push Helm Chart to **Github Container Registry**

```yaml
- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v0.2.0
  with:
    name: my-chart
    repository: appany
    tag: 0.1.0
    path: charts/my-chart # Default charts/{name}
    registry: ghcr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}

# helm pull ghcr.io/appany/my-chart:0.1.0
```

- Push Helm Chart to **Azure Container Registry**
```yaml
- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v0.2.0
  with:
    name: my-chart
    repository: helm
    tag: 0.1.0
    path: charts/my-chart # Default charts/{name}
    registry: appany.azurecr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}

# helm pull appany.azurecr.io/helm/my-chart:0.1.0
```

## Inputs

```yaml
inputs:
  name:
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
    description: Chart path (Default 'charts/{name}')
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

## Outputs

```yaml
outputs:
  image:
    value: ${{ steps.output.outputs.image }}
    description: Chart image (Default '{registry}/{repository}/{image}:{tag}')
```

## ArgoCD

1. Add container registry and enable OCI support
```yaml
repositories:
  ghcr:
    url: ghcr.io
    type: helm
    name: ...
    enableOCI: "true"

credentialTemplates:
  ghcr:
    url: ghcr.io
    username: ...
    password: ...
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
    chart: appany/my-chart
    helm:
      ...
```

## License

This project is distributed under the [MIT license](LICENSE.md).
