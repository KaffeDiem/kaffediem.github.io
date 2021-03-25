---
layout: post
title: Remarkable 2 thoughts on software and some modifications
---

A few modifications to the reMarkable 2 makes it way more pleasant to use. Notice that if you
do install these mods or change the lockscreen wallpaper, they will dissapear after a software
update. Therefore, *it is recommended, that you disable automatic updates.*

# Changing the lockscreen image

![alt text][1]

One thing that the reMarkable team should have included in the desktop software
is a way to change the lockscreen wallpaper. The default "reMarkable is
sleeping" is just so boring. Lucky for us the user is given root access to the
device and we can change the lockscreen image manually (the lockscreen text is
actually just a .png image being loaded every time you lock the screen). 

##### Method 1: Using Cyberduck

Cyberduck is an application that connects to servers or the cloud using
different protocols. It also suppports SSH which is what we will be using to access the
reMarkable 2, also this can be done wirelessly. 

[Download Cyberduck](https://cyberduck.io). 
(For Mac users using Homebrew: `$ brew install cyberduck`)

For Cyberduck to know what device to connect to it will need an IP address.
This is the address of the reMarkable. This address and the password can be found under
`Settings -> Help -> Copyrights and licenses`. You will need them to access 
the reMarkable, and also *keep the password safe and stored, take an image or
put it down on a piece of paper!* 
If anything goes bad this will be your only way to access the device.

![alt text][2]

The local IP address can be seen on the bottom of the page. Just above it you
should see the password.
Notice that the IP address is a local one - no one on the
internet will be able to access your device with it, that is why I am sharing
mine without a doubt here, however, *keep the password secret*. 

If your device is connected to a computer two IP addresses will be shown. For 
wireless access use the one starting with `192.168.x.xx`.

![alt text][3]

Open up Cyberduck and press `New Connection`. Enter the IP address and the
password that you have just found on the reMarkable. The port should be set
to `22` and the username to `root`.

![alt text][4]

Start by navigating to the root folder.

![alt text][5]

Then navigate to `usr/share/remarkable`. Here you should see a `suspended.png`
file. This is the one you will be replacing. Start by renaming it to
`suspended.old` in case you want to use it again sometime. Then simply drag and
drop your new lockscreen image into the folder. Rename your lockscreen image to
`suspended.png` and try locking your device! For best results you should use an
image of the size *1404x1872*. This is the native resolution of the reMarkable
2.

# Installing ddvk mods

The ddvk mods adds a loft of improvements to the original software. It allows
you to quickly change between recently opened files and adds some very useful 
getures like being able to quickly change between the most recently used tools
and a gesture for undo and redo. 

Take a look at the [Github page](https://github.com/ddvk/remarkable-hacks) 
for a comprehensive list of features.

The install instructions may not be intuitively clear for those who have not
used the terminal before. 

Open Spotlight (`CMD + Space`) and search for terminal. Then enter `ssh
root@192.168.x.xx` where the x's should be replaced by your IP address. See the
guide for replacing your lockscreen for details on where to find it. Then press
enter. You should now be asked for your password. This can be found in above
guide as well. After succesfully connecting to your reMarkable you should be
met by the following screen:

![alt text][01]

Then copy and paste this *automagic* line. It downloads and patches the binary
files on the reMarkable with the modded ones.

```shell
sh -c "$(wget https://raw.githubusercontent.com/ddvk/remarkable-hacks/master/patch.sh -O-)"
```

![alt text][02]

After pressing enter you should be met by this screen, and the reMarkable
should restart.

![alt text][03]

You can now play around with the mods. Hold down `CTRL` and press `c` to either
abort or install them. To install the mods press `y` and then `enter` to make
them permanent (at least till you update the device, thus it is recommended
that you disable automatic updates).

![alt text][04]

[1]: /images/2021-remarkable2/8.jpeg "reMarkable 2 with a custom wallpaper"
[2]: /images/2021-remarkable2/7.jpeg "reMarkable 2 SSH access"
[3]: /images/2021-remarkable2/2.png "Cyberduck screenshot"
[4]: /images/2021-remarkable2/3.png "Cyberduck navigation"
[5]: /images/2021-remarkable2/5.png "Cyberduck navigation"
[01]: /images/2021-remarkable2/01.png "Terminal"
[02]: /images/2021-remarkable2/02.png "Terminal"
[03]: /images/2021-remarkable2/03.png "Terminal"
[04]: /images/2021-remarkable2/04.png "Terminal"
