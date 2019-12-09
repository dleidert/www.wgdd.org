---
lang: en
title: Packages removed from the debian.wgdd.de repository
date: '2008-02-29T16:48:00.000+01:00'
tags:
  - repository
  - software
  - debian
  - debichem
  - packaging
  - chemistry
redirect_from:
  - /2008/02/packages-removed-from-debianwgddde.html
---

Several packages have been removed from the archive:

## CDK

The [Chemistry Development Kit] now has been [officially packaged] and
[uploaded by Michael Koch]. If you still have my packages installed, first
uninstall/purge `libcdk-java-doc`, `cdk` und `libcdk-java-dirbrowser`
(completely) and then install the current version of [`libcdk-java`]. Scripts
found in `cdk` will probably be added to the Debian distribution soon.

[Chemistry Development Kit]: http://cdk.sourceforge.net/
[officially packaged]: {% include pkg name="libcdk-java" %}
[`libcdk-java`]: {% include pkg name="libcdk-java" %}

## Jchempaint

[Jchempaint] has been merged into CDK some time ago and there are plans to
build/package it for Debian. My packages were just outdated. Please expect
updated packages from the Debian mirror next to you :)

[Jchempaint]: http://jchempaint.sourceforge.net/

## Jmol

Ditto. ~~We are working on an official Debian package.~~ I'm not planning nor
working on an official Debian package. But there is an [ITP] for it.

[Jmol]: http://jmol.sourceforge.net/
[ITP]: {% include bts bug="512930" %}

## MOLDEN

The [MOLDEN] package was outdated. The current release is version 4.6. The
packaging files have been moved to the [debichem groups SVN repository]. You
can build the package yourself by using [`svn-buildpackage`]. Just download the
[MOLDEN source] and the [packaging files]. Then set the configuration option
<var>svn-override=buildArea</var> for `svn-buildpackage` to the place where the
upstream tarball resists (create the symlink <code>molden_4.6.orig.tar.gz -&gt;
molden4.6.tar.gz</code>) and run `svn-buildpackage` with your preferred
options.

[MOLDEN]: http://www.cmbi.ru.nl/molden/molden.html
[debichem groups SVN repository]: http://svn.debian.org/wsvn/debichem/non-free/molden/
[`svn-buildpackage`]: {% include pkg name="svn-buildpackage" %}
[MOLDEN source]: ftp://ftp.cmbi.ru.nl/pub/molgraph/molden/
[packaging files]: svn://svn.debian.org/debichem/non-free/molden/

We are currently **not** allowed to distribute MOLDEN binaries or its source
with the [Debian distribution]. But we are in contact with upstream.

[Debian distribution]: https://www.debian.org

## Clamassassin

There is an official [Debian package] of [Clamassassin] for [some time] now.
However, the package only ships the `clamssassin` script, but not
`clamdassassin`.

[Clamassassin]: http://jameslick.com/clamassassin/
[Debian package]: {% include pkg name="clamassassin" %}
[some time]: http://packages.qa.debian.org/c/clamassassin/news/20070606T223908Z.html

*[CDK]: Chemistry Development Kit
*[ITP]: Intent to Package
*[SVN]: Subversion

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
