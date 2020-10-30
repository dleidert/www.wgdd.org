---
title: Ubuntu Jaunty repository replaced by Ubuntu Intrepid repository
date: '2009-08-18T21:47:00.000+02:00'
category:
- planet-debian
- ubuntu
tags:
- ubuntu
- repository
- software
- packaging
- bluefish
last_modified_at: '2015-02-11T21:16:49.069+01:00'
redirect_from:
- /2009/08/ubuntu-jaunty-repository-replaced-by.html
---

Packages of `bluefish-unstable` are now built for Ubuntu Jaunty instead of
Intrepid. You must adjust the entries in [`/etc/apt/sources.list`] or update
[`/etc/apt/sources.list.d/debian.wgdd.de_ubuntu.list`]. You'll receive HTML
error code <code>410</code> ("resource gone") using the old entries.

[`/etc/apt/sources.list`]: http://debian.wgdd.de/stuff/debian.wgdd.de_ubuntu.list
[`/etc/apt/sources.list.d/debian.wgdd.de_ubuntu.list`]: http://debian.wgdd.de/debian/#apt-get

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
