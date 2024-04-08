# This is a Quick-Start for ArgoRollouts

## this enables you to quickly deploy argo-Rollouts rollout-manager and Dashboard via a Helm Chart

to use the helm chart you can use it dirctly from the ghcr.io or pull it to your local station

```Bash
helm pull oci://ghcr.io/tal-hason/argo-rollouts-stuff/helm/rollouts-manager:0.1.1
```

in the value file here is the major keys:

| Key                                | Value                                   | Description                                                                                             |
|------------------------------------|-----------------------------------------|---------------------------------------------------------------------------------------------------------|
| replicaCount                       | 1                                       | Number of replicas for the rollouts-manager deployment                                                    |
| image.registry                     | quay.io                                | Registry where the image is hosted                                                                       |
| image.repository                   | openshiftdemos                         | Repository of the image                                                                                  |
| image.name                         | rollouts-terminal-tooling               | Name of the image                                                                                        |
| image.pullPolicy                   | Always                                  | Pull policy for the image                                                                                |
| image.tag                          | 1.11                                    | Tag of the image                                                                                         |
| imagePullSecrets                   | []                                      | Secrets for pulling the image                                                                            |
| nameOverride                       | ""                                      | Override for the Helm chart name                                                                          |
| fullnameOverride                   | ""                                      | Override for the full name of resources                                                                   |
| serviceAccount.create              | true                                    | Specifies whether a service account should be created                                                     |
| serviceAccount.annotations         | {}                                      | Annotations to add to the service account                                                                 |
| serviceAccount.name                | rollouts-manager                        | Name of the service account                                                                              |
| service.type                       | ClusterIP                               | Type of service                                                                                          |
| service.port                       | 3100                                    | Port for the service                                                                                     |
| service.portName                   | 3100-tcp                                | Name of the service port                                                                                 |
| route.enabled                      | true                                    | Whether to create an OpenShift route                                                                     |
| route.clusterDomain                | apps-crc.testing                        | Cluster domain for the OpenShift route                                                                   |
| route.tls.insecureEdgeTerminationPolicy | Redirect                            | Edge termination policy for TLS                                                                          |
| route.tls.termination              | edge                                    | TLS termination policy for the route                                                                     |
| resources                          | {}                                      | Resource requests and limits for the deployment                                                          |
| nodeSelector                       | {}                                      | Node selector for the deployment                                                                         |
| tolerations                        | []                                      | Tolerations for the deployment                                                                           |
| affinity                           | {}                                      | Affinity settings for the deployment                                                                     |
| podAnnotations                     | {}                                      | Annotations for the deployment pods                                                                       |
| podSecurityContext                 | {}                                      | Security context for the deployment pods                                                                 |
| securityContext                    | {}                                      | Security context for the containers in the deployment                                                     |

---

## Under exmaples there is a tested and working example of a blue-green rollout deployment

under examples/blugreen/base

```Bash
oc apply -k examples/blugreen/base
```

```Bash
yq -i '.spec.template.spec.containers[].image |= sub(":.*", ":<<new_color>>") examples/blugreen/base/rollout.yaml'
```

change the image tag to the following colors to test how the rollout works.

1. blue (default)
2. green
3. orange
4. purple
5. yellow

