---
lang: en
title: svn-buildpackage, debian/ only and dpatch-edit-patch
date: '2007-11-04T20:09:00.000+01:00'
category:
  - planet-debian
  - debian
tags:
  - english
  - debian
  - packaging
redirect_from:
- /2007/11/svn-buildpackage-debian-only-and-dpatch.html
---

I guess, we (the [debichem] developers) are not the only people doing some
collaborative package maintenance using a [SVN server] (just look at
[svn.debian.org]) and [svn-buildpackage]. To avoid duplication of source code
we decided to only keep the [Debian packaging files] under version control
(this also leads to less checkout traffic).

This layout has a problem. You cannot directly create patches, because the SVN
of course misses the source code of the package. Fortunately, there is a
solution for [dpatch] users. The `dpatch-edit-patch` utility provides a switch
to handle the above described design: the `-b` switch. Now all we have to do
is, to tell dpatch, where to find the `.orig.tar.gz` tarball. There is another
utility used for this task: `dpatch-get-origtargz`. This small tool does the
following:

1. check if the tarball can be found in the location given by the
   <var>DPEP_GETORIGTARGZ</var> environment variable or the
   <var>conf_getorigtargz</var> option (`${HOME}/.dpatch.conf`)

1. try to get the tarball from the Debian archive

1. try to get the tarball using `debian/watch`

I don't want to speak about the possibilities two or three. Interesting is the
possibility one. In my case, I have the SVN directories under
`/usr/local/src/packages/pkg-${PACKAGE}` and the tarballs under
`/usr/local/src/packages/${PACKAGE}`. So I tell dpatch the following via
`${HOME}/.dpatch.conf`:

```shell
PACKAGENAME="$(dpkg-parsechangelog | \
        sed -n '/^Source:/{s/^Source:[[:space:]]\+\(.*\)/\1/;p;q}')"
UPSTREAMVERSION="$(dpkg-parsechangelog | \
        sed -n '/^Version:/{s/^Version:[[:space:]]\+\([0-9]\+:\)\?\([^-]\+\).*/\2/;p;q}')"

conf_origtargzpath="/usr/local/src/packages/${PACKAGENAME}"
```
{: title="${HOME\}/.dpatch.conf"}

Now some of you might use different locations of the `.orig.tar.gz` tarballs.
I've created another example `dpatch.conf` to satisfy such needs. Just adjust
the <code>if...else</code> construct to adjust the following
`${HOME}/.dpatch.conf` for your needs:

```shell
PACKAGENAME="$(dpkg-parsechangelog | \
        sed -n '/^Source:/{s/^Source:[[:space:]]\+\(.*\)/\1/;p;q}')"
UPSTREAMVERSION="$(dpkg-parsechangelog | \
        sed -n '/^Version:/{s/^Version:[[:space:]]\+\([0-9]\+:\)\?\([^-]\+\).*/\2/;p;q}')"

if [[ `pwd` =~ '^.*/debian-med/trunk/packages/.*$' ]]
then
        conf_origtargzpath="/usr/local/src/packages/debian-med/trunk/packages/${PACKAGENAME}"
else
        conf_origtargzpath="/usr/local/src/packages/${PACKAGENAME}"
fi
```
{: title="${HOME\}/.dpatch.conf"}

What about [quilt]-users? Well, I did not yet use it, so I cannot tell you,
what to do here. But I'm sure, there is some way to realize the same behaviour.

## Update

The tool `svn-do` can be used to create [quilt] patches.

[debichem]: https://debichem-team.pages.debian.net/
[SVN server]: https://svn.debian.org/wsvn/debichem
[svn.debian.org]: https://svn.debian.org/
[svn-buildpackage]: {% include pkg name="svn-buildpackage" %}
[Debian packaging files]: https://www.debian.org/doc/maint-guide/
[dpatch]: {% include pkg name="dpatch" %}
[quilt]: {% include pkg name="quilt" %}

*[SVN]: Subversion

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
