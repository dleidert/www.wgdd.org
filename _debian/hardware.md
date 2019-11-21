---
title: Hardware
Description: >-
  Debian GNU/Linux is running on all my systems. This includes latops from
  Toshiba, Acer and Lenovo, but also Intel- and AMD-based based servers.
  Sometimes a few tweaks are required as described here.
toc: true
---

I'm running several systems with different purposes but all running [Debian
GNU/Linux][debian]. These systems are described below. If necessary I list all
packages and configurations that might be useful to know about when running
such a piece of hardware. Usually I install both free and non-free Linux
firmware packages.

[debian]: http://www.debian.org/

## [ACER Aspire 7 (A717-71G)][AcerAspire7]

> Laptop-Workstation _Vogon_

In late 2018 I got in need for a new and fast laptop.

[AcerAspire7]: https://www.acer.com/ac/de/DE/content/support-product/7297?b=1&pn=NX.GPFEG.007

## [HP N54L][HPN54L]

> Home Theatre PC _HoG (Heart of Gold)_

[HPN54L]: https://h20195.www2.hpe.com/v2/getpdf.aspx/c04111672.pdf?ver=28

## [Lenovo ThinkPad Yoga 11e (Type 20DA)][Lenovo11e]

> Laptop-Workstation _Beeblebrox_

I decided for this model because it is handy, robust, light enough and provides
a good battery time (more than 5 hours). It also has a touchscreen. If I could
change one or two things, I'd have preferred a matt display instead of the
shiny one and one more USB port. As usual I decided for a model that only uses Intel hardware, so I can be sure, that it is well supported by Linux (even the touchscreen works). Basically the following packages are needed:

* [intel-microcode][intel-microcode] (Kernel),
* [libdrm-intel1][libdrm-intel1] (`drm` module),
* [xserver-xorg-video-intel][xserver-xorg-video-intel] (X.org server),
* [firmware-iwlwifi][firmware-iwlwifi] (`iwlwifi` module) and
* [firmware-realtek][firmware-realtek] (Realtek RTL8168 ethernet device),

together with the usual kernel, firmware and video driver stuff. There is not
much manual configuraion necessaryto `/etc/modules`:

```
# detected by sensors-detect
coretemp
```
{: title="contents of the /etc/modules file"}

[Lenovo11e]: https://support.lenovo.com/de/en/solutions/pd100094 "Product description of the Lenovo ThinkPad Yoga 11e (Type 20DA)"
[intel-microcode]: https://packages.debian.org/intel-microcode
[libdrm-intel1]: https://packages.debian.org/libdrm-intel1
[xserver-xorg-video-intel]: https://packages.debian.org/xserver-xorg-video-intel
[firmware-iwlwifi]: https://packages.debian.org/firmware-iwlwifi
[firmware-realtek]: https://packages.debian.org/firmware-realtek

<a href="/tags/#lenovo" class="page__taxonomy-item" rel="tag">lenovo</a>

## [TOSHIBA Tecra A10-1HU (PTSB5E)][ToshibaTecraA10]

> Laptop-Workstation _Haktar (not used anymore)_

This laptop almost only utilizes Intel hardware and comes without any operating
system. Besides the modem and the fingerprint scanner, which I both don't use,
everything is working. So whats basically needed here is

* [libdrm-intel1][libdrm-intel1] (`drm` module),
* [xserver-xorg-video-intel][xserver-xorg-video-intel] (X.org server) and
* [firmware-iwlwifi][firmware-iwlwifi] (Intel WiFi Link 5100, `iwlwifi` module)

together with the usual kernel, firmware and video driver stuff. There is not
much manual configuration necessary to `/etc/modules`:

```
# Bluetooth
toshiba_bluetooth
# FireWire
firewire-sbp2
# detected by sensors-detect
coretemp
```
{: title="contents of the /etc/modules file"}

This Toshiba based laptop might need [toshutils][toshutils] and/or
[toshset][toshset].

When I bought the laptop, the battery held for more than 4 hours in normal
operation. In my opinion, this is quite good. Suspend and sleep modes etc. also
work fine.

**November 2014: ATM I'm suffering from the laptop changing audio mode to
earphones after waking up from suspend. This is weired.**

I got this laptop sponsored partly by the Bluefish project. It was later
donated to a school in Nepal.

<a href="/tags/#tecra" class="page__taxonomy-item" rel="tag">tecra</a>

[ToshibaTecraA10]: http://www.toshiba.de/discontinued-products/tecra-a10-1hu/
[libdrm-intel1]: https://packages.debian.org/libdrm-intel1
[xserver-xorg-video-intel]: https://packages.debian.org/xserver-xorg-video-intel
[firmware-iwlwifi]: https://packages.debian.org/firmware-iwlwifi
[toshutils]: https://packages.qa.debian.org/toshutils
[toshset]: https://packages.qa.debian.org/toshset


# vim: set tw=79 ts=2 sw=2 ai si et:
