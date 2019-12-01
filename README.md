# KISS Linux for powerpc64le

This is a KISS Linux repository containing packages from the main KISS repos which have been patched to build on powerpc64le.

All packages from core, xorg, extra and testing now build.  Currently working through community packages.

## Using the repo

You should check this repo out to your machine then add it to your KISS_PATH such that it appears first, e.g.:

    export KISS_PATH=/home/myuser/kiss-ppc64le/repo:/home/myuser/kiss-ppc64le/community:[your other repos]

This repo contains packages which also exist in the main KISS repos.  However if this repo is specified first in your KISS_PATH, this means that the powerpc version of the package will be built instead of the x86 version.

Once you have set KISS_PATH can then build packages as normal with "kiss b ...".

## Installing KISS on powerpc64le

Please refer to the [KISS](https://getkiss.org/pages/install) webpage for general information about installing KISS.

### TalosII/Blackbird users

As per the instructions on the KISS webpage, boot your machine into another distro and bootstrap KISS from there.

For TalosII/Blackbird users, you can load the [Debian netboot](http://ftp.debian.org/debian/dists/buster/main/installer-ppc64el/current/images/netboot/debian-installer/ppc64el/) image directly into petitboot by pressing "n" on the boot menu.
From here you can install KISS by switching to another terminal and following the [install instructions](https://getkiss.org/pages/install).

There is a powerpc64le version of the KISS root tarball available [here](https://github.com/jdavies-dev/kiss-ppc64le-dist/blob/master/kiss-ppc64le.tar.xz) which you can use to perform the initial install.

This was built with -mcpu=power9, so you will need a Power9-based system to use this tarball

### Kernel modules

Be sure to load evdev on boot to load keyboard input support.  Tested with amdgpu on a rx580: supported and works fine with xorg.

### GRUB

You don't need GRUB or any other additional bootloader to boot your KISS installation on the TalosII/Blackbird.  Petitboot parses the file /boot/grub/grub.cfg directly to look for kernels. Therefore all you need is something appropriate in your /boot/grub/grub.cfg file.  You can use the below example, replacing the root partition with your own:

    menuentry 'KISS Linux' {
            linux /boot/vmlinux root=/dev/sda1 ro
    }

## Repo Structure

Packages which override ones in core/ extra/ xorg/ and testing/ have symlinks to the corresponding files on your machine in /var/db/kiss/repo/, and are in the top level "repo" directory.
Packages which override ones in community/ contain a copy of the set of build files, and are in the top level "community" directory.

# Package build status
## core

Core: | Status
------------ | ------------
baselayout | <span style="color:green">OK</span>
binutils | <span style="color:green">Patched (specify build type)</span>
bison | <span style="color:green">OK</span>
busybox | <span style="color:green">OK</span>
bzip2 | <span style="color:green">OK</span>
curl | <span style="color:green">OK</span>
dhcpcd | <span style="color:green">OK</span>
e2fsprogs | <span style="color:green">OK</span>
eudev | <span style="color:green">OK</span>
flex | <span style="color:green">OK</span>
gcc | <span style="color:green">OK. Patched (specify ppc build)</span>
git | <span style="color:green">OK</span>
grub | <span style="color:yellow">Not required</span>
gzip | <span style="color:green">OK</span>
kiss | <span style="color:green">OK</span>
kiss-utils | <span style="color:green">OK</span>
libelf | <span style="color:green">OK. Patched (specify build type)</span>
libnl | <span style="color:green">OK</span>
libressl | <span style="color:green">OK</span>
linux-headers | <span style="color:green">OK</span>
m4 | <span style="color:green">OK</span>
make | <span style="color:green">OK</span>
mandoc | <span style="color:green">OK</span>
musl | <span style="color:green">OK. Patched (fix location of ldd)</span>
perl | <span style="color:green">OK</span>
pkgconf | <span style="color:green">OK</span>
rsync | <span style="color:green">OK. Patched (specify build type)</span>
util-linux | <span style="color:green">OK</span>
wpa_supplicant | <span style="color:green">OK</span>
xz | <span style="color:green">OK</span>
zlib | <span style="color:green">OK</span>
