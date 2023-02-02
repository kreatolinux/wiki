# nyaa3 Internals
Welcome! In this page you will find information as how nyaa3 works.

# What is nyaa3?
Nyaa3 is the rewrite of the package manager called [nyaa2](https://github.com/kreatolinux/nyaa2) in Nim. This has been done for many reasons, which i won't repeat here. Nyaa2 has more features in some areas, but is now **unsupported** and shouldn't be used.

# Layout of nyaa3
The layout of the project is really simple to understand.

* `nyaa.nimble` specifies the dependencies.
* `docker-compose.yml` is there for testing.
* `man` directory has the pandoc-generated manpages, which have their source files in `src/man`.

# The src directory
`src` directory has many projects, including (currently) purr for testing, nyaastrap for building packages and rootfs automatically, and nyaa itself. These projects are **seperate** and are only added because they include the nyaa3 functions.

## nyaastrap
`src/nyaastrap` has the source code of nyaastrap. Nyaastrap v3 is the newest rewite the Kreato Linux build tool. It is rewritten in Nim, so it can utilize nyaa's internal functions and have better error handling than nyaastrap v2. It allows you to build packages, and an rootfs. More features may come soon.

You can learn how to build an rootfs [through here](./how-to-rootfs.md).

## purr
`src/purr` has the source code of purr. Purr is an test utility, checking if things are still working the way they should.

Please note that both of these projects should be ran on an Docker container, which is why `docker-compose.yml` exists. **DO NOT** run these tols in your host machine, as it will probably break your host system and/or not work at all.

## nyaa
The main project, which includes an easy-to-use library to use for other projects. It resides mostly in `src/nyaa` and is neatly seperated onto seperate files.
`src/nyaa/modules` includes more internal functions such as the downloader, the config system, etc.
