---
layout: page
title: Setup 
permalink: /setup/
---

This page is for *personal reference* and includes applications that I would
install on a new machine.

---

### Package Manager

The only real choice for a package manager on Mac OS is *Homebrew*. Homebrew allows
you to install applications and command-line-interface (CLI) tools with
a simple command. 

Download and install Homebrew from [brew.sh](https://brew.sh)

### Installing applications with Homebrew

To install applications with a user interface (UI) with brew use 

```
$ brew cask install <application>
```

And to install CLI tools

```
$ brew install <cli tool>
```

It is also possible to search for applications with 

```
$ brew search <application>
```

Dump of some of the applications that I use for easy install. A mix of GUI
applications and nice-to-haves like *tree* and *htop*.

```
$ brew install chromium discord cyberduck iterm2 logitech-options spotify
neofetch neovim typora tree visual-studio-code vlc htop
```

Also to install *lua* and *Löve2D*

```
$ brew install lua love
```

### Setting up Visual Studio Code

*Not really necessary anymore, as they allowed for settings to be synced
online*
