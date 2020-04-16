---
layout: post
title:  "VNC Setup on Ubuntu"
---

## Ubuntu 14.04

Many people have complained about the incompatibility between VNC and Ubuntu 14.04. The default xstartup file just doesn't work. If you go online, there are tons of different xstartup files for you to choose from. Of course the majority still don't work, but there are two successful cases.

One is using xfce4. The GUI is a little bit "ugly", but who cares ;) [This][xfce4] is a very good tutorial following this setup.

{% highlight shell %}
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
{% endhighlight %}

The other one was discovered by my labmate. The GUI is the original Ubuntu, so really there is nothing I could complain about ;) The original link is [here][ubuntu].

{% highlight shell %}
#!/bin/sh
def
export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
 
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
{% endhighlight %}

## Ubuntu 16.04

According to some of my labmates, the xstartup immediate above still works for 16.04. That is not the case for me after upgrading though. Fortunately, with the **Desktop Sharing** provided by 16.04, I do not need to bother with the xstartup file at all!

Just follow [this step-by-step guide][guide] first to enable desktop sharing on the server. Then just open your VNC Viewer and connect to the server's IP address!



[guide]: http://ubuntuhandbook.org/index.php/2016/07/remote-access-ubuntu-16-04/

[xfce4]: https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-14-04
[ubuntu]: http://onkea.com/ubuntu-vnc-grey-screen/