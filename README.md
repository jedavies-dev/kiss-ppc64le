

# [KISS Linux](https://k1ss.org/) for powerpc64le

This is a repository containing an unofficial port of [KISS Linux](https://k1ss.org/) for powerpc64le.

This was built with ``-mcpu=powerpc64le`` so should be compatible with at least power8 and power9 cpus, though this has only been tested on power9.

**Note 2020-12-21 The repo has been restructured to match the main KISS repo by not relying on /var/db/kiss/repo being in place**

## Installing KISS on powerpc64le

Please refer to the main [KISS webpage](https://k1ss.org/install) for general information about installing KISS.
Once you have installed the tarball to your machine, see the "Using this repo" and "GRUB" sections for ppc-specific instructions.

## TalosII/Blackbird users

You must boot your machine into another distro first and bootstrap KISS from there.

For TalosII/Blackbird users, you can load the [Debian netboot](http://ftp.debian.org/debian/dists/buster/main/installer-ppc64el/current/images/netboot/debian-installer/ppc64el/) image directly into petitboot by pressing "n" on the boot menu when you start your machine. From here you can install KISS by switching to another terminal (e.g. using Alt-F2), then using wget or curl to obtain the [tarball](https://github.com/jedavies-dev/kiss-ppc64le/releases/download/0.1.7/kiss-chroot-powerpc64le.tar.xz) and following the [install instructions](https://k1ss.org/install).

There is a powerpc64le version of the KISS root tarball available [here](https://github.com/jedavies-dev/kiss-ppc64le/releases/download/0.1.7/kiss-chroot-powerpc64le.tar.xz) which you can use to perform the initial install.

As on x86_64, it is recommended you rebuild the base packages with CFLAGS/CXXFLAGS appropriate for your system.  On a TalosII, you could use:
```
export CFLAGS="-mcpu=power9 -mtune=power9 -O3 -pipe"
export CXXFLAGS=$CFLAGS
```


## Using this repo

This repo is checked out to ``/var/db/kiss/kiss-ppc64le`` in the tarball.

Note that the KISS_PATH environment variable specifies the kiss-ppc64le repo before the generic KISS repos.  This means that packages in the kiss-ppc64le repo will override the generic packages where necessary.  The aim of this repo is to keep the number of packages being overridden to a minimum, only overriding the x86_64 packages where it does not build without intervention.

You can add other repositories to your KISS_PATH, for example [community](https://github.com/kisslinux/community), [games](https://github.com/sdsddsd1/kiss-games) or [wayland](https://github.com/sdsddsd1/mywayland).

## Kernel modules

Add a line to /etc/inittab, for example:

```
::once:/bin/modprobe evdev
::once:/bin/modprobe amdgpu
```

Xorg tested with amdgpu driver on a rx580.


## GRUB

You don't need GRUB or any other additional bootloader to boot your KISS installation on the TalosII/Blackbird.  Petitboot parses the file /boot/grub/grub.cfg directly to look for kernels. Therefore all you need is something appropriate in your /boot/grub/grub.cfg file.  You can use the below example, replacing the root partition with your own:

    menuentry 'KISS Linux' {
            linux /boot/vmlinux root=/dev/sda1 ro
    }

## Package build failues

PRs of Issues are welcome if you find a package that doesn't build.  Not supporting Rust or Firefox currently.
