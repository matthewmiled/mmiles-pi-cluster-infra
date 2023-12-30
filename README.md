# mmiles-pi-cluster-helm-repo
Repository for Helm charts that are deployed to Pi Cluster

# Add Helm repository
`helm repo add mmiles-pi-cluster-helm-repo https://github.com/matthewmiled/mmiles-pi-cluster-helm-repo/`

# Deploy a Helm Release
`helm upgrade --install <chart-name> mmiles-pi-cluster-helm-repo/<chart-release> --namespace <namespace> --dry-run`
