# 💥 Helm OCI Chart Releaser 💥

🚀 Push Helm Charts to OCI-based (Docker) registries! 🚀

💡 Store **Helm Charts** with your **Docker images**. No more need to host Helm repositories ♿

📝 More info about secure **OCI-based** hosting https://helm.sh/docs/topics/registries/

## Usage

- Push Helm Chart to **Github Container Registry**

```yaml
- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v0.5.0
  with:
    name: my-chart
    repository: appany
    tag: 0.1.0
    path: charts/my-chart # Default charts/{name}
    registry: ghcr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}
    update_dependencies: 'true' # Defaults to false

# helm pull ghcr.io/appany/my-chart:0.1.0
```

- Push Helm Chart to **Github Container Registry** and sign the package

```yaml
- name: Import GPG key
  uses: crazy-max/ghaction-import-gpg@v6
  id: gpg
  with:
    gpg_private_key: ${{ secrets.GPG_PRIVATE_KEY }} # Private key of the GPG key
    passphrase: ${{ secrets.GPG_PASSPHRASE }} # Passphrase for the key, if required

# Helm requires the legacy GPG format
# @link https://helm.sh/docs/topics/provenance/#the-workflow
- name: Convert GPG v2 key
  run: |
    gpg --export > ~/.gnupg/pubring.gpg
    gpg --batch --pinentry-mode loopback --yes --passphrase '${{ secrets.GPG_PASSPHRASE }}' --export-secret-key > ~/.gnupg/secring.gpg
- name: Chart | Push and sign
  uses: appany/helm-oci-chart-releaser@v0.5.0
  with:
    name: my-chart
    repository: appany
    tag: 0.1.0
    path: charts/my-chart # Default charts/{name}
    registry: ghcr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}
    sign: true
    signing_key: ${{ steps.gpg.outputs.name }}
    signing_passphrase: ${{ secrets.GPG_PASSPHRASE }}
    update_dependencies: 'true' # Defaults to false

# helm pull ghcr.io/appany/my-chart:0.1.0
```

- Push Helm Chart to **Azure Container Registry**
```yaml
- name: Chart | Push
  uses: appany/helm-oci-chart-releaser@v0.5.0
  with:
    name: my-chart
    repository: helm
    tag: 0.1.0
    path: charts/my-chart # Default charts/{name}
    registry: appany.azurecr.io
    registry_username: ${{ secrets.REGISTRY_USERNAME }}
    registry_password: ${{ secrets.REGISTRY_PASSWORD }}
    update_dependencies: 'true' # Defaults to false

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
  sign:
    required: false
    default: 'false'
    description: Use a PGP private key to sign this package
  signing_key:
    required: false
    default: ''
    description: Name of the key to use when signing. Required if "sign" is true
  signing_passphrase:
    required: false
    default: ''
    description: Passphrase for the signing key
  signing_keyring:
    required: false
    default: ~/.gnupg/secring.gpg
    description: Location of the public keyring
  update_dependencies:
    required: false
    default: 'false'
    description: Update chart dependencies before packaging (Default 'false')
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
