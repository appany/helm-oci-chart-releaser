# test-application

![Version: 0.0.0](https://img.shields.io/badge/Version-0.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.0.0](https://img.shields.io/badge/AppVersion-0.0.0-informational?style=flat-square)

A Helm chart for Kubernetes

## Requirements

| Repository | Name | Version |
| ---------- | ---- | ------- |

## Values

| Key                                        | Type   | Default                                                                     | Description |
| ------------------------------------------ | ------ | --------------------------------------------------------------------------- | ----------- |
| affinity                                   | object | `{}`                                                                        |             |
| application.dbConnection                   | string | `"mysql"`                                                                   |             |
| application.dbDatabase                     | string | `"test"`                                                                    |             |
| application.dbHost                         | string | `"mysql"`                                                                   |             |
| application.dbPassword                     | string | `"test"`                                                                    |             |
| application.dbPort                         | int    | `3306`                                                                      |             |
| application.dbUsername                     | string | `"test"`                                                                    |             |
| autoscaling.enabled                        | bool   | `false`                                                                     |             |
| autoscaling.maxReplicas                    | int    | `100`                                                                       |             |
| autoscaling.minReplicas                    | int    | `1`                                                                         |             |
| autoscaling.targetCPUUtilizationPercentage | int    | `80`                                                                        |             |
| fullnameOverride                           | string | `""`                                                                        |             |
| image.digest                               | string | `"sha256:da3b65f32ea75f8041079d220b72da4f605738996256a7dc32715424cc117271"` |             |
| image.pullPolicy                           | string | `"Always"`                                                                  |             |
| image.registry                             | string | `"ghcr.io"`                                                                 |             |
| image.repository                           | string | `"hoverkraft-tech/ci-github-container/application-test"`                    |             |
| image.tag                                  | string | `""`                                                                        |             |
| imagePullSecrets                           | list   | `[]`                                                                        |             |
| ingress.annotations                        | object | `{}`                                                                        |             |
| ingress.className                          | string | `""`                                                                        |             |
| ingress.enabled                            | bool   | `false`                                                                     |             |
| ingress.hosts[0].host                      | string | `"chart-example.local"`                                                     |             |
| ingress.hosts[0].paths[0].path             | string | `"/"`                                                                       |             |
| ingress.hosts[0].paths[0].pathType         | string | `"ImplementationSpecific"`                                                  |             |
| ingress.tls                                | list   | `[]`                                                                        |             |
| mysql.auth.database                        | string | `"test"`                                                                    |             |
| mysql.auth.password                        | string | `"test"`                                                                    |             |
| mysql.auth.rootPassword                    | string | `"root"`                                                                    |             |
| mysql.auth.username                        | string | `"test"`                                                                    |             |
| mysql.enabled                              | bool   | `false`                                                                     |             |
| mysql.fullnameOverride                     | string | `"mysql"`                                                                   |             |
| nameOverride                               | string | `""`                                                                        |             |
| nodeSelector                               | object | `{}`                                                                        |             |
| podAnnotations                             | object | `{}`                                                                        |             |
| podSecurityContext                         | object | `{}`                                                                        |             |
| replicaCount                               | int    | `1`                                                                         |             |
| resources.limits.cpu                       | string | `"100m"`                                                                    |             |
| resources.limits.memory                    | string | `"128Mi"`                                                                   |             |
| resources.requests.cpu                     | string | `"100m"`                                                                    |             |
| resources.requests.memory                  | string | `"128Mi"`                                                                   |             |
| securityContext.allowPrivilegeEscalation   | bool   | `false`                                                                     |             |
| securityContext.capabilities.drop[0]       | string | `"ALL"`                                                                     |             |
| securityContext.readOnlyRootFilesystem     | bool   | `true`                                                                      |             |
| securityContext.runAsNonRoot               | bool   | `true`                                                                      |             |
| securityContext.runAsUser                  | int    | `10001`                                                                     |             |
| securityContext.seccompProfile.type        | string | `"RuntimeDefault"`                                                          |             |
| service.port                               | int    | `8080`                                                                      |             |
| service.type                               | string | `"ClusterIP"`                                                               |             |
| serviceAccount.annotations                 | object | `{}`                                                                        |             |
| serviceAccount.create                      | bool   | `true`                                                                      |             |
| serviceAccount.name                        | string | `""`                                                                        |             |
| tolerations                                | list   | `[]`                                                                        |             |

---

Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
