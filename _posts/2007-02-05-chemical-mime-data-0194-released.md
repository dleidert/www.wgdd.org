---
lang: en
title: `chemical-mime-data` 0.1.94 released
date: '2007-02-05T02:00:00.000+01:00'
category:
  - software
  - planet-debian
tags:
  - chemical-mime
  - english
  - software
  - chemistry
last_modified_at: '2015-02-11T21:05:54.151+01:00'
---

Today I [released] a new version of the [chemical-mime-data] package, namely
**0.1.94**. This version adds and improves support for various chemical MIME
types (see below). It fixes several build issues and improves some detection
and build stuff. The [RH bug #225095] ([SF.net bug #1616568]) has been fixed.
The TODO list is now also a little bit shorter, because several items (source
and package documentation) have been done with this release too.

This version adds support for:

* chemical/x-cactvs-ascii
* chemical/x-cactvs-binary
* chemical/x-cactvs-table
* chemical/x-cdxml
* chemical/x-gamess-output
* chemical/x-gulp
* chemical/x-ncbi-asn1
* chemical/x-ncbi-asn1-binary
* chemical/x-ncbi-asn1-xml

Support has been improved for:

* chemical/x-cdx
* chemical/x-cml
* chemical/x-cif
* chemical/x-dmol
* chemical/x-gamess-input
* chemical/x-gaussian-input
* chemical/x-gaussian-log
* chemical/x-genbank
* chemical/x-hin
* chemical/x-inchi
* chemical/x-inchi-xml
* chemical/x-mdl-rxnfile
* chemical/x-mmcif
* chemical/x-mol2
* chemical/x-msi-car
* chemical/x-msi-hessian
* chemical/x-msi-mdf
* chemical/x-msi-msi
* chemical/x-pdb
* chemical/x-shelx

The full release changelog can found at the [SF.net project site].

An updated Debian package will be available soon in the *experimental* tree
(not in *sid* because of the release freeze).

[released]: https://sourceforge.net/project/showfiles.php?group_id=159685
[chemical-mime-data]: http://chemical-mime.sourceforge.net/
[RH bug #225095]: https://bugzilla.redhat.com/225095
[SF.net bug #1616568]: http://sourceforge.net/p/chemical-mime/bugs/1/
[SF.net project site]: http://chemical-mime.svn.sourceforge.net/viewvc/chemical-mime/tags/release_0_1_94/chemical-mime-data/NEWS?revision=120

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
