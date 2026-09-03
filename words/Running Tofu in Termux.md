
## Tofu in Termux fails to resolve providers during init

The core of the issue is that Termux is not FHS compliant:
wiki.termux.com/wiki/Differences_from_Linux

https://stackoverflow.com/questions/38959067/dns-lookup-issue-when-running-my-go-app-in-termux

The following issue is resolved by installing proot and running `termux-chroot`:

```
Initializing provider plugins...
- Reusing previous version of cloudflare/cloudflare from the dependency lock file
╷
│ Error: Failed to resolve provider packages
│
│ Could not resolve provider cloudflare/cloudflare: could not connect to registry.opentofu.org: failed to request discovery document: Get
│ "https://registry.opentofu.org/.well-known/terraform.json": dial tcp: lookup registry.opentofu.org on [::1]:53: read udp
│ [::1]:42163->[::1]:53: read: connection refused
╵
```

Certificate fetching also fails because of searching a nonexistent location, it searches `/etc/ssl` instead of `/etc/tls` which is what termux is using:
https://stackoverflow.com/questions/40051213/where-is-golang-picking-up-root-cas-from
https://go.dev/src/crypto/x509/root_linux.go

So you need to copy or symlink those files over: `ln -s /etc/tls /etc/ssl`

