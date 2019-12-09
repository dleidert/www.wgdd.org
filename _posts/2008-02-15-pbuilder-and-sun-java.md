---
lang: en
title: pbuilder and SUN Java
date: '2008-02-15T19:31:00.000+01:00'
tags:
  - packaging
  - java
  - pbuilder
redirect_from:
  - /2008/02/pbuilder-and-sun-java.html
---

[`pbuilder`] with default settings will fail to build a package depending on
[`sun-java5`] or [`sun-java6`] because the license needs to be accepted first.

Now some time ago I saw a patch for `pbuilder` itself to <q>fix</q> this, but
for the time beeing I used to set <var>DEBIAN_FRONTEND</var> to **readline** in
my `pbuilderrc`. But today Michael Koch came up with much better suggestions:
Preset the debconf value in the CHROOT and save it.

It's pretty easy:

```console?prompt=#,$
$ sudo pbuilder login --save-after-login
[..]
# echo "sun-java5-jdk shared/accepted-sun-dlj-v1-1 boolean true" | debconf-set-selections
# echo "sun-java6-jdk shared/accepted-sun-dlj-v1-1 boolean true" | debconf-set-selections
# exit
```
{: title="Sample pbuilder session logging in and pre-setting debconf values"}

and voila, problem solved. Thanks to Michael for the tip.

## Update

Manual Prinz suggested a slightly [different way] which realizes the same
debconf setting, but with hooks.

[`pbuilder`]: {% include pkg name="pbuilder" %}
[`sun-java5`]: {% include pkg name="sun-java5" qa=true %}
[`sun-java6`]: {% include pkg name="sun-java6" qa=true %}
[different way]: http://lists.debian.org/debian-java/2008/05/msg00024.html


<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
