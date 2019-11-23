---
lang: en
date: 2005-06-17T21:31:00.000+02:00
last_modified_at: 2015-02-11T20:58:28.455+01:00
title: >
  Experimental Bluefish packages available
description: >
  Experimental Debian packages for bluefish have been added to debian.wgdd.de.
category:
- debian
- planet-debian
- software
tags:
- english
- repository
- bluefish
- packaging
redirect_from:
- /2005/06/experimental-bluefish-packages.html
---

I provide bluefish packages made from CVS[^1], which contain the latest
features. If you want to test the latest bluefish version, then you can install
the [`bluefish-cvs`][bluefish-cvs] package in additon to a stable `bluefish`
Debian package. Both packages use their own files and directories, so you can
do relaxed testing of the latest features. Please note that the development
version may not be stable and crash. The packages are located in the
**experimental** tree of my [Debian package repository][repository].

[^1]: Concurrent Versions System

[bluefish-cvs]: apt+http://debian.wgdd.de?package=bluefish-cvs?dist=experimental?section=main
[repository]: http://debian.wgdd.de/debian/

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
