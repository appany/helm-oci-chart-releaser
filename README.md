# 💥 Helm OCI Chart releaser 💥

🚀 Push Helm Charts to OCI-based registries. 🚀

💡 Store Helm Charts with your Docker images. No more need to host Helm repositories! ♿

📝 More info about secure OCI-based hosting https://helm.sh/docs/topics/registries/

## Usage

```yaml
# Push Helm Chart to Github Container Registry

- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v1
  with:
    image: super-chart
    repository: appany
    tag: 0.1.0
    path: charts/super-chart
    registry: ghcr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}

# helm chart pull ghcr.io/appany/super-chart:0.1.0
# helm chart export ghcr.io/appany/super-chart:0.1.0
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