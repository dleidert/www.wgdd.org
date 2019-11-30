---
lang: en
title: Gabedit, DRAWxtl and libint are on their way into Debian
date: '2007-06-18T20:21:00.000+02:00'
category:
  - software
  - planet-debian
  - debian
tags:
  - english
  - debichem
  - packaging
  - chemistry
  - drawxtl
  - libint
  - molden
  - svn-buildpackage
redirect_from:
- /2007/06/gabedit-drawxtl-and-libint-are-on-their.html
---

This is an information for all those users and developers, which are interested
in chemistry and computational chemistry packages in [Debian]: As part of the
[debichem] project <del>at Alioth</del> I recently added [Gabedit], [DRAWxtl]
and [libint] to our project [<del>SVN</del> repository]. All packages are in a fairly good
state for an upload into the [Debian NEW queue]. Today we (Michael Banck and
me) began with [gabedit]. The other packages will follow soon (I swear).

Also thanks to Abdul-Rahman Allouche, Larry Finger (and the other DRAWxtl
authors) and Edward Valeev for these software packages and their response to my
mails :)

Our SVN repository further contains Debian packaging files for the [MOLDEN]
software package. Unfortunately we are currently not allowed to ship its source
or binaries within Debian. However, you can use our SVN repository to build the
package for yourself. Just install the [svn-buildpackage] package, download the
[MOLDEN source tarball] and [our `wnpp/molden` subversion repository],
configure `svn-buildpackage` for this setup (a complete how-to will follow
soon) and then build the package by running `svn-buildpackage`[^1].

If you are interested in our work and/or if you want to help, subscribe to our
[mailing list] and meet us there.

[Debian]: https://www.debian.org/
[debichem]: https://debichem-team.pages.debian.net/
[Gabedit]: http://gabedit.sourceforge.net/
[DRAWxtl]: http://www.lwfinger.net/drawxtl/
[libint]: https://github.com/evaleev/libint
[SVN repository]: https://salsa.debian.org/debichem-team/wnpp
[Debian NEW queue]: https://ftp-master.debian.org/new.html
[gabedit]: {% include pkg name="gabedit" %}
[MOLDEN]: http://www.cmbi.ru.nl/molden/molden.html
[svn-buildpackage]: {% include pkg name="svn-buildpackage" %}
[MOLDEN source tarball]: ftp://ftp.cmbi.ru.nl/pub/molgraph/molden/
[our `wnpp/molden` subversion repository]: https://salsa.debian.org/debichem-team/wnpp/molden
[mailing list]: https://alioth-lists.debian.net/cgi-bin/mailman/listinfo/debichem-devel

[^1]: The tree was originally created for the MOLDEN 4.x series and `svn-buildpackage`. It might be outdated by the time you read it.

*[SVN]: Subversion

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
