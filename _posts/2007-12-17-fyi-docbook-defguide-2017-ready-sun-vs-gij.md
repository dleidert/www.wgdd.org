---
lang: en
title: 'FYI: docbook-defguide 2.0.17 ready - Sun Java vs. GIJ building the package'
date: '2007-12-17T21:51:00.000+01:00'
category:
  - planet-debian
  - debian
tags:
  - english
  - docbook
  - packaging
  - java
  - gij
  - docbook-defguide
redirect_from:
  - /2007/12/fyi-docbook-defguide-2017-ready-sun.html
---

Ok guys. After spending several hours of this weekend to package the latest
release of Norman Walshs [<cite>DocBook: The Definitive Guide</cite>][defguide]
I'm now proud to tell you: It's [done]!

I was able to build the package with the free Java engine ([GIJ]) so
`docbook-defguide` can stay in main. However, it was some kind of
disappointing: [Sun Java] needs an hour and a maximum heapsize of 512MB to
build the package on [my system]. GIJ needs **16 hours** and a maximum heap
size of 1GB to build. [kaffe], which I tried too, fails much earlier than GIJ
with a maximum heap size of 512MB. So I decided against it and for GIJ.

If you know of a way to speed up the build process (besides the possibility to
buy a faster system ... except you want to make it your christmas or birthday
present for me *g*) don't hesitate to tell me. The packaging files are in the
[Debian XML/SGML groups SVN repository].

However, expect the package in your Debian repository soon (guess, my sponsor
wants to rebuild it, which may need another 1x hours :)).

## Update

Ardo van Rangelrooij kindly [offered] to build the package on an AMD X2 4600+
with 6GB. The build time decreased to at least 7-8 hours. The package will be
uploaded to the Debian archive within the next days.

[defguide]: http://docbook.org/tdg/
[done]: http://debian.wgdd.de/debian/incoming/packages/
[GIJ]: http://gcc.gnu.org/java/
[Sun Java]: {% include pkg name="sun-java5-jre" %}
[my system]: http://debian.wgdd.de/system/
[GIJ]: {% include pkg name="gij" %}
[kaffe]: {% include pkg name="kaffe-pthreads" %}
[Debian XML/SGML groups SVN repository]: http://svn.debian.org/wsvn/debian-xml-sgml/packages/docbook-defguide/trunk/?rev=0&amp;sc=0
[offered]: http://lists.debian.org/debian-mentors/2007/12/msg00322.html

*[GIJ]: GNU Interpreter for Java

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
