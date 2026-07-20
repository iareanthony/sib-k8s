# Falco driver topology

Ubuntu 26.04's `7.0.0-27-generic` kernel requires GCC 15 and current
binutils to build Falco's 10.2.0 kernel module. The custom loader image in
`falco-driver-loader/` supplies that toolchain while retaining Falco's
official 0.44.1 loader entrypoint.

The main `sib-k8s-falco` DaemonSet selects nodes labeled
`falco-driver=kmod`. Five nodes currently use this stable kernel-module
path. `k8-worker03` has Secure Boot enabled and is labeled
`falco-driver=modern-ebpf`; it runs a standalone Falco 9.1.0 release using
`ops/falco-worker03-values.yaml` until a Machine Owner Key can be enrolled.

Apply the worker03 exception with:

```sh
helm upgrade --install falco-modern-worker03 falcosecurity/falco \
  --version 9.1.0 \
  --namespace security \
  --values ops/falco-worker03-values.yaml
```

After enrolling a trusted module-signing key and rebooting worker03, label
it `falco-driver=kmod` and uninstall the standalone exception release.
