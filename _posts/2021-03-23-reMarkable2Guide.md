---
layout: post
title: Remarkable 2 modifications 
---

A few modifications to the reMarkable 2 makes it a joy to use. Notice that if you
do install mods or change the lockscreen wallpaper, they will dissapear on a software
update. Therefore, it is recommended, that you disable automatic updates. 

## Changing the lockscreen image

![alt text][1]

One thing that the reMarkable team should have included in the desktop software
is a way to change the lockscreen wallpaper. As the user is given root access to 
the device this can be done manually. 

##### Method 1: Using Cyberduck

Cyberduck is an application that connects to servers or the cloud using
different protocols. It also suppports SSH which is what we can access the
reMarkable 2 with wirelessly. 

[Download Cyberduck](https://cyberduck.io).

For Cyberduck to know what device to connect to it will need an IP address. The
IP address for the reMarkable 2, as well as the password, can be found under
`Settings -> Help -> Copyrights and licenses`. You will need them to access 
the reMarkable wirelessly. *Keep the password safe, write it down!* If anything
goes bad this will be your only way to access the device.

![alt text][2]

The local IP address can be seen on the bottom of the page. Just above it the 
password is written. Notice that the IP address is a local one - no one on the
internet will be able to access your device with it. 

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
file. This is the one you will be replacing. Replace it with some other image
in the resolution *1404 x1872*. This is the native resolution of the reMarkabe.

## Installing ddvk mods

The ddvk mods adds a loft of improvements to the original software. It allows
you to quickly change between recently opened files and adds some useful
getures. 

Take a look at the [Github page](https://github.com/ddvk/remarkable-hacks) 
for a comprehensive list of features.

The install instructions may not be intuitively clear

[1]: /images/2021-remarkable2/8.jpeg "reMarkable 2 with a custom wallpaper"
[2]: /images/2021-remarkable2/7.jpeg "reMarkable 2 SSH access"
[3]: /images/2021-remarkable2/2.png "Cyberduck screenshot"
[4]: /images/2021-remarkable2/3.png "Cyberduck navigation"
[5]: /images/2021-remarkable2/5.png "Cyberduck navigation"