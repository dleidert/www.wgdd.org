---
lang: en
title: Sarge -> Etch transition
date: '2007-05-14T20:02:00.000+02:00'
category:
  - debian
  - planet-debian
tags:
  - english
  - debian
  - dist-upgrade
redirect_from:
  - /2007/05/sarge-etch-transition.html
---

Yesterday I've finally updated my server from Sarge to Etch:

* around 300 packages to update,
* 100 newly installed and
* 15 to remove.

The whole transition went smooth in a <tt>screen</tt> session in about
4&nbsp;hours or so.

I began with a normal _upgrade_ as suggested by the release notes. The next
step introduced the new [initrd-tools] and [libc6] to the system, followed by
the installation of a new [linux-image] and [udev]. The last step in updating
the packages involved a complete <em>dist-upgrade</em>.

Then it was time for a reconfiguration of all the services, that installed
massively changed config files[^1] and fixing all the chroots and broken
package configurations caused by package transitions.

The reboot brought up the system at first go. Checking with <tt>dmesg</tt> and
[bootlogd] did not show any serious issues: <tt>/dev</tt> ok and all services
up and running with the new kernel. So besides a few modules, which are not
longer available or changed their name, no issues occured.

With the new system up and running I did some cleanup, removing unused packages
and those, that were removed in Etch (all together around 25).

That's all. New system up and running (with a few configuration works left) and
no need to restore the system from the image :). So yes, I'm satisfied. Let's
see, if issues will occur later.

[Sarge]: https://www.debian.org/releases/sarge/
[Etch]: https://www.debian.org/releases/etch/
[release notes]: https://www.debian.org/releases/stable/i386/release-notes/ch-upgrading
[initrd-tools]: {% include pkg name="initrd-tools" %}
[libc6]: {% include pkg name="libc6" %}
[linux-image]: {% include pkg name="linux-image" %}
[udev]: {% include pkg name="udev" %}
[bootlogd]: {% include pkg name="bootlogd" %}

[^1]: In this case I installed the package maintainers version and re-added my changes later.

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
