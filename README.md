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



Package | Status | Comment
------------ | ------------ | ------------
baseinit | :heavy_check_mark:
baselayout | :heavy_check_mark:
binutils | :heavy_check_mark: | Patched (enable arch)
bison | :heavy_check_mark: | Patched build file (parallel build issue)
busybox | :heavy_check_mark:
bzip2 | :heavy_check_mark:
curl | :heavy_check_mark:
flex | :heavy_check_mark:
gcc | :heavy_check_mark: | Patched (enable arch)
git | :heavy_check_mark:
grub | :white_check_mark: | Not used
gzip | :heavy_check_mark:
kiss | :heavy_check_mark: | Patched 
libressl | :heavy_check_mark:
linux-headers | :heavy_check_mark:
m4 | :heavy_check_mark:
make | :heavy_check_mark:
musl | :heavy_check_mark: | Patched (Update ldd symlink location)
pkgconf | :heavy_check_mark:
rsync | :heavy_check_mark: | Patched (Update build target)
xz | :heavy_check_mark:
zlib | :heavy_check_mark:

## xorg

Package | Status | Comment
------------ | ------------ | ------------
libICE | :heavy_check_mark:
libSM | :heavy_check_mark:
libX11 | :heavy_check_mark:
libXScrnSaver | :heavy_check_mark:
libXau | :heavy_check_mark:
libXcomposite | :heavy_check_mark:
libXcursor | :heavy_check_mark:
libXdamage | :heavy_check_mark:
libXext | :heavy_check_mark:
libXfixes | :heavy_check_mark:
libXfont2 | :heavy_check_mark:
libXft | :heavy_check_mark:
libXi | :heavy_check_mark:
libXinerama | :heavy_check_mark:
libXmu | :heavy_check_mark:
libXrandr | :heavy_check_mark:
libXrender | :heavy_check_mark:
libXt | :heavy_check_mark:
libXtst | :heavy_check_mark:
libXxf86vm | :heavy_check_mark:
libfontenc | :heavy_check_mark:
libpciaccess | :heavy_check_mark:
libxcb | :heavy_check_mark:
libxkbcommon | :heavy_check_mark:
libxkbfile | :heavy_check_mark:
libxshmfence | :heavy_check_mark:
pixman | :heavy_check_mark:
setxkbmap | :heavy_check_mark:
sowm | :heavy_check_mark:
st | :heavy_check_mark:
xauth | :heavy_check_mark:
xbitmaps | :heavy_check_mark:
xcb-proto | :heavy_check_mark:
xcb-util | :heavy_check_mark:
xcb-util-cursor | :heavy_check_mark:
xcb-util-image | :heavy_check_mark:
xcb-util-keysyms | :heavy_check_mark:
xcb-util-renderutil | :heavy_check_mark:
xcb-util-wm | :heavy_check_mark:
xev | :heavy_check_mark:
xf86-input-libinput | :heavy_check_mark:
xf86-video-amdgpu | :heavy_check_mark:
xf86-video-ati | :heavy_check_mark:
xf86-video-intel | :white_check_mark:
xf86-video-nouveau | :heavy_check_mark:
xf86-video-vesa | :heavy_check_mark:
xinit | :heavy_check_mark:
xinput | :heavy_check_mark:
xkbcomp | :heavy_check_mark:
xkeyboard-config | :heavy_check_mark:
xorg-server | :heavy_check_mark:
xorg-util-macros | :heavy_check_mark:
xorgproto | :heavy_check_mark:
xprop | :heavy_check_mark:
xrandr | :heavy_check_mark:
xrdb | :heavy_check_mark:
xset | :heavy_check_mark:
xsetroot | :heavy_check_mark:
xtrans | :heavy_check_mark:


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

