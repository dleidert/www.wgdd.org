---
lang: en
date: 2005-10-31T22:12:00.000+01:00
last_modified_at: 2015-02-11T20:59:44.631+01:00
title: >
  The Debian package repository at debian.wgdd.de is now signed
description: >
  The private Debian repository at debian.wgdd.de is now signed. Using it may
  result in GPG related warnings about non verified signatures as long as the
  key is not added to the apt-key keyring.
category:
- debian
- planet-debian
tags:
- english
- packaging
- repository
redirect_from:
- /2005/10/debian-package-repository-at.html
---

My repository is now signed according to `apt-secure(8)`. So maybe you see the
following warning when running `apt-get`{: title="Debian APT package handling
utility"} from Debian Etch or Sid or Ubuntu Breezy:

```console
W: GPG error: http://debian.wgdd.de unstable Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 0F719C35E394D996
W: You may want to run »apt-get update« to correct these problems
```

Please read the related information about how getting my key under [Archive
signing key].

[Archive signing key]: http://debian.wgdd.de/repository#gpgkey

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
