---
vim: tw=79:ts=2:sw=2:ai:si:et
date: 2021-05-05 17:03 +0200
title: Check if secure boot is enabled on your Debian system
description: This command checks if secure boot is enabled on your system.
category:
- planet-debian
- debian
tags:
- mokutils
- secureboot
---
This command checks if your system has secure boot enabled:

```console
$ sudo mokutil --sb-state
```

If it is enabled the output will say

> SecureBoot enabled

otherwise:

> Failed to read SecureBoot

