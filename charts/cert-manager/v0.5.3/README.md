## Installing the Chart

Full installation instructions, including details on how to configure extra
functionality in cert-manager can be found in the [getting started docs](https://cert-manager.readthedocs.io/en/latest/getting-started/).

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release stable/cert-manager
```

In order to begin issuing certificates, you will need to set up a ClusterIssuer
or Issuer resource (for example, by creating a 'letsencrypt-staging' issuer).

More information on the different types of issuers and how to configure them
can be found in our documentation:

https://cert-manager.readthedocs.io/en/latest/reference/issuers.html

For information on how to configure cert-manager to automatically provision
Certificates for Ingress resources, take a look at the `ingress-shim`
documentation:

https://cert-manager.readthedocs.io/en/latest/reference/ingress-shim.html

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the cert-manager chart and their default values.

| Parameter                                       | Description                                                                                                                              | Default                                    |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| `image.repository`                              | Image repository                                                                                                                         | `quay.io/jetstack/cert-manager-controller` |
| `image.tag`                                     | Image tag                                                                                                                                | `v0.5.3`                                   |
| `image.pullPolicy`                              | Image pull policy                                                                                                                        | `IfNotPresent`                             |
| `replicaCount`                                  | Number of cert-manager replicas                                                                                                          | `1`                                        |
| `createCustomResource`                          | Create CRD/TPR with this release                                                                                                         | `true`                                     |
| `clusterResourceNamespace`                      | Override the namespace used to store DNS provider credentials etc. for ClusterIssuer resources                                           | Same namespace as cert-manager pod         |
| `leaderElection.Namespace`                      | Override the namespace used to store the ConfigMap for leader election                                                                   | Same namespace as cert-manager pod         |
| `certificateResourceShortNames`                 | Custom aliases for Certificate CRD                                                                                                       | `["cert", "certs"]`                        |
| `extraArgs`                                     | Optional flags for cert-manager                                                                                                          | `[]`                                       |
| `extraEnv`                                      | Optional environment variables for cert-manager                                                                                          | `[]`                                       |
| `rbac.create`                                   | If `true`, create and use RBAC resources                                                                                                 | `true`                                     |
| `serviceAccount.create`                         | If `true`, create a new service account                                                                                                  | `true`                                     |
| `serviceAccount.name`                           | Service account to be used. If not set and `serviceAccount.create` is `true`, a name is generated using the fullname template            |                                            |
| `resources`                                     | CPU/memory resource requests/limits                                                                                                      |                                            |
| `nodeSelector`                                  | Node labels for pod assignment                                                                                                           | `{}`                                       |
| `affinity`                                      | Node affinity for pod assignment                                                                                                         | `{}`                                       |
| `tolerations`                                   | Node tolerations for pod assignment                                                                                                      | `[]`                                       |
| `ingressShim.defaultIssuerName`                 | Optional default issuer to use for ingress resources                                                                                     |                                            |
| `ingressShim.defaultIssuerKind`                 | Optional default issuer kind to use for ingress resources                                                                                |                                            |
| `ingressShim.defaultACMEChallengeType`          | Optional default challenge type to use for ingresses using ACME issuers                                                                  |                                            |
| `ingressShim.defaultACMEDNS01ChallengeProvider` | Optional default DNS01 challenge provider to use for ingresses using ACME issuers with DNS01                                             |                                            |
| `podAnnotations`                                | Annotations to add to the cert-manager pod                                                                                               | `{}`                                       |
| `podDnsPolicy`                                  | Optional cert-manager pod [DNS policy](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#pods-dns-policy)         |                                            |
| `podDnsConfig`                                  | Optional cert-manager pod [DNS configurations](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#pods-dns-config) |                                            |
| `podLabels`                                     | Labels to add to the cert-manager pod                                                                                                    | `{}`                                       |
| `http_proxy`                                    | Value of the `HTTP_PROXY` environment variable in the cert-manager pod                                                                   |                                            |
| `https_proxy`                                   | Value of the `HTTPS_PROXY` environment variable in the cert-manager pod                                                                  |                                            |
| `no_proxy`                                      | Value of the `NO_PROXY` environment variable in the cert-manager pod                                                                     |                                            |
| `webhook.enabled`                               | Toggles whether the validating webhook component should be installed                                                                     | `false`                                    |
| `webhook.replicaCount`                          | Number of cert-manager webhook replicas                                                                                                  | `1`                                        |
| `webhook.podAnnotations`                        | Annotations to add to the webhook pods                                                                                                   | `{}`                                       |
| `webhook.extraArgs`                             | Optional flags for cert-manager webhook component                                                                                        | `[]`                                       |
| `webhook.resources`                             | CPU/memory resource requests/limits for the webhook pods                                                                                 |                                            |
| `webhook.image.repository`                      | Webhook image repository                                                                                                                 | `quay.io/jetstack/cert-manager-webhook`    |
| `webhook.image.tag`                             | Webhook image tag                                                                                                                        | `v0.5.2`                                   |
| `webhook.image.pullPolicy`                      | Webhook image pull policy                                                                                                                | `IfNotPresent`                             |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml .
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Contributing

This chart is maintained at [github.com/jetstack/cert-manager](https://github.com/jetstack/cert-manager/tree/master/contrib/charts/cert-manager).
