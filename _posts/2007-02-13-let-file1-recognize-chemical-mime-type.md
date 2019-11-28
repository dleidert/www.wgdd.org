---
lang: en
title: Let file(1) recognize a chemical MIME type
date: '2007-02-13T08:12:00.000+01:00'
category:
  - software
  - planet-debian
tags:
  - chemical-mime
  - english
  - software
  - chemistry
last_modified_at: '2015-02-11T21:06:03.082+01:00'
redirect_from:
  - /2007/02/let-file1-recognize-chemical-mime-type.html
classes: wide
---

Ok, it's 8 o'clock in the morning and I need some sleep. But first let's show
you some small example, how to detect chemical MIME types with the file(1)
command. Put the following stuff into your `/etc/magic` (the local magic data configuration file for the file(1) command):

```shell
0               string          VjCD0100                CDX binary file
>8              belong          0x04030201
>>12            bequad          0x0000000000000000
>>>20           beshort         0x0000
>>>>34          string          ChemDraw                written with ChemDraw
>>>>>42         string          x                       b%.4s
>>>>22          beshort         0x0080                  (new format)
>>>>22          beshort         0x0000                  (old format)
```
{: title="/etc/magic"}

Now search for a *CDX* (ChemDraw binary) file and run the file command:

```console
$ find . -name "*.cdx" -exec file "{}" ";"
./example.cdx: data (that's really broken)
./dummy.cdx: lif file (that's a CACTVS file in reality)
./x-chemdraw/structures25-27.cdx: CDX binary file written with ChemDraw 4.5 (old format)
./x-chemdraw/structures96-101.cdx: CDX binary file written with ChemDraw 4.5 (old format)
./x-chemdraw/structures40-48.cdx: CDX binary file written with ChemDraw 4.5 (old format)
./x-chemdraw/dimethylamine.cdx: CDX binary file written with ChemDraw 7.0 (old format)
./x-chemdraw/dimethylaminesimple.cdx: CDX binary file (old format)
./x-chemdraw/untitled.cdx: CDX binary file written with ChemDraw 8.0 (new format)
./x-chemdraw/structures1-12.cdx: CDX binary file written with ChemDraw 4.5 (old format)
```

Why I do this? The [chemical-mime-data](http://chemical-mime.sf.net/) package
contains magic pattern, that can be used to automatically create the rules for
the file command too, so *file*(**1**) can determine the chemical MIME type
too. Expect a stylesheet to extract this information from the database soon.

And now I will get some sleep.

## Update

And here, how to recognize the MIME type. Add the following to
`/etc/magic.mime`:

```shell
0               string          VjCD0100
>8              belong          0x04030201
>>12            bequad          0x0000000000000000
>>>20           beshort         0x0000
>>>>22          beshort         0x0080                  chemical/x-cdx
>>>>22          beshort         0x0000                  chemical/x-cdx
```
{: title="/etc/magic.mime"}

and run the *file*(**1**) command with the `-i` switch:

```console
$ find . -name "*.cdx" -exec file -i "{}" ";"
./example.cdx: application/octet-stream
./dummy.cdx: application/octet-stream
./x-chemdraw/structures25-27.cdx: chemical/x-cdx
./x-chemdraw/structures96-101.cdx: chemical/x-cdx
./x-chemdraw/structures40-48.cdx: chemical/x-cdx
./x-chemdraw/dimethylamine.cdx: chemical/x-cdx
./x-chemdraw/dimethylaminesimple.cdx: chemical/x-cdx
./x-chemdraw/untitled.cdx: chemical/x-cdx
./x-chemdraw/structures1-12.cdx: chemical/x-cdx
```

And now I really get some sleep. Cheerio!

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
