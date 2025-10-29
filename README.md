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

Since installing pihole, there has been a few DNS resolution issues (because pihole itself acts as a nameserver).

If DNS fails (e.g. pods can't pull images), check which nameservers are being used on the pis:

```
matt@mmiles-pi-master-00:~$ resolvectl status
Global
           Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
    resolv.conf mode: stub
         DNS Servers: 9.9.9.9
Fallback DNS Servers: 1.1.1.1

...
```

9.9.9.9 and 1.1.1.1 are the Quad9 and Cloudflare nameservers. If they don't appear, then you can add them by doing the following:


1. Run `sudo nano /etc/systemd/resolved.conf`

2. Inside that file, make sure it looks like the below:

```
[Resolve]
DNS=9.9.9.9
FallbackDNS=1.1.1.1
DNSStubListener=yes
```

3. Run `sudo systemctl restart systemd-resolved`

4. Run `sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf`

5. The 9.9.9.9 and 1.1.1.1 nameservers should then appear when you run `resolvectl status`

   



