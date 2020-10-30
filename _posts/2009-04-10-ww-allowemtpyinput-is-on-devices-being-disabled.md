---
title: "(WW) AllowEmtpyInput is on, devices using drivers &lt;kbd&gt; or &lt;mouse&gt; will be disabled"
date: '2009-04-10T21:47:00.000+02:00'
category:
- debian
- planet-debian
tags:
- software
- bug
- debian
- xorg
last_modified_at: '2015-02-11T21:16:37.575+01:00'
redirect_from:
- /2009/04/ww-allowemtpyinput-is-on-devices-using.html
---

Maybe you will observe a changed mouse and keyboard behavior after updating
X.org recently in Debian Sid. Then you will probably discover the warning
mentioned in the title in your X.org server log `/var/log/Xorg.0.log`. The very
short and dirty solution to get things working for the moment is to put this
into your `/etc/X11/xorg.conf`:

```
Section "ServerLayout"
    Option "AutoAddDevices" "off"
EndSection
```

See the first entry in `/usr/share/doc/xserver-xorg/NEWS.Debian.gz` and follow
the mentioned links for more information. However, the above solution should
only be a temporary workaround: Try to migrate things (I will post changes for
[my system] asap).

[my system]: http://debian.wgdd.de/system/

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
