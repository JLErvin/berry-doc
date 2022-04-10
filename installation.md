---
title: Installation
has_children: false
nav_order: 2
---

# Installation

## Build from source

`berry` has two main dependencies: The `XLib` and `Xft` headers.
On Debian based distributions, these can be installed via the following commands:

```bash
sudo apt-get install libx11-dev
sudo apt-get install libxft-dev
sudo apt-get install libxinerama-dev
```

Next, clone and make the respository.

```bash
git clone https://github.com/JLErvin/berry
cd berry
make
sudo make install
```
Copy the sample configuration files (assuming you are in the `berry` directory)

```bash
mkdir $HOME/.config/berry
cp examples/sxhkdrc $HOME/.config/berry/sxhkdrc
cp examples/autostart $HOME/.config/berry/autostart
```

## Using a package manager

Some operating systems already provide binaries for `berry`, for everyone else
please [read the instructions to build `berry` from source](#build-from-source).

### Arch Linux

```bash
yay -S berry-git
```

### Debian

Grab `.deb` from [barnumbirr/berry-debian](https://github.com/barnumbirr/berry-debian/releases), then

```bash
dpkg -i berry_<version>_amd64_<debian_version>.deb
```

### GNU Guix

`berry` is available from Guix R' Us [channel](https://guix.gnu.org/manual/en/html_node/Channels.html) provided by [WhereIsEveryone](https://whereis.みんな/)

Once [subscribed](https://git.sr.ht/~whereiseveryone/guixrus#subscribing), run the following command:

```bash
guix install berry
```

[Substitutes](https://guix.gnu.org/manual/en/html_node/Substitutes.html) are available from [bags.whereis.みんな](https://bags.whereis.みんな/)

### FreeBSD

```sh
pkg install berry
```

### Kiss

```bash
kiss b berry && kiss i berry
```

### Void Linux

```bash
sudo xbps-install -S berry
```

## Start berry using a display manager

If you are using a display manager, create a file called `berry.desktop` in `/usr/share/xsessions`
with the following contents:

```ini
[Desktop Entry]
Encoding=UTF-8
Name=berry
Comment=berry - a small window manager
Exec=berry
Type=XSession
```
