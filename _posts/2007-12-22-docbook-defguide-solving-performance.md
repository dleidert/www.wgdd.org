---
lang: en
title: docbook-defguide - solving performance and timing issues with native code
date: '2007-12-22T18:50:00.000+01:00'
category:
  - software
  - planet-debian
tags:
  - english
  - docbook
  - packaging
redirect_from:
  - /2007/12/docbook-defguide-solving-performance.html
---

Some days ago [I wrote down] my experiences with packaging
[`docbook-defguide`]. The main (remaining) issues I mentioned were the
resources and the time the package needs to build. Even on an AMD X2 4600+ with
6GB of RAM it needs 7-8 hours.

[I wrote down]: {% post_url 2007-12-17-fyi-docbook-defguide-2017-ready-sun-vs-gij %}
[`docbook-defguide`]: {% include pkg name="docbook-defguide" %}

Today I met with Torsten Werner. He mentioned that there are some more JVMs I
could try. So I tested alternatives to GIJ this night. I found [this short
summary] about free JVMs which was some kind of interesting.

[this short summary]: http://web.archive.org/web/*/http://www.rnd.cx/freejava.html

## CACAO

I began with [`cacao`] which seemed to be fast, but it was killed very early in
the build process with an `java.lang.OutOfMemory` error. Even playing around
with the `-Xms` and `-Xmx` switches in `buildtools/saxon.sh` did not help. So I
dropped it from the list. Seems both `cacao` and `kaffe` create similar
problems here and are not suitable for building the package.

[`cacao`]: {% include pkg name="cacao" %}

## SableVM

Second alternative I tried was [`sablevm`]. It instantaneously threw out some
warnings or errors so I directly dropped it too.

[`sablevm`]: {% include pkg name="sablevm" %}

## JamVM

Next JVM was [`jamvm`]. But it was as slow as GIJ. So I dropped it from the list of alternatives too.

[`jamvm`]: {% include pkg name="jamvm" %}

## GCJ

Then I found an interesting statement in the article I linked somewhere above.
The author said, that his perfomance test time with GCJ/GIJ reduced from 433 to
9&nbsp;seconds when he compiled his application into a native executable. So I
took a quick look through the [`docbook-defguide`] build dependencies and found
that [Debian] already provides a natively compiled Xerces package
[`libxerces2-java-gcj`]. But there were no packages for [`libsaxon-java`]
([#458247]), [`libxml-commons-resolver1.1-java`] ([#458248]) and
[`docbook-xsl-saxon`]. So short and dirty: I downloaded the source for these
packages, added the necessary stuff to get natively compiled packages too,
built and installed them. Fortunately packages with native code already existed
for their dependencies [JAXP] 1.3 and [Xerces].

[Debian]: https://www.debian.org/
[`libxerces2-java-gcj`]: {% include pkg name="libxerces2-java-gcj" %}
[`libsaxon-java`]: {% include pkg name="libsaxon-java" %}
[`libxml-commons-resolver1.1-java`]: {% include pkg name="libxml-commons-resolver1.1-java" %}
[`docbook-xsl-saxon`]: {% include pkg name="docbook-xsl-saxon" %}
[JAXP]: https://jaxp.java.net/
[Xerces]: http://xerces.apache.org/xerces2-j/
[#458248]: {% include pkg id="458248" %}
[#458247]: {% include pkg id="458247" %}

And what should I say: Building the TDG now needs less then 512MB RAM and it
builds in around an hour ... even on [my system]. I will ask the Debian Java
maintainers to add `-gcj` packages for [Saxon] and [XML-Commons] and fix my own
`docbook-xsl-saxon` package. This will hopefully help maintaining
`docbook-defguide`.

[my system]: http://debian.wgdd.de/system/
[Saxon]: http://saxon.sourceforge.net/
[XML-Commons]: http://xml.apache.org/commons/

*[JVM]: Java Virtual Machine
*[GIJ]: GNU Interpreter for Java
*[GCJ]: GNU Compiler for Java
*[JAXP]: Java API for XML
*[TDG]: DocBook - The Definitive Guide

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
