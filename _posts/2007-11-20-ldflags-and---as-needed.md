---
lang: en
title: LDFLAGS and −−as−needed
date: '2007-11-20T20:04:00.000+01:00'
category:
  - debian
  - planet-debian
tags:
  - english
  - debian
  - packaging
  - ld
redirect_from:
  - /2007/11/ldflag-and.html
---

Now that I discovered this nice flag I checked a few of my packages. It works
nice for the [`gnome-chemistry-utils`] application packages. Unfortunately
[`libgcu0`] does not benefit from the flag because of [`libtool`] bug
[`#347650`]. However there is an appreciably difference in the dependencies for
the plugin and application packages where the amount of dependencies
decreased. For example compare the old

```text
Depends: iceweasel | iceape-browser | xulrunner, libart-2.0-2 (>= 2.3.18),
libatk1.0-0 (>= 1.20.0), libc6 (>= 2.6.1-1), libcairo2 (>= 1.4.0),
libgcc1 (>= 1:4.2.1), libgconf2-4 (>= 2.13.5), libgcu0 (<< 0.9),
libgcu0 (>= 0.8), libgl1-mesa-glx | libgl1, libglade2-0 (>= 1:2.6.1),
libglib2.0-0 (>= 2.14.0), libglu1-mesa | libglu1,
libgnomecanvas2-0 (>= 2.11.1), libgnomeprint2.2-0 (>= 2.17.0),
libgnomeprintui2.2-0 (>= 2.17.0), libgnomevfs2-0 (>= 1:2.17.90),
libgoffice-0-4 (>= 0.4.2), libgsf-1-114 (>= 1.14.7), libgtk2.0-0 (>= 2.12.0),
libgtkglext1, libice6 (>= 1:1.0.0), libnspr4-0d (>= 1.8.0.10),
libopenbabel2, liborbit2 (>= 1:2.14.1), libpango1.0-0 (>= 1.18.3), libsm6,
libstdc++6 (>= 4.2.1), libx11-6, libxml2 (>= 2.6.27), libxmu6, libxt6,
zlib1g (>= 1:1.2.3.3.dfsg-1)
```
{: title="Old Depends for gcu-plugin"}

and the new Depends field for [`gcu-plugin`]:

```text
Depends: libc6 (>= 2.6.1-1), libgcc1 (>= 1:4.2.1), libgcu0 (<< 0.9),
libgcu0 (>= 0.8), libglib2.0-0 (>= 2.14.0), libgnomevfs2-0 (>= 1:2.17.90),
libgtk2.0-0 (>= 2.12.0), libnspr4-0d (>= 1.8.0.10), libstdc++6 (>= 4.2.1),
libx11-6, libxml2 (>= 2.6.29), iceweasel | iceape-browser | xulrunner
```
{: title="New Depends for gcu-plugin"}

As another example [`bluefish`] now (the next upload) really only shows the
necessary dependencies. Compare the current:

```text
Depends: libart-2.0-2 (>= 2.3.18), libaspell15 (>= 0.60),
libatk1.0-0 (>= 1.20.0), libbonobo2-0 (>= 2.15.0), libbonoboui2-0 (>= 2.15.1),
libc6 (>= 2.6.1-1), libcairo2 (>= 1.4.0), libfontconfig1 (>= 2.4.0),
libgconf2-4 (>= 2.13.5), libglib2.0-0 (>= 2.14.0), libgnome2-0 (>= 2.17.3),
libgnomecanvas2-0 (>= 2.11.1), libgnomeui-0 (>= 2.17.1), libgnomevfs2-0 (>= 1:2.17.90),
libgtk2.0-0 (>= 2.12.0), libice6 (>= 1:1.0.0), liborbit2 (>= 1:2.14.1),
libpango1.0-0 (>= 1.18.2), libpcre3 (>= 6.0), libpopt0 (>= 1.10), libsm6,
libx11-6, libxcomposite1 (>= 1:0.3-1), libxcursor1 (>> 1.1.2),
libxdamage1 (>= 1:1.1), libxext6, libxfixes3 (>= 1:4.0.1), libxi6, libxinerama1,
libxrandr2 (>= 2:1.2.0), libxrender1
```
{: title="Old Depends for bluefish"}

to the upcoming Depends field:

```text
Depends: libaspell15 (>= 0.60), libc6 (>= 2.7-1), libglib2.0-0 (>= 2.14.0),
libgnomeui-0 (>= 2.17.1), libgnomevfs2-0 (>= 1:2.17.90),
libgtk2.0-0 (>= 2.12.0), libpango1.0-0 (>= 1.18.3), libpcre3 (>= 6.0)
```
{:  title="New Depends for bluefish"}

Nice result. I will check (my) other packages too :) Maybe that's also
something for [debichems] TODO list.

[`gnome-chemistry-utils`]: {% include pkg name="src:gnome-chemistry-utils" %}
[`libgcu0`]: {% include pkg name="libgcu0" %}
[`libtool`]: {% include pkg name="libtool" %}
[`#347650`]: {% include bug is="347650" %}
[`gcu-plugin`]: {% include pkg name="gcu-plugin" %}
[`bluefish`]: {% include pkg name="bluefish" %}
[debichem]: http://debichem.alioth.debian.org/


<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
