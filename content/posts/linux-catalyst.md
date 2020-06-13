+++
title = ""
date = "2020-06-13T06:31:44-04:00"
author = "Tom Konidas"
authorTwitter = "tomkonidas"
cover = ""
tags = ["linux", "catalyst"]
keywords = ["linux", "screen", "gnu","catalyst", "switch","router"]
description = "Connecting to Cisco hardware consoles on Linux with GNU Screen."
showFullContent = false
draft = true
+++

> Connecting to Cisco hardware consoles on Linux with GNU Screen.

After a little bit of online googling, I came to a conclusion there aren't
that many tutorials that go about connecting to Cisco gear via COM port with Linux.
Most articles are using SSH/Telnet or through PuTTy on Windows.

So here I am making this easy to follow guide on how to do it.
This is more for me to reference when/if I forget how in the future.
I actually find it a lot easier this way rather than going to sketchy Chinese
websites to download specific drivers, then to put in the important settings such
as Parity, Baud Rate, etc...

My way; the Linux way, is the simplest IMHO.
All you need is 1 program and your off to the races.

**Note**: This also works for BSDs or any other \*NIX OS that is able to run GNU Screen... (I'm looking at you OSX🧐)

## Step 0: Prerequisites

What is [GNU Screen](https://www.gnu.org/software/screen/)?

> Screen is a full-screen window manager that multiplexes a physical terminal between several processes, typically interactive shells. Each virtual terminal provides the functions of the DEC VT100 terminal and, in addition, several control functions from the ANSI X3.64 (ISO 6429) and ISO 2022 standards (e.g., insert/delete line and support for multiple character sets). There is a scrollback history buffer for each virtual terminal and a copy-and-paste mechanism that allows the user to move text regions between windows. When screen is called, it creates a single window with a shell in it (or the specified command) and then gets out of your way so that you can use the program as you normally would. Then, at any time, you can create new (full-screen) windows with other programs in them (including more shells), kill the current window, view a list of the active windows, turn output logging on and off, copy text between windows, view the scrollback history, switch between windows, etc. All windows run their programs completely independent of each other. Programs continue to run when their window is currently not visible and even when the whole screen session is detached from the users terminal.
>
> - [Introduction to GNU Screen](https://www.gnu.org/software/screen/)

Let's make sure we have all we need; our one program.
You can type `screen -v` in the terminal. If you get a version number, any version number your good to go.
You can [proceed to Step 1](#step-1)

Most Linux Distros ship with GNU Screen installed, but if you are like me and running a minimalistic Gentoo or Arch setup it might not be there.
Here is how you would go about doing so.

### Arch

`sudo pacman -Syu screen`

### Gentoo

`sudo emerge --ask app-misc/screen`

### Solus

`sudo eopkg install screen`

### Debian (and Debian based distros)

`sudo apt install screen`

### Fedora

`sudo dnf install screen`

### RHEL/CentOS

`sudo yum install screen`

I think we covered pretty good ground here.  
Let's continue.

## Step 1
