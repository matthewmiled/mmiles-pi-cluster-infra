# mmiles-pi-cluster-infra
Repository for Helm charts that are deployed to Pi Cluster

# Usage

### Manifests

Manifests can be installed just using `kubectl apply -f /path/to/dir/ --context mmiles-pi-cluster`

### Helm

For new installs:

`helm install <chart_name> . --kube-context mmiles-pi-cluster --namespace test`

For upgrades:

`helm upgrade <chart_name> . --kube-context mmiles-pi-cluster --namespace test`

# Troubleshooting

### DNS Resolution

If DNS fails (e.g. pods can't pull images), check which nameservers are being used on the pis:

```
matt@mmiles-pi-master-00:~$ cat /etc/resolv.conf
nameserver 1.1.1.1
nameserver 8.8.8.8
```

1.1.1.1. and 8.8.8.8 are the google and cloudflare nameservers. If they don't appear, then add them:

`sudo bash -c 'echo -e "nameserver 1.1.1.1\nnameserver 8.8.8.8" > /etc/resolv.conf'`
