# KISS Linux for powerpc64le

This is a KISS Linux repository containing packages from the main KISS repos which have been patched to build on powerpc64le.

See tables below for package build status.  Currently testing the community package set.

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

Package | Status
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

## xorg

Package | Status
------------ | ------------
cairo | OK
fontconfig | OK
freetype-harfbuzz | OK
gdk-pixbuf | OK
gtk+2 | OK
gtk+3 | OK
hicolor-icon-theme | OK
libICE | OK
libSM | OK
libX11 | OK
libXScrnSaver | OK
libXau | OK
libXcomposite | OK
libXcursor | OK
libXdamage | OK
libXext | OK
libXfixes | OK
libXfont2 | OK
libXft | OK
libXi | OK
libXinerama | OK
libXmu | OK
libXrandr | OK
libXrender | OK
libXt | OK
libXxf86vm | OK
libdrm | OK
libepoxy | OK
libevdev | OK
libfontenc | OK
libinput | OK
libpciaccess | OK
libxcb | OK
libxkbfile | OK
libxshmfence | OK
mesa | OK. Patched (modify config flags)
mtdev | OK. Patched (specify build type)
pango | OK
pixman | OK
python-mako | OK
setxkbmap | OK
sowm | OK
st | OK
xbitmaps | OK
xcb-proto | OK
xcb-util | OK
xcb-util-cursor | OK
xcb-util-image | OK
xcb-util-keysyms | OK
xcb-util-renderutil | OK
xcb-util-wm | OK
xf86-input-libinput | OK
xf86-video-amdgpu | OK
xf86-video-ati | Not tested
xf86-video-intel | Not tested
xf86-video-nouveau | Not tested
xf86-video-vesa | Not tested
xinit | OK
xinput | OK
xkbcomp | OK
xkeyboard-config | OK
xorg-server | OK
xorg-util-macros | OK
xorgproto | OK
xprop | OK
xrandr | OK
xrdb | OK
xset | OK
xsetroot | OK
xtrans | OK

## extra
Package | Status
------------ | ------------
alsa-lib | OK
alsa-utils | OK
atk | OK
autoconf | OK
automake | OK
cbindgen | OK
ccache | OK
clang | OK
cmake | OK
cryptsetup | OK
efibootmgr | Not required
efivar | Not required
expat | OK
ffmpeg | OK
firefox | OK. Patched (mozconfig and build script)
fribidi | OK
giflib | OK
glib | OK
gnupg1 | OK
gperf | OK
json-c | OK
lame | OK
libaio | OK
libass | OK
libffi | OK
libjpeg-turbo | OK
libogg | OK
libpng | OK
libtheora | OK. Patched (specify build type)
libtool | OK
libvorbis | OK
libvpx | OK
libwebp | OK
libxml2 | OK
llvm | OK
lvm2 | OK
meson | OK
mpv | OK
nasm | OK
ncurses | OK
nodejs | OK
openssh | OK
opus | OK
popt | OK. Patched (specify build type)
python | OK
python2 | OK
rust | OK. Patched (use external bootstrap)
samurai | OK
shared-mime-info | OK
sqlite | OK
sudo | OK
tiff | OK
tzdata | OK
vim | OK
x264 | OK
x265 | OK. Patched (added ppc-specific optimizations)
xvidcore | OK
yasm | OK. Patched (specify build type)
zip | OK

## testing
Package | Status
------------ | ------------
qt5 | OK
