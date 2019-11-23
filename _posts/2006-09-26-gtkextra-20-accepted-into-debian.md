---
lang: en
title: Gtk+Extra 2.0 accepted into Debian
date: '2006-09-26T22:10:00.000+02:00'
category:
- debian
- planet-debian
- software
tags:
- english
- packaging
- gtk+extra2
last_modified_at: '2015-02-11T21:01:30.916+01:00'
redirect_from:
- /2006/09/gtkextra-20-accepted-into-debian.html
---

[Debian] now [officially contains] packages for [Gtk+Extra 2.0]. So I removed
the packages from my repository. Please use the ones officially provided by
Debian. There is **no** automatic way of upgrading to the official Debian
packages, so you have to remove my packages first:

```console
su -c "apt-get remove --purge libgtkextra-2.0-1 libgtkextra-2.0-1-dev"
```

before you install the official Debian packages!

[Debian]: https://www.debian.org/ "The Debian project"
[officially contains]: https://packages.qa.debian.org/gtk+extra2
[Gtk+Extra 2.0]: http://gtkextra.sourceforge.net/

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
