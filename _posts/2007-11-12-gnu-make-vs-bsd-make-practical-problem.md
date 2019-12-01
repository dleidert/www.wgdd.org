---
lang: en
title: GNU make vs. BSD make - a practical problem experience
date: '2007-11-12T21:04:00.000+01:00'
category:
  - planet-debian
  - software
tags:
  - bsd
  - english
  - gnu
  - jailkit
  - make
  - software
redirect_from:
- /2007/11/gnu-make-vs-bsd-make-practical-problem.html
---

I'm currently evaluating Olivier Sessinks [`jailkit`] to maintain a small
[`cvsd`] CHROOT with an included [SSH server]. The `cvsd-buildroot` command
e.g. doesn't handle the [`libpam-modules`] dependency in the CHROOT. So I tried
to update the Debian packaging files included in the `jailkit` source. During
this work I found some issues with the build environment - e.g. no
<var>DESTDIR</var> support and some other stuff (another user [already
complained] that there might be problems with the SUID installation part for
`jk_chrootsh`, `jk_uchroot`, and `jk_procmailwrapper` of the Makefiles).

So I began to check and &#8220;fix&#8221; the Makefiles and the configure
script and then sent everything to Olivier. I did not only add the
<var>DESTDIR</var> variables. I also made use of built-in rules, common
variables (also for implicit rules), etc. to make the Makefiles shorter and
easier to maintain. My fault: I tested everything with [GNU `make`]. But now
Olivier complained, that BSD's make doesn't work anymore. So we began a short
hack session to check for the problems.

My first issue: I had to find some BSD make to test it myself. I found it in
the [`freebsd5-buildutils`] which contains the `freebsd-make` command. Then we
began to check for incompatibilities and that's the result:

## <code>ifdef</code> statements differ in syntax

* GNU `make` uses <code>ifdef <var>VAR</var></code>

* BSD `make` uses <code>.ifdef <var>VAR</var></code>

We replaced the statement with a construct similar to
<var>AM&#95;CONDITIONAL</var>. But we do not use this macro, because it would need
to be shipped in `aclocal.m4`, which is currently not necessary. The code
simply sets a variable <var>foo&#95;TRUE</var> to &#8216;<code># </code>&#8216;
based on a condition check.

```shell
if test "x$my_condition" != "xno" ; then
    AC_SUBST([foo_TRUE], [])
else
    AC_SUBST([foo_TRUE], [# ])
fi
```
{: title="configure.ac"}

Processing `Makefile.in` the variable then gets replaced with the assigned
value. If the value `# ` was assigned, the second line in the following example
would be commented.

```shell
FILES = bar
@foo_TRUE@FILES += foo
```
{: title="Makefile.in"}

becomes:

```shell
FILES = bar
# FILES += foo
```
{: title="Makefile"}

in the final `Makefile`.

## prerequisite variables differ in syntax

* GNU `make` uses <code>$&lt;</code>, <code>$^</code>, <code>$@</code>, ...

* BSD `make` uses <code>${.IMPSRC}</code>, <code>${.ALLSRC}</code>,
  <code>${.TARGET}</code>, ... (note, that both <var>	&#42;SRC</var> variables
  hold a **list** of source files)

Unfortunately both `make` implementations don't seem to share a variable for
the list of prerequisites. So the only solution is to list all prerequisites in
the rule again. A variable would be much more comfortable. Maybe one could
write a function which first tests <code>${.IMPSRC}</code> and falls back to
<code>$^</code>. Maybe that's an alternative, but it's IMHO not a very good
solution. We've chosen to write down all prerequisites in a rule instead of
using a variable. This is a little bit harder to maintain, but it works.

## built-in rules are not shared and do not use the same variables

* GNU `make` ships built-in rules to build objects from sources **and** link
  them; rules consider <var>CPPFLAGS</var>

* BSD `make` ships built-in rules to build objects from sources, but there are
  no rules to link them; rules do not consider <var>CPPFLAGS</var>

In the case of GNU `make` one can simply write:

```shell
myprog: foo.o bar.o
```
{: title="Makefile.in"}

and GNU `make` will automatically create `foo.o` from `foo.c` ([`.c.o:`], ditto
for `bar.o`) and at least link `myprog` ([`.o:`]). But BSD `make` will only
create the object files. There is no final link-step. So we had to include
the rule to link the program in the Makefile.

## Conclusion

Finally we got it and it looks good now. I/we learned a lot of new things (I
especially learned a lot about BSD `make`), **but** it took us 1-2 hours to
understand and fix the problems.

Here is a list of URLs that might give some more information about the
programs, their syntax and limitations:

* [GNU `make` manual]
* [FreeBSDs `make`]
* [Autoconf: Limitations of make]

[`jailkit`]: http://olivier.sessink.nl/jailkit/
[`cvsd`]: {% include pkg name="cvsd" %}
[SSH server]: {% include pkg name="openssh-server" %}
[`libpam-modules`]: {% include pkg name="libpam-modules" %}
[already complained]: https://lists.gnu.org/archive/html/jailkit-dev/2007-09/msg00000.html
[GNU `make`]: {% include pkg name="make" %}
[`freebsd5-buildutils`]: {% include pkg name="freebsd5-buildutils" %}
[`.c.o:`]: https://www.gnu.org/software/make/manual/make.html#Catalogue-of-Rules
[`.o:`]: https://www.gnu.org/software/make/manual/make.html#Catalogue-of-Rules
[GNU `make` manual]: https://www.gnu.org/software/make/manual/make.html
[FreeBSDs `make`]: http://www.khmere.com/freebsd_book/html/ch01.html
[Autoconf: Limitations of make]: https://www.gnu.org/software/autoconf/manual/autoconf.html#Portable-Make

*[SSH]: Secure Shell
*[GNU]: GNU is Not Unix
*[BSD]: Berkeley Software Distribution
*[IMHO]: in my humble opinion

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
