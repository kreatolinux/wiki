# Installation

## Introduction 
This guide shows you how to install Kreato Linux. This is not a in-depth guide and never will be because;
1- It requires too much work
2- This distro is not for people that need in-depth guides.
It is assumed that you have a partition layout already setup.
It is assumed that you are using a UEFI system.
Kreato Linux doesn't have a live ISO image. It is assumed that you would start the installation from another Linux installation. 
If you do not have a working Linux install, we recommend [Arch Linux LiveISO](https://archlinux.org/download/) for installation.
This guide is **work-in-progress** and may not work. Please open a issue if so.

## Get rootfs tarball
First step should be to get the rootfs tarball. Kreato Linux installs through a rootfs (Like Gentoo). You can get the latest nightly through [Github Actions](https://github.com/kreatolinux/nyaa3/actions?query=is%3Asuccess).

### Choosing the right tarball
Kreato Linux is a modular distribution. There are two build types currently available.
* nocc-rootfs
* and builder-rootfs.

nocc-rootfs is completely built by GitHub Actions and as the name implies, doesnt have any compilers by default. You can use binaries to install any compilers, or dont build at all and use the system with just binaries.

builder-rootfs is also built by GitHub actions and comes with gcc.

More builds will be available soon.

### Extracting
Mount the partition you are gonna install it to `/mnt`.
Once downloaded, extract the zip file and you will get a tarball.
Extract the tarball using the command here;
`tar --same-owner -xvf kreato-linux-*.tar.gz -C /mnt`
Once extracted, we can move on to chrooting.

## Chrooting
Before chrooting, mount your EFI partition to `/boot`.
Run these commands to chroot.

```
mount -o bind /dev /mnt/dev
mount -t proc none /mnt/proc
mount -o bind /sys /mnt/sys
mount -o bind /tmp /mnt/tmp
chroot /mnt /bin/bash
. /etc/profile
```

And you should be in! 

## Installing base system packages

### Binary vs. Source
Kreato Linux offers 2 choices for installation.
* Source based (compiling software),
* And binary based (installing from binary repository).

Both choices have their own advantages.

#### Advantages and disadvantages of building packages
* Updates come faster.
* Has more customizability and optimization options.
* Building is slower than downloading a binary tarball.

#### Advantages and disadvantages of binary packages
* Updates are available with a lag. 
* Has less customizability.
* Doesn't require building packages, making it more suitable to older/less powerful systems.
* Is not currently stable, packages may not even exist on the mirror.

This installation guide will assume that you are gonna install binary packages (`nyaa install packagename`). If you want to build packages, please change `nyaa install` to `nyaa build` so it builds the packages instead of installing the binary.

Now we can continue with installing base system packages.

### Installing the init system
Kreato Linux includes multiple init systems. OpenRC, systemd and busybox init exist as a option.

* If you want busybox init, you can install `base-runit`: `nyaa install base-runit`
* If you want OpenRC: you can install `openrc`: `nyaa install openrc`

### Installing networking tools
`dhcpcd` is recommended. run `nyaa install dhcpcd` to install `dhcpcd`.
you should install `wpa_supplicant` aswell if you need Wi-Fi connectivity. run `nyaa install wpa_supplicant` to install it.

### Building the kernel
You can either build your own kernel or use Kreato Linux's kernel, that uses Arch Linux's kernel configuration.
It is recommended to build your own kernel, since it will be much more minimal and will compile faster.
You can run `nyaa install linux-arch` to install the prebuilt kernel.
As for building your own kernel, you can check out [This video](https://www.youtube.com/watch?v=NVWVHiLx1sU).

### Installing shadow
Installing `shadow` is recommended since a lot of software uses shadow.
Run `nyaa install shadow` to install `shadow`.
You can enable shadowed passwords by running `pwconv`, and enable shadowed group passwords by running `grpconv`.

### Installing the bootloader
Kreato Linux offers multiple bootloaders.
You can use Limine, Grub or if you have a kernel that has EFISTUB enabled (prebuilt kernel does have it enabled), you can use [efictl](https://github.com/kreatolinux/efictl/)

This guide will show Limine since it is the most tested option.
You can install Limine by running `nyaa install limine`.
Configuration is already explained greatly on [Arch Wiki](https://wiki.archlinux.org/title/Limine), so i wont repeat it here.

## Change the root password
You should change the root password by running this command;
`passwd root`
If you want to do so, you can also add additional users with `useradd`.

Now you should be able to boot Kreato Linux by itself.

## Setting up the locale
You can set up the locale by running these commands. Change `LOCALE=en_US` with your language (Example; `LOCALE=de_DE` for German)

```
LOCALE=en_US
mkdir -p /usr/lib/locale
localedef -i $LOCALE -c -f UTF-8 $LOCALE
echo "export LANG=$LOCALE" >> /etc/profile
```

## Installing a Window Manager
Kreato Linux only offers `sway` for now and will only support Wayland for now.
You can install sway by running `nyaa install sway`.
More Wayland window managers are coming soon.
You can also install foot, a terminal by running `nyaa install foot`
