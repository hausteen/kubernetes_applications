# kubernetesApplications

I am using the app of apps pattern in Argo CD to deploy and manage Kubernetes applications.

## dependency order / sync wave

| name | sync wave | reason |
| ---- | --------- | ------ |
| cilium | 10 | this is the cni and needs to be configured first |
| argocd | 20 | the less it manages before it self-manages, the better |
| certManager | 30 | get certificates up so they are available for other services |
| istio | 40 | overlay networking service mesh |
| longhorn | 50 | storage |
| gatewayApi | 60 | gateways and routes. needs istio |
