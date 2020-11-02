---
vim: tw=79:ts=2:sw=2:ai:si:et
title: Import the tails Debian repository key
description: >-
  The import of the tails Debian repository key failed with '... but contains
  no user ID - skipped'. This is due to keys.openpgp.org stripping all ID
  information.
category:
- planet-debian
- debian
tags:
- gnupg
- tails
- repository
- apt-secure
- openpgp
---

I recently had to deal with [tails] to create a [custom image]. I needed to
[add] the Tails repository to my system in order to build it. But `apt` started
throwing errors:

```console
$ sudo apt-get update
[..]
W: GPG error: http://deb.tails.boum.org builder-bullseye InRelease:
The following signatures couldn't be verified because the public key is not available: NO_PUBKEY C7988EA7A358D82E
```

Trying to import the key failed too due to

```console
$ gpg --recv-keys C7988EA7A358D82E
gpg: key C7988EA7A358D82E: new key but contains no user ID - skipped
gpg: Total number processed: 1
gpg:           w/o user IDs: 1
```

Then I remembered that my default keyserver `hkp://keys.openpgp.org` [strips]
the identity information. I finally ended up importing the key from the old SKS
keyservers using `apt-key`:

```console
$ sudo apt-key adv --keyserver hkps.pool.sks-keyservers.net --allow-non-selfsigned-uid --recv-keys C7988EA7A358D82E
```

[tails]: https://tails.boum.org/
[custom image]: https://tails.boum.org/contribute/how/code/HACKING/
[add]: https://tails.boum.org/contribute/build/
[strips]: https://keys.openpgp.org/about
