---
title: Writing manual pages in GROFF (1)
date: '2009-09-15T21:56:00.000+02:00'
category:
- planet-debian
- free-software
tags:
- gnu
- groff
- software
- manpage
last_modified_at: '2015-02-11T21:16:57.731+01:00'
redirect_from:
- /2009/09/writing-manual-pages-in-groff-1.html
---

I always wanted to write a short howto for Debian package maintainers, how to
write a [manual page in GROFF]. This is useful for short documents. For longer
documents, DocBook and docbook-xsl can be a good choice. I already have written
some parts. However, here is the first part of hints. More might follow later.

[manual page in GROFF]: https://www.schweikhardt.net/man_page_howto.html

## The delimiter in the NAME section

The name section is (probably) the only place, where [exactly one] hypen-minus
[`\-`] must appear. The hyphen-minus is the delimiter between the command name
and a one-line description.

[exactly one]: https://lintian.debian.org/tags/hyphen-used-as-minus-sign.html
[`\-`]: https://www.gnu.org/software/groff/manual/html_node/Using-Symbols.html#index-_005c_002d-1

```
.SH NAME
foo-bar \- foos the template foo-what-bar
```

## Typical mistakes regarding paragraphs

Using a [`.PP`] macro directly following a [`.SH`] or [`.SS`] macro is useless.
This macro should be used between paragraphs:

[`.PP`]: https://www.gnu.org/software/groff/manual/html_node/Man-usage.html#index-_002ePP
[`.SH`]: https://www.gnu.org/software/groff/manual/html_node/Man-usage.html#index-_002eSH
[`.SS`]: https://www.gnu.org/software/groff/manual/html_node/Man-usage.html#index-_002eSS

```
.SH OPTIONS
The program follows the usual GNU command line syntax, with long options starting with
two dashes (`\-').
.PP
A summary of options is included below.
```

## Options/File descriptions

To describe options or files it's usually useful to make use of the [`.TP`]
macro.

[`.TP`]: https://www.gnu.org/software/groff/manual/html_node/Man-usage.html#index-_002eTP

```
.SH OPTIONS
.TP
.B \-f, \-\-force
Force the execution of the specified command.
```

```
.SH FILES
.TP
.I ~/.foobar
Per user configuration file.
```

To create more than one intended paragraph the [`.IP`] macro can be used.

[`.IP`]: https://www.gnu.org/software/groff/manual/html_node/Man-usage.html#index-_002eIP

```
.TP
.B \-f, \-\-force
Force the execution of the specified command.
.IP
This option has no effect in conjunction with \fB\-\-foo\fP.
```

## Avoid hyphenation in URLs/URIs/paths

Usually we don't want URLs or URIs to be hyphenated. This can be done using the
[`\%`] sequence. Typical examples:

[`\%`]: https://www.gnu.org/software/groff/manual/html_node/Manipulating-Hyphenation.html#index-_005c_0025-1

```
A short tutorial is available online at \fI\%https://foo.tld/some/path/here/manual.html\fP.
```

```
On a Debian system the complete text of the GNU General Public License
version 2 can be found in the file \fI\%/usr/share/common-licenses/GPL\-2\fP.
```

## Referencing persons and their mail address

The common markup is to write the person name in bold letters and the mail
address in roman letters is put into angle brackets. It's usually a good idea
to mark where the mail address starts and ends. We can use the [`\&amp;`]
sequence as shown in the following example:

[`\&amp;]: https://www.gnu.org/software/groff/manual/html_node/Ligatures-and-Kerning.html#index-_005c_0026-1

```
\fBDaniel Leidert\fP &lt;\&amp;daniel.leidert@wgdd.de\&amp;&gt;
```

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
