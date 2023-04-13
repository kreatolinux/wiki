# How to build an rootfs
This tutorial will teach you how to build an rootfs.

# Dependencies
* Docker/podman and docker/podman-compose
* Nim with Nimble
* All of this on a glibc system (for now).
* Git

# Steps

## Downloading the source tree
You can clone the source code with `git clone https://github.com/kreatolinux/src`.
If you want, you can also use an stable release off GitHub Releases.

## Compiling kreastrap
Download dependencies by running `nimble install --depsOnly`.
Then run `nimble kreastrap` to build. The binary will be on `src/kreastrap/kreastrap` but **DO NOT** run this by yourself since it will break your system.


## Running kreastrap
To run kreastrap, you just do `docker compose up build-rootfs`. Change `docker compose` with `podman-compose` if you are using podman-compose.

Once finished, your rootfs will be available at `./out`. It builds builder-rootfs by default [(See what build types are)](../installation.md#choosing-the-right-tarball)
