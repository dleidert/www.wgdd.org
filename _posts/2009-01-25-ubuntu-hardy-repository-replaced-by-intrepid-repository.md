---
title: Ubuntu Hardy repository replaced by Intrepid repository
date: '2009-01-25T21:03:00.000+01:00'
tags:
  - packaging
  - repository
  - software
  - ubuntu
redirect_from:
  - /2009/01/ubuntu-hardy-repository-replaced-by.html
---

The Ubuntu Hardy repository has been dropped and replaced by an [Intrepid]
repository. If you need the [`bluefish-unstable`] package for an Ubuntu Hardy
installation, keep the <code>deb-src</code> entry from the previous
`sources.list` snippet, get the source and the build-dependencies. Then build
the package(s) and install them.

```console?prompt=#,$
$ apt-get source bluefish-unstable
$ apt-get build-dep bluefish-unstable
$ cd bluefish-unstable-VERSION
$ debuild -us -uc
...
# dpkg -i bluefish-unstable_VERSION_ARCH.deb
```

The same goes for building the package for a different architecture than
<code>i386</code>!

[Intrepid]: http://debian.wgdd.de/debian/#intrepid
[`bluefish-unstable`]: apt+http://ubuntu.wgdd.de?package=bluefish-unstable?dist=hardy?section=main

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
