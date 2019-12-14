---
title: Update to Lenny
date: '2009-02-17T19:15:00.000+01:00'
tags:
  - cvsd
  - debian
  - dist-upgrade
  - lenny
  - openssh
last_modified_at: false
redirect_from:
  - /2009/02/update-to-lenny.html
---

Now that [Lenny] has been [released] I've updated some machines and found just
one flaw. There is a [`cvsd`] installation which has been extended with an
[OpenSSH] server. After the upgrade the server refused the connection. Enabling
debugging output showed:

```text
sshd[...]: fatal: ssh_selinux_getctxbyname: ssh_selinux_getctxbyname: security_getenforce() failed
```

in the log. Searching the web a bit revealed, that the CHROOT now needs a
mounted `/proc`. Done and everything works :)

[Lenny]: https://www.debian.org/releases/lenny/
[released]: https://www.debian.org/News/2009/20090214
[`cvsd`]: {% include pkg name="cvsd" %}
[OpenSSH]: {% include pkg name="openssh-server" %}

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
