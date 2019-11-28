---
lang: en
title: Let file(1) recognize a chemical MIME type - the next level
date: '2007-02-15T20:26:00.000+01:00'
category:
  - software
  - planet-debian
tags:
  - chemical-mime
  - english
  - chemistry
last_modified_at: '2015-02-11T21:06:10.223+01:00'
redirect_from:
  - /2007/02/let-file1-recognize-chemical-mime-type_15.html
---

As written [earlier], the `file` command may detect chemical MIME types, if you
feed its database with the necessary definition rules. Now check out the
[cmd.magic.mime file] and run the `file` command with

[earlier]: {% post_url 2007-02-13-let-file1-recognize-chemical-mime-type %}
[cmd.magic.mime file]: https://www2.wgdd.de/cmd.magic.mime

```console
$ file -m cmd.magic.mime -i your_test_file.ext
```

for one or more chemical files. The detection is limited to chemical MIME
types, that have magic pattern in the [chemical-mime-data] [database].

[chemical-mime-data]: http://chemical-mime.sourceforge.net/
[database]: http://chemical-mime.svn.sourceforge.net/viewvc/chemical-mime/trunk/chemical-mime-data/src/chemical-mime-database.xml.in?revision=HEAD

The file `cmd.magic.mime` was created via XSLT conversion of the
original [chemical-mime-data] database and can be used for KDE and
*file*(**1**). One of the following package releases (probably *0.1.95*) will provide it.

[chemical-mime-data]: https://packages.debian.org/chemical-mime-data

## Update

Unfortunately this magic.mime file <strong>cannot</strong> be used for KDE. As
[pointed out by David Faure], KDE uses an older syntax that doesn't know e.g.
the <code>search</code> type. So I have to find another solution for KDE or
wait for better days.

[pointed out by David Faure]: http://lists.kde.org/?t=117179560100002&amp;r=1&amp;w=2

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
