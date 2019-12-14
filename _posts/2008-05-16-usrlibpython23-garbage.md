---
title: "/usr/lib/python2.3 garbage"
date: '2008-05-16T20:14:00.000+02:00'
tags:
  - software
  - bug
  - debian
  - python
redirect_from:
  - /2008/05/usrlibpython23-garbage.html
---

Yesterday I stumbled about files and dead symlinks left in
`/usr/lib/python2.3/site-packages/` on my Sid box. These files/symlinks seem to
have been shipped or created by:

```text
kiki
python-cairo
python-crypto
python-egenix-mxtools
python-foomatic
python-imaging
python-imaging-sane
python-ldap
python-logilab-common
python-mysqldb
python-numarray
python-pygresql
python-reportlab
python-xml
```

Deleting `/usr/lib/python2.3` (<code>dpkg -S</code> didn't show any package
relationship nor did I find something in `/var/lib/dpkg/info/`) and
reinstalling the above mentioned packages did not recreate the files/symlinks.
So it seems the directory can be safely removed. Maybe I missed some
announcement or one (or more) packages need to be fixed. No time to examine it
atm.

## Update

This is known as Debian bug [#409390]({% include bts bug="409390" %}). Thanks
to Josselin Mouette for the information.

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
