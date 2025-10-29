# mmiles-pi-cluster-infra
Repository for Helm charts that are deployed to Pi Cluster

# Usage

### Manifests

Manifests can be installed just using `kubectl apply -f /path/to/dir/ --context mmiles-pi-cluster`

### Helm

`helm upgrade <chart_name> . --kube-context mmiles-pi-cluster --namespace test`
