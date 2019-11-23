---
lang: en
title: Repository key expired II
date: '2006-10-20T23:34:00.000+02:00'
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
last_modified_at: '2015-02-11T21:02:10.885+01:00'
redirect_from:
- /2006/10/repository-key-expired-ii.html
---

The repository archive key has expired. I've changed the expiration date, so
you will have to update the key in your apt keyring. The updated key can be
found at [pgp.mit.edu] keyserver or locally in ASCII format in 
[wgdd_archive_key.asc]{: type="application/pgp"}. Detailed information can be
found in section [Archive signing key].

[pgp.mit.edu]: http://pgp.mit.edu:11371/pks/lookup?op=get&amp;search=0xE394D996
[wgdd_archive_key.asc]: http://debian.wgdd.de/stuff/wgdd_archive_key.asc
[Archive signing key]: http://debian.wgdd.de/repository#gpgkey

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
