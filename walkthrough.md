---
title: Setup Guide 
has_children: false
nav_order: 6
---

# Setup Guide 

---

## Introduction

For those who have never used a window manager without a desktop environment like
KDE or GNOME, setting up `berry` might seem daunting at first.
This is a short guide to walkthrough setting up `berry` from scratch.

### Step 1: Install the necessary dependencies

Before we can get started we should install the necessary dependencies.
The Installation tab has more detailed information about how to install `berry`,
so I'll direct you there for this step.
Regardless of whether or not you build from source,
you still may find it useful to clone the source code locally so you have access
to some of the default configuration files.

Next, you need to install some sort of hotkey daemon such as `sxhkd`.
On it's own, `berry` does not handle keyboard input.
This means that we need a program that runs constantly in the background
that will listen for the appropriate keystrokes and convert them
into commands that `berryc` will execute (more on this architecture later).
Which program you choose is up to you, but for the rest of this article I'll assume
you're using `sxhkd`.
You can build the program from it's source `[here](https://github.com/baskerville/sxhkd)`,
or install it via a package manager if your system allows it.

Technically speaking, this is all the necessary software you need to run `berry`.
However, there are some quality of life programs that I recommend.
`berry` is a window manager, nothing more.
This means if you want something like a system bar or doc you'll have to install
and run those separately.
Personally I recommend [lemonbar](https://github.com/LemonBoy/bar).
However, it can be a bit involved to get a nice bar running, so you might also check out
[polybar](https://github.com/polybar/polybar).

Another type of program you might find useful is a launcher.
This allows you to start programs without running them from the command line.
Personally I recommend and use [dmenu](https://tools.suckless.org/dmenu/),
but a lot of people really enjoy [rofi](https://github.com/davatorium/rofi).

You should also probably have some type of terminal.
I use [urxvt](http://software.schmorp.de/pkg/rxvt-unicode.html),
but there are a million options out there.


### Step 2: Configure sxhkd and berry

Before we start our programs we should setup some configuration that works with our system.
If you've cloned the `berry` repository, you'll find two files in the `examples` directory.
`autostart` is the file that `berry` will try to run upon launch - this is just a shell script
that runs `berryc` commands (and anything else you want).
You'll also find an `sxhkdrc` file which maps keystrokes to commands that are run - this will
be useful for moving windows around and launching applications like our terminal
or `dmenu`.

You should create a `berry` directory inside of your `.config` directory and copy
these two files there.
```bash
mkdir -p ~/.config
mkdir -p ~/.config/berry
cd your-local-berry-directory
cp examples/* ~/.config/berry/
```
Technically speaking you could keep these configuration files anywhere,
but this is a very sane place to keep them.

Once these are copied you should edit them to fit your needs.
The default `autostart` file shouldn't need any changing (but feel free to change it if you want!
It just does things like set the active colors and border widths).
You should, however, edit the `sxhkdrc` file and make sure you know the key bindings
and that the relevant applications launched are correct.
For example, a good sanity check is to make sure `Super + Enter` is set to run your favorite
terminal emulator.

### Step 3: Starting berry and sxhkd

Once our programs are configured we must start them.
There are two primary paths here - using a display manager like `lightdm`
or using `xinit` and launching directly from the `tty`.
Personally I find it a lot easier to use `xinit`, but I'll cover both options here to be thorough.

#### Step 3a: Using xinit

This is the appropriate option if you aren't currently using a display manager.
A display manager is something like `lightdm` - when you turn on your computer you launch
into a pretty graphical interface which lets you login and select a desktop environment.
However, if you've done a minimal install from a distro like Arch or Gentoo, this won't
be included.
You'll need to install the necessary packages for display drivers and the X11 server.
For Arch Linux users I recommend reading the [Xorg](https://wiki.archlinux.org/index.php/xorg)
page on the wiki (this will probably be useful to everyone in some ways, however).

Once this is done you'll want to create a file called `.xinitrc` in your home directory.
This is a shell script that will start both `berry` and `sxhkd`.
This can be very minimal - all you really need to get running are the following lines:
```bash
#!/bin/bash
# 
# ~/.xinitrc

sxhkd -c $HOME/.config/berry/sxhkdrc &
exec berry
```
This will start `sxhkd` in the background (don't forget the `&`!)
and then start `berry`.
Note that since our `sxhkdrc` is not in the default directory we must specify explicitly
where it comes from.
`berry` also has a `-c` flag if you want to use a different `autostart` file.

Now, you should be able to start `berry` simply by typing `startx` from the `tty`.

#### Step 3b: Using a display manager

If you're coming from a desktop environment like GNOME or KDE you likely already have a
display manager installed.
`berry` can be launched from a display manager.
Creating a desktop entry will vary depending on which display manager you used, but for something
like `lightdm` would create the following file `berry.desktop` in `/usr/share/xsessions`

```ini
[Desktop Entry]
Encoding=UTF-8
Name=berry
Comment=berry - a small window manager
Exec=berry
Type=XSession
```

Once this is done you'll still need to start `sxhkd` at startup.
An easy way to do this is start `sxhkd` the same way we would for `xinit` but instead place
the startup command in `~/.xprofile` like so
```
#!/bin/bash
#
# ~/.xprofile

sxhkd -c $HOME/.config/berry/sxhkdrc &
```
Note we don't start `berry` here since the display manager is handling that, we just need to
start `sxhkd`.

You should be able to logout and now select `berry` to launch from your display manager.

### Step 4: Use berry

And that's it!
After following `3a` or `3b` you should have a minimal working `berry` installation.
However, the world is your oyster when it comes to managing windows with `berry`.

The way `berry` works is there is a small command line client called `berryc` which
allows you to interact with your window manager.
Open up a terminal and type something like
```
berryc window_move 10 10
```
And you'll see your active window move by 10 pixels in the x direction and 10 pixels in the y direction.
`berry` has a list of all possible commands on the man pages (i.e. `man berryc`).
You should write shell scripts to create more complex behavior than `berry` provides by default
(if you want to of course).
You can change the look of window decorations and title bars using `berryc` as well.

Another thing you might find useful are properties managed by the `x11` server that tell us about
`berry`'s internal state.
We can view these properties using a tool like `xprop`.

The following command will give you the id's of all windows managed by `berry`
```
xprop -root | grep -E "^_NET_CLIENT_LIST"
```
You can inspect these windows further by looking at the `BERRY_WINDOW_STATUS` property on one of
these windows, something like
```
xprop -id 0xXXXXXX BERRY_WINDOW_STATUS
```
where `0xXXXXXX` is on the id's from the previous command.
This will tell you information like the coordinates of a window and what desktop it's on, etc.

That should be enough to get you on your journey!
