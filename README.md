

# [KISS Linux](https://k1ss.org/) for powerpc64le

This is a repository containing an unofficial port of [KISS Linux](https://k1ss.org/) for powerpc64le.

This was built with -mcpu=powerpc64le so should be compatible with at least power8 and power9 cpus, though this has only been tested on power9.

## Installing KISS on powerpc64le

Please refer to the main [KISS webpage](https://k1ss.org/install) for general information about installing KISS.
Once you have installed the tarball to your machine, see the "Using this repo" and "GRUB" sections for ppc-specific instructions.

## TalosII/Blackbird users

You must boot your machine into another distro first and bootstrap KISS from there.

For TalosII/Blackbird users, you can load the [Debian netboot](http://ftp.debian.org/debian/dists/buster/main/installer-ppc64el/current/images/netboot/debian-installer/ppc64el/) image directly into petitboot by pressing "n" on the boot menu when you start your machine. From here you can install KISS by switching to another terminal (e.g. using Alt-F2), then using wget or curl to obtain the [tarball](https://github.com/jedavies-dev/kiss-ppc64le/releases/download/0.1.6/kiss-chroot-powerpc64le.tar.xz) and following the [install instructions](https://k1ss.org/install).

There is a powerpc64le version of the KISS root tarball available [here](https://github.com/jedavies-dev/kiss-ppc64le/releases/download/0.1.6/kiss-chroot-powerpc64le.tar.xz) which you can use to perform the initial install.

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
Package | Status | Comment
------------ | ------------ | ------------
acpid | :heavy_check_mark:
alsa-lib | :heavy_check_mark:
alsa-utils | :heavy_check_mark:
atk | :heavy_check_mark:
cairo | :heavy_check_mark:
cbindgen | :heavy_check_mark:
ccache | :heavy_check_mark:
clang | :heavy_check_mark:
cmake | :heavy_check_mark:
dhcpcd | :heavy_check_mark:
dosfstools | :heavy_check_mark:
e2fsprogs | :heavy_check_mark:
efibootmgr | :heavy_check_mark:
efivar | :heavy_check_mark:
eiwd | :heavy_check_mark:
eudev | :heavy_check_mark:
expat | :heavy_check_mark:
ffmpeg | :heavy_check_mark:
firefox | :heavy_check_mark:
firefox-bin | :heavy_check_mark:
firefox-privacy | :heavy_check_mark:
fontconfig | :heavy_check_mark:
freetype-harfbuzz | :heavy_check_mark:
fribidi | :heavy_check_mark:
gdk-pixbuf | :heavy_check_mark:
giflib | :heavy_check_mark:
glib | :heavy_check_mark:
gnupg1 | :heavy_check_mark:
gperf | :heavy_check_mark:
gtk+2 | :heavy_check_mark:
gtk+3 | :heavy_check_mark:
hicolor-icon-theme | :heavy_check_mark:
intel-vaapi-driver | :white_check_mark: | Fails  to build
lame | :heavy_check_mark:
libass | :heavy_check_mark:
libdrm | :heavy_check_mark:
libelf | :heavy_check_mark:
libepoxy | :heavy_check_mark:
liberation-fonts | :heavy_check_mark:
libevdev | :heavy_check_mark:
libffi | :heavy_check_mark:
libinput | :heavy_check_mark:
libjpeg-turbo | :heavy_check_mark:
libogg | :heavy_check_mark:
libpng | :heavy_check_mark:
libtheora | :heavy_check_mark:
libva | :heavy_check_mark:
libva-utils | :heavy_check_mark:
libvorbis | :heavy_check_mark:
libvpx | :heavy_check_mark:
libwebp | :heavy_check_mark:
libxml2 | :heavy_check_mark:
llvm | :heavy_check_mark:
mandoc | :heavy_check_mark:
mesa | :heavy_check_mark:
meson | :heavy_check_mark:
mpv | :heavy_check_mark:
mtdev | :heavy_check_mark:
nasm | :heavy_check_mark:
ncurses | :heavy_check_mark:
nodejs | :heavy_check_mark:
opendoas | :heavy_check_mark:
openresolv | :heavy_check_mark:
openssh | :heavy_check_mark:
opus | :heavy_check_mark:
pango | :heavy_check_mark:
perl | :heavy_check_mark:
python | :heavy_check_mark:
python2 | :heavy_check_mark:
rust | :heavy_check_mark:
samurai | :heavy_check_mark:
sqlite | :heavy_check_mark:
sudo | :heavy_check_mark:
tiff | :heavy_check_mark:
tzdata | :heavy_check_mark:
util-linux | :heavy_check_mark:
vim | :heavy_check_mark:
wpa_supplicant | :heavy_check_mark:
x264 | :heavy_check_mark:
x265 | :heavy_check_mark:
xvidcore | :heavy_check_mark:
zip | :heavy_check_mark:
zstd | :heavy_check_mark:

## community
Package | Status | Comment
------------ | ------------ | ------------
2bwm | :heavy_check_mark:
9base | :heavy_check_mark:
aerc | :heavy_check_mark:
aria2 | :heavy_check_mark:
autoconf | :heavy_check_mark:
automake | :heavy_check_mark:
bash | :heavy_check_mark:
bc | :white_check_mark: | Fails to build
bdftopcf | :heavy_check_mark:
berry | :heavy_check_mark:
bim | :heavy_check_mark:
bkeymaps | :heavy_check_mark:
boost | :heavy_check_mark:
bspwm | :heavy_check_mark:
btpd | :heavy_check_mark:
cfm | :heavy_check_mark:
cmus | :heavy_check_mark:
conky | :heavy_check_mark:
coreutils | :heavy_check_mark:
cryptsetup | :heavy_check_mark:
custard | :heavy_check_mark:
cyrus-sasl | :heavy_check_mark:
cython | :heavy_check_mark:
dash | :heavy_check_mark:
diffutils | :heavy_check_mark:
discount | :heavy_check_mark:
dmenu | :heavy_check_mark:
dosbox | :heavy_check_mark:
dwm | :heavy_check_mark:
ed | :white_check_mark: | Fails to build, bad tar file
emacs | :white_check_mark: | Fails to build
emacs-git | :white_check_mark: | Fails to build
emacs-nox | :heavy_check_mark:
ethtool | :heavy_check_mark:
exa | :heavy_check_mark: | OK, but downloads Rust crates
expect | :heavy_check_mark: | Patched, added to ppc repo
extra-cmake-modules | :heavy_check_mark:
falkon | :white_check_mark: | Fails to build
fd | :heavy_check_mark:
fdm | :heavy_check_mark:
feh | :heavy_check_mark:
fff | :heavy_check_mark:
file | :heavy_check_mark:
findutils | :heavy_check_mark:
flac | :heavy_check_mark:
flashrom | :white_check_mark: | Fails to build
font-awesome | :heavy_check_mark:
freeglut | :heavy_check_mark:
gauche | :heavy_check_mark:
gawk | :heavy_check_mark:
gdb | :heavy_check_mark:
girara | :heavy_check_mark:
glib-networking | :heavy_check_mark:
glu | :heavy_check_mark:
gmp | :heavy_check_mark:
gnu-netcat | :heavy_check_mark: | Patched, added to ppc repo
gnugrep | :heavy_check_mark:
gnupg2 | :heavy_check_mark:
gnutls | :heavy_check_mark:
go | :heavy_check_mark: | Recently updated
groff | :heavy_check_mark:
gtar | :heavy_check_mark:
hack | :heavy_check_mark:
harfbuzz-icu | :heavy_check_mark:
hexyl | :heavy_check_mark: | OK, but downloads Rust crates
hsetroot | :heavy_check_mark:
htop | :heavy_check_mark:
hyperfine | :heavy_check_mark: | OK, but downloads Rust crates
i3 | :white_check_mark: | Fails to build
i3-gaps | :white_check_mark: | Fails to build
icu | :heavy_check_mark:
imagemagick | :heavy_check_mark:
imlib2 | :heavy_check_mark:
intel-media-driver | :white_check_mark: | Fails to build
iproute2 | :heavy_check_mark:
iptables | :heavy_check_mark:
iputils | :heavy_check_mark:
irssi | :heavy_check_mark:
isync | :heavy_check_mark:
jbig2dec | :heavy_check_mark:
jq | :heavy_check_mark:
json-c | :heavy_check_mark:
kakoune | :heavy_check_mark:
keyutils | :heavy_check_mark:
kmod | :heavy_check_mark:
lazygit | :heavy_check_mark:
lcms2 | :heavy_check_mark:
ledger | :white_check_mark: | MPFR fails to download
lemonbar | :heavy_check_mark:
less | :heavy_check_mark:
libXslt | :heavy_check_mark:
libaio | :heavy_check_mark:
libarchive | :heavy_check_mark:
libassuan | :heavy_check_mark:
libcap | :heavy_check_mark:
libconfig | :heavy_check_mark:
libev | :heavy_check_mark:
libevent | :heavy_check_mark:
libexif | :heavy_check_mark:
libgcrypt | :heavy_check_mark:
libgpg-error | :heavy_check_mark:
libksba | :heavy_check_mark:
libmad | :heavy_check_mark:
libmpdclient | :heavy_check_mark:
libmupdf | :heavy_check_mark:
libnl | :heavy_check_mark:
libpsl | :heavy_check_mark:
libsodium | :heavy_check_mark:
libsoup | :heavy_check_mark:
libtool | :heavy_check_mark:
libtorrent | :heavy_check_mark:
libxaw3d | :heavy_check_mark:
links2 | :heavy_check_mark:
loksh | :heavy_check_mark:
lua | :heavy_check_mark:
luajit | :white_check_mark: | Fails to build
lux | :heavy_check_mark:
lvm2 | :heavy_check_mark:
lynx | :heavy_check_mark:
lzip | :heavy_check_mark:
lzo | :heavy_check_mark:
man-pages | :heavy_check_mark:
man-pages-posix | :heavy_check_mark:
mawk | :heavy_check_mark:
mg | :heavy_check_mark:
minisign | :heavy_check_mark:
mksh | :heavy_check_mark:
mpc | :heavy_check_mark:
mpd | :heavy_check_mark:
mpfr | :heavy_check_mark:
msmtp | :heavy_check_mark:
mutt | :heavy_check_mark:
nano | :heavy_check_mark:
nawk-git | :heavy_check_mark:
ncdu | :heavy_check_mark:
neatvi | :heavy_check_mark:
neofetch | :heavy_check_mark:
neovim | :white_check_mark: | Fails to build
netsurf | :heavy_check_mark:
nettle | :heavy_check_mark:
nmap | :heavy_check_mark:
nnn | :heavy_check_mark:
npth | :heavy_check_mark:
nss | :heavy_check_mark:
ntfs-3g | :heavy_check_mark:
oath-toolkit | :heavy_check_mark:
oed | :heavy_check_mark:
openbox | :heavy_check_mark:
openjpeg2 | :heavy_check_mark:
openvpn | :heavy_check_mark:
opusfile | :heavy_check_mark:
os-prober | :heavy_check_mark:
osh | :heavy_check_mark:
pandoc-bin | :heavy_check_mark:
parted | :heavy_check_mark:
pash | :heavy_check_mark:
patch | :heavy_check_mark:
pciutils | :heavy_check_mark:
pcre | :heavy_check_mark:
perl-html-parser | :heavy_check_mark:
perl-html-tagset | :heavy_check_mark:
pfetch | :heavy_check_mark:
picom | :heavy_check_mark:
pinentry | :heavy_check_mark:
pinentry-dmenu | :heavy_check_mark:
pkcs11-helper | :heavy_check_mark:
poppler | :heavy_check_mark:
popt | :heavy_check_mark:
procps-ng | :heavy_check_mark:
qemu | :heavy_check_mark:
qrencode | :heavy_check_mark: | Patched, added to ppc repo
qt5 | :heavy_check_mark:
qt5-declarative | :heavy_check_mark:
qt5-svg | :heavy_check_mark:
qt5-webchannel | :heavy_check_mark:
qt5-webengine | :white_check_mark: | Fails to build
qt5-x11extras | :heavy_check_mark:
radare2 | :heavy_check_mark:
rage | :white_check_mark: | OK, Downloads Rust crates
readline | :heavy_check_mark:
ripgrep | :heavy_check_mark: | OK, Downloads Rust crates
rtorrent | :heavy_check_mark:
ruby | :heavy_check_mark:
runit | :heavy_check_mark:
rxvt-unicode | :heavy_check_mark:
sbase | :heavy_check_mark:
sc | :heavy_check_mark:
sc-im | :heavy_check_mark:
screen | :heavy_check_mark:
sdl | :heavy_check_mark:
sdl2 | :heavy_check_mark:
sed | :heavy_check_mark:
setroot | :heavy_check_mark:
sfeed | :heavy_check_mark:
shadow | :heavy_check_mark:
shellcheck-bin | :heavy_check_mark:
sic-git | :heavy_check_mark:
sinit | :heavy_check_mark:
slmenu | :heavy_check_mark:
slock | :heavy_check_mark:
socat | :heavy_check_mark:
strace | :heavy_check_mark:
surfraw | :heavy_check_mark:
sxhkd | :heavy_check_mark:
sxiv | :heavy_check_mark:
syncthing | :heavy_check_mark:
sysmgr | :heavy_check_mark:
tabbed | :heavy_check_mark:
tcc | :white_check_mark: | Fails to build, “Unsupported CPU”
tcl | :heavy_check_mark:
tdb | :heavy_check_mark:
terminus-font | :heavy_check_mark:
tk | :heavy_check_mark:
tmux | :heavy_check_mark:
tokei | :heavy_check_mark: | OK, Downloads Rust crates
tor | :heavy_check_mark:
transmission-daemon | :heavy_check_mark:
tree | :heavy_check_mark:
tty-clock | :heavy_check_mark:
ubase | :heavy_check_mark:
uemacs | :heavy_check_mark:
unifont | :heavy_check_mark:
urlview | :heavy_check_mark:
uthash | :heavy_check_mark:
vimb | :heavy_check_mark:
vimpc | :heavy_check_mark:
webkit2gtk | :heavy_check_mark:
weechat | :heavy_check_mark:
wget | :heavy_check_mark:
wmutils-core | :heavy_check_mark:
xbacklight | :heavy_check_mark:
xcb-util-xrm | :heavy_check_mark:
xclip | :heavy_check_mark:
xcompmgr | :heavy_check_mark:
xf86-input-mtrack | :heavy_check_mark:
xkb-switch | :heavy_check_mark:
xmlsec1 | :heavy_check_mark:
xmodmap | :heavy_check_mark:
xsel | :heavy_check_mark:
xtrlock | :heavy_check_mark:
xwallpaper | :heavy_check_mark:
yajl | :heavy_check_mark:
youtube-dl | :heavy_check_mark:
zathura | :heavy_check_mark:
zathura-pdf-mupdf | :heavy_check_mark:
zathura-pdf-poppler | :heavy_check_mark:

