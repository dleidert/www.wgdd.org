---
title: Repository key expired V
date: '2009-10-16T21:54:00.000+02:00'
description: >
  The key used to sign the Debian repository at debian.wgdd.de expired
  recently and got prolonged for another year.
category:
- debian
- planet-debian
tags:
- ubuntu
- english
- repository
- debian
- packaging
last_modified_at: '2015-02-11T21:17:15.976+01:00'
redirect_from:
- "/2009/10/repository-key-expired-v.html"
---

The repository archive key had expired at October 16th 2009. I've changed the
expiration date to be October 17th 2010. So you will have to update the key in
your apt keyring. The updated key can be found at the [pgp.mit.edu][keyerver]
keyserver or locally in ASCII format at [`wgdd_archive_key.asc`][filelink]{:
type="application/pgp"}. Alternatively the `wgdd-archive-keyring` package can
be updated. Detailed information can be found [here][helplink].

[keyerver]: http://pgp.mit.edu:11371/pks/lookup?op=get&amp;search=0xE394D996
[filelink]: http://debian.wgdd.de/stuff/wgdd_archive_key.asc
[helplink]: http://debian.wgdd.de/repository#gpgkey

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
