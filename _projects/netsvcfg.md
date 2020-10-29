---
title: NetSVCfg
---

The so called [`NetSVCfg`] script was created to turn off the many services
running on a default Windows&nbsp;XP computer. In these days Microsoft enabled
many services by default (they thought this might be more comfortable for
users) although most users didn't need them. Unfortunately several of these
services were open to anyone. After several vulnerabilities had been detected
in the LSASS and in the RPC/DCOM systems two computer worms spread acrosis the
world wide web. They were called [W32.Blaster] and [W32.Sasser] - both capable
of infecting online Windows machines automatically.  During this time a German
manual by Frank Kaune existed in which he described how to turn off
non-essential services and harden the system. The script first was an implementation
of this manual but soon turned off more unneccesary services and eventually
became the role model or blue print of what Microsoft did in the Service Pack 3 for
Windows XP.

I was part of the Usenet in these days and also cared about securing my system
working on optimizing the configuration to run and offer as few services as
possible and not provide services to the outside world. I read a lot of the XP
documentation then to understand which impact it would have to shut down a
service or set it to a manual start (the documentatioin was actually quite
good). So I helped with some minor parts of the script.

The script became obsolete when Microsoft released Servive Pack 3 for Windows
XP in which they changed their policy and shut down services themselves.

[`NetSVCfg`]: https://web.archive.org/web/20080124011130/http://www.ntsvcfg.de/ "Web-Archive Snapshot from 2008"
[W32.Blaster]: https://en.wikipedia.org/wiki/Blaster_(computer_worm)
[W32.Sasser]: https://en.wikipedia.org/wiki/Sasser_(computer_worm)

*[LSASS]: Local Security Authority Subsystem Service
*[RPC]: Remote Procedure Call
*[DCOM]: Distributed Component Object Model

# vim: set tw=79 ts=2 sw=2 ai si et:
