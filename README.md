# KISS Linux for powerpc64le

This is a KISS Linux repository containing packages from the main KISS repo which have been patched to build on powerpc64le.

This is currently for testing purposes only.  While most packages will build without any trouble, there are still some which need some work.  Of these, Rust is the most significant.  It does not build because Rust do not provide stage0 tarballs for powerpc64le musl yet.  Because Rust doesn't build, that means no Firefox.  However, it is possible to build these packages on this platform - Void has done this previously.  Once the necessary changes have been made to the KISS build files, these will be added to this repository. 

## Using the repo

You should check this repo out to your machine then add it to your KISS_PATH such that it appears first, e.g.:

    export KISS_PATH=/home/myuser/kiss-ppc64le/repo:[your other repos]

This repo contains packages which also exist in the main KISS repo.  However if this repo is specified first in your KISS_PATH, this means that the powerpc version of the package will be built instead of the x86 version.

You can then install the package as normal with "kiss i ...".

## Installing KISS on powerpc64le

Please refer to the [KISS](https://getkiss.org/pages/install) webpage for general information about installing KISS.

### TalosII/Blackbird users

As per the instructions on the KISS webpage, boot your machine into another distro and bootstrap KISS from there.

For TalosII/Blackbird users, you can load the [Debian netboot](http://ftp.debian.org/debian/dists/buster/main/installer-ppc64el/current/images/netboot/debian-installer/ppc64el/) image directly into petitboot by pressing "n" on the boot menu.
This means you can install KISS on your machine without having to install another distro first.

There is a powerpc64le version of the KISS root tarball available [here](https://github.com/jdavies-dev/kiss-ppc64le-dist/blob/master/kiss-ppc64le.tar.xz) which you can use to perform the initial install as per the instructions on the KISS website.

This was built with -mcpu=power9, so you will need a Power9-based system to use this tarball.

### GRUB

You don't need GRUB, or any other additional bootloader to boot your KISS installation on the TalosII/Blackbird.  Petitboot parses the file /boot/grub/grub.cfg directly to look for kernels, so you just need to put something in here.  This is what I have - you can use this by replacing the root partition with your own:

    menuentry 'KISS Linux' {
            linux /boot/vmlinux root=/dev/nvme0n1p2 ro
    }

