# Установка пакетов в Ubuntu 20.04

```shell
sudo apt-get install build-essential libgtk3.0-dev libdbus-glib-1-dev autoconf2.13 \
yasm libegl1-mesa-dev libasound2-dev libxt-dev zlib1g-dev libssl-dev \
libsqlite3-dev libbz2-dev libpulse-dev libgconf2-dev libx11-xcb-dev \
zip python2.7 python-dbus mc tmux ncdu
```
# Получение кода
```shell
wget http://archive.palemoon.org/source/palemoon-29.4.4.source.tar.xz
```

# Распаковка архива кода
```bash
tar -xf palemoon-29.4.4.source.tar.xz
```
# Создать файл .mozconfig в директории кода
```bash
# Clear this if not a 64bit build
_BUILD_64=1

# Set GTK Version to 2 or 3
_GTK_VERSION=3

# Standard build options for Pale Moon
ac_add_options --enable-application=palemoon
ac_add_options --enable-optimize="-O2 -w"
ac_add_options --enable-default-toolkit=cairo-gtk$_GTK_VERSION
ac_add_options --enable-jemalloc
ac_add_options --enable-strip
ac_add_options --enable-devtools
ac_add_options --enable-av1
ac_add_options --disable-eme
ac_add_options --disable-webrtc
ac_add_options --disable-gamepad
ac_add_options --disable-tests
ac_add_options --disable-debug
ac_add_options --disable-necko-wifi
ac_add_options --disable-updater
ac_add_options --with-pthreads

# Please see https://www.palemoon.org/redist.shtml for restrictions when using the official branding.
ac_add_options --enable-official-branding
export MOZILLA_OFFICIAL=1

mk_add_options MOZ_MAKE_FLAGS="-j8"

# Processor architecture specific build options
if [ -n "$_BUILD_64" ]; then
  ac_add_options --x-libraries=/usr/lib64
else
  ac_add_options --x-libraries=/usr/lib
fi

export MOZ_PKG_SPECIAL=gtk$_GTK_VERSION
```
# Сборка
```bash
./mach build
```
# Сборка пакета
```
./mach package
```
Пакет будет находится по следующему адресу - ~/palemoon-source/obj-x86_64-pc-linux-gnu/dist/palemoon-{version}.linux-x86_64-gtk2.tar.xz