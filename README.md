# mmiles-pi-cluster-infra
Repository for Helm charts that are deployed to Pi Cluster

# Usage

### Manifests

Manifests can be installed just using `kubectl apply -f /path/to/dir/ --context mmiles-pi-cluster`

### Helm

* Whenever you edit/create a chart in `charts/`, it needs to be firstly packaged to the `docs/` folder (don't forget to bump chart version):

```commandline
helm package charts/<chart-name> -d docs/
```

* Then need to recreate the index.yaml (we're just using GitHub to host the helm repo):

```commandline
helm repo index ./docs --url https://raw.githubusercontent.com/matthewmiled/mmiles-pi-cluster-helm-repo/master/docs
```

* If the helm repo isn't already created, need to create it first:

```commandline
helm repo add mmiles-pi-cluster-helm-repo https://raw.githubusercontent.com/matthewmiled/mmiles-pi-cluster-helm-repo/master/docs
```

* Push all the chart changes to GitHub

* Then update the repo (may need to wait a few mins after pushing to GitHub):

```commandline
helm repo update
```

* Then install/upgrade the chart to the cluster:

```commandline
helm upgrade --install <chart-name> mmiles-pi-cluster-helm-repo/<chart-name> --namespace <test|infra|prod> --dry-run
```

* Can search releases using:

```commandline
helm search repo
```
