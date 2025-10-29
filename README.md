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

Since installing pihole, there has been a few DNS resolution issues (because pihole itself acts as a nameserver). A lot of the solutions using `systemd-resolved` to dynamically update the `/etc/resolv.conf` didn't seem to work on the pis, but this slightly hacky one did.

If DNS fails (e.g. pods can't pull images), check which nameservers are being used on the pis:

```
matt@mmiles-pi-worker-01:~$ cat /etc/resolv.conf
nameserver 1.1.1.1
nameserver 8.8.8.8
nameserver 9.9.9.9
```

1.1.1.1, 8.8.8.8 and 9.9.9.9 are the Cloudflare, Google and Quad9 nameservers. If none of them appear, then you can add them by doing the following:


1. Disabling systemctl: `sudo systemctl disable --now systemd-resolved`

2. Removing the existing file: `sudo rm /etc/resolv.conf`

3. Repopulating it with the nameservers: `echo -e "nameserver 1.1.1.1\nnameserver 8.8.8.8\nnameserver 9.9.9.9" | sudo tee /etc/resolv.conf`

4. And then making it immutable (a bit hacky): `sudo chattr +i /etc/resolv.conf`


