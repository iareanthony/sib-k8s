# Falco driver topology

Ubuntu 26.04's `7.0.0-27-generic` kernel requires GCC 15 and current
binutils to build Falco's 10.2.0 kernel module. The custom loader image in
`falco-driver-loader/` supplies that toolchain while retaining Falco's
official 0.44.1 loader entrypoint.

The `sib-k8s-falco` DaemonSet selects nodes labeled
`falco-driver=kmod`. All six cluster nodes use this stable kernel-module
path. Secure Boot must remain disabled on these nodes unless the locally
compiled Falco module is signed with a key trusted by the firmware.
