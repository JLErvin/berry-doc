---
title: Installation
has_children: false
nav_order: 2
---

# Installation

## Build from source

`berry` has two main dependencies: The `XLib` and `Xft` headers.
On debian based distributions, these can be installed via the following commands:

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

## From a package manger

If you are using `void` or `arch` linux then `berry` is available via your package manager.

On `arch`, install by running:
```
yay -S berry-git
```

On `void`, install by running:
```
sudo xbps-install -S berry
```

On `KISS`, install by running:
```
kiss b berry && kiss i berry
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
