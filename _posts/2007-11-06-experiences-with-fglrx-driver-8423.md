---
lang: en
title: Experiences with the “new” fglrx-driver 8.42.3 package
date: '2007-11-06T20:19:00.000+01:00'
category:
  - software
  - debian
  - planet-debian
tags:
  - debian
  - driver
  - english
  - fglrx
  - graphics
  - software
redirect_from:
  - /2007/11/experiences-with-fglrx-driver-8423.html
---

Yesterday I found some minutes to update my kernel. Because I did not have time
to compile a 2.6.22 kernel I simply installed [`linux-source-k7`]
([`linux-source-2.6-k7`]). This was a &#8220;welcome&#8221; occassion to update
the [ATI/AMD Linux driver] for my Radeon X1650 Pro graphics card to their
latest version [8.42.3].


As a first step I had to find out that upgrade from my [8.38.x] version did
not seem to work properly. I got some error messages regarding the diversions
in `/usr/lib/fglrx/diversions/`. So I purged the [`fglrx`] packages. Then I
manually removed the diversions, the (now) empty `/usr/lib/fglrx/diversions/`
directory, and the configuration directory `/etc/ati`:

```console
$ apt-get remove --purge fglrx-driver fglrx-kernel-src fglrx-control
$ dpkg-divert --remove /usr/llib/libGL.so.1
$ dpkg-divert --remove /usr/llib/libGL.so.1.2
$ rm -rf /usr/lib/fglrx /etc/ati
```
{: title="Shell output"}

Then I reinstalled the `fglrx` packages, installed the headers
[`linux-headers-2.6-k7`] and prepared the flgrx module package with `m-a`:

```console
$ m-a prepare
$ m-a -l 2.6.22-3-k7 build fglrx
```
{: title="Shell output"}

Installing the package and rebooting brought up the system again. `glxgears`
shows around 3000 FPS. However, although everything seems to work properly, I
found some log entries and errors, that concern me.

First thing is, that `fgl_glxgears` refuses to work.

```console
$ fgl_glxgears
Using GLX_SGIX_pbuffer
X Error of failed request:  GLXUnsupportedPrivateRequest
  Major opcode of failed request:  131 (GLX)
  Minor opcode of failed request:  16 (X_GLXVendorPrivate)
  Serial number of failed request:  42
  Current serial number in output stream:  43
```
{: title="Shell output"}

Looking into the `Xorg.0.log` shows me the error message 

```text
(EE) fglrx(0): Failed to enable interrupts.
```
{: title="Xorg.0.log"}

And `dmesg` shows this:

```text
[fglrx] IRQ_MGR is disabled untill GART_CACHABLE memory will be implemented
[fglrx] Internal AGP support requested, but kernel AGP support active.
[fglrx] Have to use kernel AGP support to avoid conflicts.
[fglrx] AGP detected, AgpState   = 0x1f000217 (hardware caps of chipset)
agpgart: Found an AGP 2.0 compliant device at 0000:00:00.0.
agpgart: Putting AGP V2 device at 0000:00:00.0 into 4x mode
agpgart: Putting AGP V2 device at 0000:01:00.0 into 4x mode
[fglrx] AGP enabled,  AgpCommand = 0x1f000314 (selected caps)
[fglrx:firegl_lock] *ERROR* Process 32648 is using illegal context 0x00000003
```
{: title="dmesg output"}

This is very similar to everything I read at e.g. [phoronix.com]. So if you
read between the lines: I did not find a solution nor an answer to the shown
error message(s) nor the runtime error. So if you know, what's causing this and
how it can be solved, please let me know.

At least the good news is: XVideo seems to work again. No juddering video
playback. I like that. Now the bad news: It still burdens my CPU (causes a
constant usage of 50-70%). I can even observe this effect when the
`screensaver` is running ... and I think, this is **NOT** the intended design.
So I turned off the screensaver for now and simply make the screen go black and
lock.

**PS:** Maybe I will have a look at updating the fglrx manpages (@ATI/AMD: They
are still offered for adoption!)

[`linux-source-k7`]: https://packages.qa.debian.org/linux-source-k7
[`linux-source-2.6-k7`]: https://packages.qa.debian.org/linux-source-2.6-k7
[ATI/AMD Linux driver]: http://www.ati.com/online/rss/atilinuxdriver.rss?OTC-rssfeedlinux
[8.42.3]: http://www2.ati.com/drivers/linux/linux_8.42.3.html
[8.38.x]: http://www2.ati.com/drivers/linux/linux_8.38.6.html
[`fglrx`]: https://packages.qa.debian.org/fglrx-driver
[`linux-headers-2.6-k7`]: https://packages.qa.debian.org/linux-headers-2.6-k7
[phoronix.com]: http://www.phoronix.com/forums/showthread.php?t=5947

*[ATI]: ATI Technologies Inc.
*[AMD]: Advanced Micro Devices

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
