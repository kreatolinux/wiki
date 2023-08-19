# Kreaiso
Kreaiso is Kreato Linux's image generator. It currently only works on images using systemd. 

# How it simply works
It works by untarring the rootfs tarball the user chooses and putting it into a SquashFS image. Then it packages a initramfs and a kernel and makes it an ISO using `grub2-mkrescue`.

Very simple, I know. Open for suggestions.

# Usage
Kreaiso is currently only usable through CI, but a docker-compose configuration is coming soon.
**DO NOT run kreaiso without a container**

# Roadmap
Next thing to do will be supporting non-systemd images, polishing the experience, etc.

This project is *very* new so bugs are expected.
