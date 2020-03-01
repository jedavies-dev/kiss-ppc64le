# [KISS Linux](https://k1ss.org/) for powerpc64le

This is a repository containing an unofficial port of [KISS Linux](https://k1ss.org/) to the powerpc64le TalosII platform.

## Installing KISS on powerpc64le

Please refer to the main [KISS webpage](https://k1ss.org/install) for general information about installing KISS.
Once you have installed the tarball to your machine, see the "Using this repo" and "GRUB" sections for ppc-specific instructions.

## TalosII/Blackbird users

You must boot your machine into another distro first and bootstrap KISS from there.

For TalosII/Blackbird users, you can load the [Debian netboot](http://ftp.debian.org/debian/dists/buster/main/installer-ppc64el/current/images/netboot/debian-installer/ppc64el/) image directly into petitboot by pressing "n" on the boot menu when you start your machine. From here you can install KISS by switching to another terminal (e.g. using Alt-F2), then using wget or curl to obtain the [tarball](https://github.com/jedavies-dev/kiss-ppc64le/releases/download/0.1/kiss-chroot.tar.xz) and following the [install instructions](https://getkiss.org/pages/install).

There is a powerpc64le version of the KISS root tarball available [here](https://github.com/jedavies-dev/kiss-ppc64le/releases/download/0.1/kiss-chroot.tar.xz) which you can use to perform the initial install.

This was built with -mcpu=power9, so you will need a Power9-based system to use this tarball


## Using this repo

Once you've extracted the tarball onto your machine, you should chroot into that location and check this GitHub repo out to your machine then add it to your KISS_PATH such that it appears first, e.g.:

    git clone https://github.com/jedavies-dev/kiss-ppc64le.git
    export KISS_PATH=/home/myuser/kiss-ppc64le/repo:/home/myuser/kiss-ppc64le/community:[your other repos]

This repo contains packages which also exist in the main KISS repos.  However if this repo is specified first in your KISS_PATH, this means that the powerpc version of the package will be built instead of the x86 version.

Once you have set KISS_PATH can then build packages as normal with "kiss b ...".


## Kernel modules

[Load the](https://k1ss.org/wiki/Load-a-module-at-boot) ```evdev``` kernel module on boot to have keyboard input support under xorg.  See [this](https://k1ss.org/wiki/Replacing-eudev) page for alternatives to eudev.

Xorg tested with amdgpu driver on a rx580.


## GRUB

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
baselayout | OK
binutils | Patched (specify build type)
bison | OK
busybox | OK
bzip2 | OK
curl | OK
dhcpcd | OK
e2fsprogs | OK
eudev | OK
flex | OK
gcc | OK. Patched (specify ppc build)
git | OK
grub | Not required
gzip | OK
kiss | OK
kiss-utils | OK
libelf | OK. Patched (specify build type)
libnl | OK
libressl | OK
linux-headers | OK
m4 | OK
make | OK
mandoc | OK
musl | OK. Patched (fix location of ldd)
perl | OK
pkgconf | OK
rsync | OK. Patched (specify build type)
util-linux | OK
wpa_supplicant | OK
xz | OK
zlib | OK

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

## community
Package | Status
------------ | ------------
abduco | OK
aria2 | OK
bash | OK
bdftopcf | OK
berry | OK
bim | OK
bspwm | OK
btrfs-progs | OK
cmus | OK
conky | OK
cyrus-sasl | OK
dmenu | OK
dwm | OK
emacs | OK
fd | OK
feh | OK
fff | OK
file | OK
girara | OK
gnutls | OK
go | OK
haserl | OK
htop | OK
i3-gaps | OK
imlib2 | OK
joe | OK
kakoune | OK
lemonbar | OK
liberation-fonts-ttf | OK
libev | OK
libevent | OK
libexif | OK. Patched (specify build type)
libgcrypt | OK
libgpg-error | OK
libmad | OK. Patched (specify build type)
libxkbcommon | OK
links2 | OK
lua | OK
luajit | Fail: Unsupported on ppc
lynx | OK
lzo | OK
mc | OK
mini_httpd | OK
mutt | OK
nano | OK
ncdu | OK
ne | OK
neofetch | OK
neovim | Fail: Build fails.
nettle | OK
nmap | OK. Patched (specify build type)
openbox | OK. Patched (specify build type)
os-prober | OK
pandoc-bin | OK
pcre | OK
pfetch | OK
poppler-glib | OK
ripgrep | OK
ruby | OK
rxvt-unicode | OK
sdl | OK. Patched (specify build type)
sdl2 | OK
setroot | OK
shellcheck-bin | OK
slock | OK
spotifyd | OK
sxhkd | OK
sxiv | OK
terminus-font | OK
tig | OK
tmux | OK
tree | OK
unifont | OK
weechat | OK
xcb-util-xrm | OK
xclip | OK
xcompmgr | OK
xorriso | OK. Patched (specify build type)
xsel | OK
yajl | OK
zathura | OK
zathura-pdf-poppler | OK
zsh | OK
zstd | OK

