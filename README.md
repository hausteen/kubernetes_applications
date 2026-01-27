# kubernetesApplications

I am using the app of apps pattern in Argo CD to deploy and manage Kubernetes applications.

## sync waves

| name | sync wave |
| ---- | --------- |
| namespaceCreation | 0 |
| customResourceDefinitions | 10 |
| certManager | 20 |
| envoyGateway | 30 |
| gatewayApi | 40 |
| cilium | 50 |
| longhorn | 60 |
| argocd | 70 |
| coredns | 80 |

## dependency list

| name | dependency list |
| ---- | ---------------- |
| namespaceCreation | none |
| customResourceDefinitions | namespaceCreation |
| certManager | namespaceCreation |
| envoyGateway | namespaceCreation |
| gatewayApi | namespaceCreation, certManager, envoyGateway |
| argocd | gatewayApi |
| cilium | gatewayApi |
| coredns | namespaceCreation, gatewayApi |
| longhorn | namespaceCreation, gatewayApi |

I am putting the gateway api routes with each application. That means then that envoy gateway, gateway api, and
certificates have to be in place before the other applications get installed.

## pod security admission standard

By default, this cluster is using the level = `restricted` for all 3 modes = `enforce`, `audit`, and `warn`.
Every namespace receives this level unless explicity overridden.
