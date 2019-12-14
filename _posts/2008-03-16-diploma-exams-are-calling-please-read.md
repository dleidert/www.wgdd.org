---
lang: en
title: 'Diploma exams are calling: Please read if you want to NMU my packages'
date: '2008-03-16T22:19:00.000+01:00'
tags:
  - debian
  - packaging
redirect_from:
  - /2008/03/diploma-exams-are-calling-please-read.html
---

Because my diploma exams are getting nearer I have to reduce my contribution to
the Debian project for the next two months (up to mid/end of May). There is
fortunately currently not much to do for me and also no need to NMU [my
packages]. But please read the following notes, if you (still) think there is a
reason for a NMU:

[my packages]: http://qa.debian.org/developer.php?login=daniel.leidert@wgdd.de

## GCC 4.3 transition

**Done**. All related packages have been fixed. My sponsor just needs to upload
[`psicode`] to fix the last outstanding bug.

[`psicode`]: {% include pkg name="psicode" qa=true %}

*PS*: Also the build-twice-in-a-row release goal will be reached by the upload
of the [`apbs`] update by my sponsor.

[`apbs`]: {% include pkg name="apbs" qa=true %}

## gfortran transition

Almost **done**. [`mpqc`] already reached the buildds. [`ghemical`] has been
uploaded, but waits for [`mopac7`] and [`libghemical`] which are in NEW because
of the new library names.

[`mpqc`]: {% include pkg name="mpqc" qa=true %}
[`ghemical`]: {% include pkg name="ghemical" qa=true %}
[`mopac7`]: {% include pkg name="mopac7" qa=true %}
[`libghemical`]: {% include pkg name="libghemical" qa=true %}

[`apbs`] and [`psicode`] already have been transitioned.

## Other bugs

Ok, I've closed almost all relevant bugs in my packages. There are a few
outstanding bugs that should be examined for Lenny and can be fixed in NMUs -
preferable via delayed NMU queue and an information to the [debichem group]:

[debichem group]: http://debichem.alioth.debian.org/

[#420795] `chemical-mime-data`: Unknown media type in type <q>chemical/x-\*</q>
: Upstream bug tracker for shared-mime-info contains some more information, how
to deal with this. Patches/ideas welcome.

[#420795]: {% include bts bug="420795" %}

[#438694] gabedit: Crashes when loading any XYZ format file
: Looks tricky. Maybe an OpenGL issue related to some video card drivers. Not sure.

[#438694]: {% include bts bug="438694" %}

[#442223] openbabel: some connect information lost when convert from pdb to txyz
: Nothing examined yet to solve this bug.

[#442223]: {% include bts bug="442223" %}

[#464867] extrema: conflicts with psi3 package.
: Hope, my team will cover this asap.

[#464867]: {% include bts bug="464867" %}

[#465723] mopac7 &#8212; please do not use g2c.
: There is currently a workaround using f2c to solve this bug. But MOPAC7 has
been written in FORTRAN and we can use `gfortran` and drop `f2c` completely.
See the report for more information. This is something I would like to see in
Lenny.

[#465723]: {% include bts bug="465723" %}

For the [`xmlto`] package it was planned to add the [`dblatex`] toolchain for
PDF/PS/DVI creation because passivetex will very probably never have a comeback
in Debian and `docbook-xsl`/`fop` is not fully main and cannot create DVI
output. In the case you want to help, feel free to add this feature by NMU to
experimental (maybe with version <code>0.0.21~dblatexX.Y</code>). A first patch
is available in bug report [#416622].

[`xmlto`]: {% include pkg name="xmlto" qa=true %}
[`dblatex`]: {% include pkg name="dblatex" qa=true %}
[#416622]: {% include bts bug="416622" %}

## New upstream releases

It is possible that there will be a new upstream release for [`docbook-xsl`] in
the near future. **DO NOT consider uploading it by NMU if you did not test
it!** This upcoming release ships manpage stylesheets which have been rewritten
in large parts. So regressions can be expected. Fortunately Michael Smith and
me agreed that we should test it carefully, **before** the release is done.
Unfortunately I will not have the time to do it. So if you consider uploading
it, please get in contact with Michael (*xmldoc*) and offer your help testing
it. He added (and I hope many Debian packagers and packaging groups will like
that) some kind of [regressions tests]. These tests build the manpages from
several Debian packages: e.g. `samba`, `apt`, `aptitude`, `git`, `fglrx` and
some more. There are further some new supported features, that should be added
to the [manpage example] shipped with the Debian package. I also planned to
split the source package (atm, `docbook-xsl` and `docbook-xsl-doc` tarballs are
merged together for Debian) as soon as `docbook-xsl-ns` is packaged - which I
wanted to do with the next upstream release. So consider all of the above notes
if you plan an NMU to upload a new upstream release and in question, mail me
  and wait for my answer (which will need some days).

[`docbook-xsl`]: {% include pkg name="docbook-xsl" qa=true %}
[regressions tests]: http://docbook.svn.sourceforge.net/viewvc/docbook/trunk/contrib/samples/refentry/
[manpage example]: http://svn.debian.org/wsvn/debian-xml-sgml/packages/docbook-xsl/trunk/debian/examples/foo.1.example_manpage.xml?op=file&amp;rev=0&amp;sc=0%22%22

In all other cases new upstream releases should be easier to handle.

## ITP

All my ITP are delayed. However if you plan to still upload one of these
packages, you should consider the following notes:

`docbook-xsl-ns`
: See the above note about `docbook-xsl` and the source package split.

[HTML-XML-Utils]
: Already in a good shape. But I sent upstream some patches to improve the
manpages. Version 4.6 of the `html-xml-utils` should contain these patches and
this version should be uploaded into Debian. With this version, Bert Bos will
probably also decide, which prefix will be used for the binaries (they have
very generic names atm; the prefix will probably be `hx-` or `hxu-`). Waiting for
this releaes therefor is IMHO a good choice.

[HTML-XML-Utils]: http://www.w3.org/Tools/HTML-XML-utils/

[DocBook 5]
: I already found a problem that need to be addressed in the package: Where to
install its catalog? You will see there is already a catalog file in
`/usr/share/xml/docbook/schema/dtd/` shipped by the [`docbook-xml`]. Now I'm
not sure what to do here. Upstream ships one catalog file for all supported
schemas (RNG, DTD, W3C schema and schematron). So maybe the catalog file can go
into `/usr/share/xml/docbook/schema/`. Really not sure atm. The answer to this
question might affect the Debian XML policy and should be made carefully.

[DocBook 5]: http://www.docbook.org/schemas/5x
[`docbook-xml`]: {% include pkg name="docbook-xml" qa=true %}

## QA work/fixes

Several lintian warnings have already been fixed in the SVN repositories used
for my packages but have not yet been uploaded.

*I really only plan to reduce my work during the preparation and the exams. So
whatever you do, please try to make it easy for me to continue my packaging
work after the exams :)*

*[NMU]: Non Maintainer Upload
*[ITP]: Intent to Package
*[SVN]: Subversion
*[QA]: Quality Assurance

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
