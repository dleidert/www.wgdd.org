---
lang: en
title: bluefish-unstable packages ready for testing
date: '2007-12-22T20:39:00.000+01:00'
category:
  - planet-debian
  - debian
  - software
tags:
  - bluefish
  - english
  - software
  - debian
  - packaging
redirect_from:
  - /2007/12/bluefish-unstable-packages-ready-for.html
---

I promised it some time ago and now it has been done: Debian packages for the
development tree (1.1 series) of [Bluefish] are [ready] for Debian users and
called [`bluefish-unstable`]. The packages can be installed along with the
stable version, so you can safely test new features and give us feedback and
bug reports.

## NOTE

The packages **cannot** be (re)built on Etch, because [`debhelper`] version
5.0.57 or higher is necessary. I will fix this part of `debian/rules` soon, so
it can be (re)built on Etch too.

[Bluefish]: http://bluefish.openoffice.nl/
[ready]: http://debian.wgdd.de/debian/#experimental
[`bluefish-unstable`]: apt+http://debian.wgdd.de?package=bluefish-unstable?dist=experimental?section=main
[`debhelper`]: {% include pkg name="debhelper" %}

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
