---
title: bluefish-unstable packages for Etch removed from repository
date: '2009-02-02T21:09:00.000+01:00'
last_modified_at: false
tags:
  - bluefish
  - debian
  - packaging
  - software
redirect_from:
  - /2009/02/bluefish-unstable-packages-for-etch.html
---

The [`bluefish-unstable`] packages for [Etch] have been removed from the
repository. The 1.1 development series has been superseeded by the 1.3 series
(1.0 is still the current stable series!), which needs Glib/GTK versions higher
than available in Etch. Unfortunately, the necessary versions are also not
available from [backports.org]. So I can't build packages for Etch anymore :(.

If you have some self-packaged or self-compiled versions of these libraries,
you can of course build the application from its source.

[`bluefish-unstable`]: apt+http://debian.wgdd.de?package=bluefish-unstable?dist=etch?section=main
[Etch]: https://www.debian.org/releases/etch/
[backports.org]: https://backports.debian.org

*[GTK]: GIMP Toolkit

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
