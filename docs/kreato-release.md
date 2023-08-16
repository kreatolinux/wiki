# kreato-release file
`kreato-release` is a release file on `/etc`. It is like `os-release` in functionality.

It allows any software to see how the Kreato Linux system is configured.

It uses [an ini-like format](https://nim-lang.org/docs/parsecfg.html), like kpkg/kreastrap configuration files. 

# Example

```ini
[General]
dateBuilt=2023-05-15
klinuxVersion=rolling
srcCommit=4691104

[Core]
libc=glibc
compiler=gcc
coreutils=busybox
tlsLibrary=openssl
init=jumpstart

[Extras]
extraPackages=nim llvm mesa
```

# Options

## General
* dateBuilt: Shows the date the system has been built. Follows `YYYY-MM-DD` format.
* klinuxVersion: Shows Kreato Linux version the system is meant to run. `rolling` by default.
* srcCommit: Shows Kreato Linux source tree commit the system has been built with. Does not include kpkg included in the system.

## Core/Extras
Core and Extras parts are almost exactly the same as kreastrap configuration files, look at kreastrap.conf(5) for information on those areas. 

Kreastrap will generate this file at the time the rootfs is built.
