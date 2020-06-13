+++
title = "Linux and Cisco Hardware"
date = "2020-06-13T06:31:44-04:00"
author = "Tom Konidas"
authorTwitter = "tomkonidas"
cover = "img/linux-catalyst.jpg"
tags = ["linux", "catalyst"]
keywords = ["linux", "screen", "gnu","catalyst", "switch","router"]
description = "Connecting to Cisco hardware consoles on Linux with GNU Screen."
showFullContent = false
draft = false
+++

> Connecting to Cisco hardware consoles on Linux with GNU Screen.

After a little bit of online googling, I came to a conclusion that there aren't many
tutorials that go about connecting to Cisco gear via COM port with Linux.
Most articles are using SSH/Telnet or through PuTTy on Windows.

So here I am making this easy to follow guide on how to do it.
This is more for me to reference when/if I forget how in the future.
I actually find it a lot easier this way rather than going to sketchy Chinese
websites to download specific drivers, then to put in the important settings such
as Parity, Baud Rate, etc...

My way; the Linux way, is the simplest IMHO.
All you need is 1 program and your off to the races.

**Note**: This also works for BSDs or any other \*NIX OS that is able to run GNU Screen... (I'm looking at you OSX🧐)

# Step 0: Prerequisites

## Cables and Adapters

If you have an older model, you will need to get a Console cable with a USB To RS232 Serial Converter Cable Adapter.
If you have something more "modern", you can connect straight via USB. This does not affect anything where going to discuss today.

## GNU Screen

What is [GNU Screen](https://www.gnu.org/software/screen/)?

> Screen is a full-screen window manager that multiplexes a physical terminal between several processes, typically interactive shells. Each virtual terminal provides the functions of the DEC VT100 terminal and, in addition, several control functions from the ANSI X3.64 (ISO 6429) and ISO 2022 standards (e.g., insert/delete line and support for multiple character sets). There is a scrollback history buffer for each virtual terminal and a copy-and-paste mechanism that allows the user to move text regions between windows. When screen is called, it creates a single window with a shell in it (or the specified command) and then gets out of your way so that you can use the program as you normally would. Then, at any time, you can create new (full-screen) windows with other programs in them (including more shells), kill the current window, view a list of the active windows, turn output logging on and off, copy text between windows, view the scrollback history, switch between windows, etc. All windows run their programs completely independent of each other. Programs continue to run when their window is currently not visible and even when the whole screen session is detached from the users terminal.
>
> - [Introduction to GNU Screen](https://www.gnu.org/software/screen/)

Let's make sure we have all we need; our one program.
You can type `screen -v` in the terminal. If you get a version number, any version number your good to go.
You can [proceed to Step 1](#step-1)

Most Linux Distros ship with GNU Screen installed, but if you are like me and running a minimalistic Gentoo or Arch setup it might not be there.
Here is how you would go about doing so.

#### Arch

`sudo pacman -Syu screen`

#### Gentoo

`sudo emerge --ask app-misc/screen`

#### Solus

`sudo eopkg install screen`

#### Debian (and Debian based distros)

`sudo apt install screen`

#### Fedora

`sudo dnf install screen`

#### RHEL/CentOS

`sudo yum install screen`

I think we covered pretty good ground here.  
Let's continue.

## Step 1

### Identifying the port your device is connected on

To do this we can use the `dmesg` command. This will print out a bunch of kernel info.
Once you plug in your cable, the device should show up. We can easily find our device
by piping the output into a grep.

`sudo dmesg | grep -i tty`

You are looking for something that resembles:

![dmesg output](/img/dmesg.jpg)

## Step 2

### Connecting to the device

This is the easy part, just use screen into your tty you discovered in the previous step.

`sudo screen /dev/ttyUSB0`

Hit the `Enter` key and your in!

![Cisco Catalyst output](/img/enter-catalyst.jpg)

## GNU Screen Cheat Sheet

If you are a VIM user like I am, Screen might be a little weird to use at first.
You might be used to using TMUX (I tried to use this but there is no COM support).
Screen goes the other way and uses Emacs key-bindings, instead of vim-like keybindings.
So here are some useful commands.

`C` is short for the [CTRL] key  
`S` is short for the [Shift] key

| Command       | Description                          |
| ------------- | ------------------------------------ |
| screen [host] | Connecting to your device            |
| C-a ?         | Show key bindings                    |
| C-a \|        | Make a new vertical split window     |
| C-a S-s       | Make a new Horizontal split window   |
| C-a S-x       | Remove the current window            |
| C-a \         | Kill all windows and quit screen     |
| C-a TAB       | Cycle through splits                 |
| C-a a         | Go to beginning of line (Workaround) |
| C-e           | Go to end of line                    |
