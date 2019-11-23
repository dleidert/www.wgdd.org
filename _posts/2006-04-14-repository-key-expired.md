---
lang: en
date: '2006-04-14T19:29:00.000+02:00'
last_modified_at: '2015-02-11T20:59:59.419+01:00'
title: >
  Repository key for debian.wgdd.de expired
description: >
  The key used to sign the Debian repository at debian.wgdd.de expired
  recently and got prolonged for another year.
category:
- debian
- planet-debian
tags:
- english
- packaging
- repository
redirect_from:
- /2006/04/repository-key-expired.html
---

The repository archive key had expired. I've changed the expiration date, so
you will have to update the key in your apt keyring. The updated key can be
found at the [pgp.mit.edu][keyerver] keyserver or locally in ASCII format at
[`wgdd_archive_key.asc`][filelink]{: type="application/pgp"}. Detailed
information can be found [here][helplink].

[keyerver]: http://pgp.mit.edu:11371/pks/lookup?op=get&amp;search=0xE394D996
[filelink]: http://debian.wgdd.de/stuff/wgdd_archive_key.asc
[helplink]: http://debian.wgdd.de/repository#gpgkey

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
