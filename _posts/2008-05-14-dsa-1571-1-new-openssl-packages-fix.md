---
title: "[DSA 1571-1] New openssl packages fix predictable random number generator"
date: '2008-05-14T22:54:00.000+02:00'
tags:
  - security
  - debian
  - bug
  - openssl
redirect_from:
  - /2008/05/dsa-1571-1-new-openssl-packages-fix.html
---

Ok [shit] sometimes also happens to Debian users.

Now I read a lot of FUD, flames, arrogant claims and much more bad things,
including blaming of downstream in general.

Well, Debian maintainers are **NOT** upstream authors. Maintainers often care
about a lot more than just 1 package. Now I wonder if one can really expect,
that maintainers know the source code of their packages as good as upstream
authors do? Is this what the user or the Debian project expects from a package
maintainer? I agree that this would be the ideal situation. But how realistic
is it if one maintains 10, 20 or more packages?

Normally users report us issues. We take a look at the source, try to catch the
issue, track it down and fix it. And IMHO in almost all cases this is enough
and it lets us handle several packages. And maybe this is also what happened
here. The maintainer got a report, tracked it down and tried to fix it. It
seems he posted it to the [openssl-dev] list, which is to [my reading]
considered for such questions, and got a positive response. And by fixing it he
made a horrible mistake. But apparently it also seems that the question had
been [discussed earlier] more than just once (I wish, the OpenSSL guys would
have created the [FAQ entry] earlier).

I don't want to blame the maintainer for doing this mistake. We are humans. But
do we need another instance that (periodically) checks (probably only
Debian-specific) patches/changes to security relevent software or do we need
different requirements for maintainers of such software[^1] or should we
simply archive this under &#8220;Shit sometimes happens &#8230; even to
Debian users&#8221;?

[shit]: http://lists.debian.org/debian-security-announce/2008/msg00152.html
[openssl-dev list]: http://marc.info/?l=openssl-dev&amp;m=114651085826293&amp;w=2
[my reading]: http://openssl.org/support/
[discussed earlier]: http://rt.openssl.org/Ticket/Display.html?id=521&amp;user=guest&amp;pass=guest
[FAQ entry]: http://www.openssl.org/support/faq.html#PROG14

[^1]: Consider [`gnupg`] which is currently [almost][almost] [unmaintained][unmaintained]. It also has Debian specific patches applied and I wonder, which skills the new maintainer should or must(?) have (IIRC this question was raised in the linked threads too)?

[`gnupg`]: {% include pkg name="gnupg" qa=true %}
[almost]: http://lists.debian.org/debian-devel/2008/04/msg00476.html
[unmaintained]: http://lists.debian.org/debian-devel/2008/04/msg00602.html

*[IIRC]: If I Remember Correctly
*[IMHO]: In My Humble Opinion

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
