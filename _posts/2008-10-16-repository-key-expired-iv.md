---
title: Repository key expired IV
description: >
  The key used to sign the Debian repository at debian.wgdd.de expired
  recently and got prolonged for another year.
date: '2008-10-16T20:26:00.000+02:00'
category:
  - debian
  - planet-debian
tags:
  - english
  - repository
  - debian
  - packaging
redirect_from:
  - /2008/10/repository-key-expired-iv.html
---

The repository archive key has expired at October 16th 2008. The new expire
date of the renewed key is October 16th 2009. You will have to update the key
in your apt keyring.  The updated key can be found at the [pgp.mit.edu]
keyserver or locally in ASCII format in [wgdd_archive_key.asc]{:
type="application/pgp"}. Detailed information can be found in section [Archive
signing key].

[pgp.mit.edu]: http://pgp.mit.edu:11371/pks/lookup?op=get&amp;search=0xE394D996
[wgdd_archive_key.asc]: http://debian.wgdd.de/stuff/wgdd_archive_key.asc
[Archive signing key]: http://debian.wgdd.de/repository#gpgkey

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
