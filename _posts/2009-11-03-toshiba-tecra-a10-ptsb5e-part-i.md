---
vim: tw=79:ts=2:sw=2:ai:si:et
title: Toshiba Tecra A10 (PTSB5E) - Part I
description: >
  I recently bought a new Toshiba laptop model Tecra A10 (PTSB5E) which comes
  without any operating system. Naturally I went for installing a recent Debian
  Squeeze. Parts of the laptop worked out of the box without any further
  customization. Some parts needed manual work and a few things are still
  untested. This is the first post of a series of how to enable all hardware
  parts running the laptop with Debian GNU/Linux.
date: '2009-11-03T21:01:00.000+01:00'
category:
- planet-debian
- debian
- software
- hardware
tags:
- toshiba
- tecra
- hardware
- software
- debian
last_modified_at: '2015-02-11T21:17:23.939+01:00'
redirect_from:
- /2009/11/toshiba-tecra-a10-ptsb5e-part-i.html
---

I recently got a Toshiba Tecra [A10-1HU] laptop. This is a series describing my
experiences with this hardware using Debian Sid.

[A10-1HU]: http://www.toshiba.de/discontinued-products/tecra-a10-1hu/

This one comes without any operating system. So I got a recent
testing-netinstall CD-image and ran the installer procedure in expert mode.
Everything went fine and I ended with a shiny Squeeze and kernel 2.6.30.
Because I use Sid as my usual system, my first action was a dist-upgrade to
Sid.

This is what <kbd>lspci -nn</kbd> tells:

```console
00:00.0 Host bridge [0600]: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub [8086:2a40] (rev 07)
00:02.0 VGA compatible controller [0300]: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller [8086:2a42] (rev 07)
00:02.1 Display controller [0380]: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller [8086:2a43] (rev 07)
00:03.0 Communication controller [0780]: Intel Corporation Mobile 4 Series Chipset MEI Controller [8086:2a44] (rev 07)
00:19.0 Ethernet controller [0200]: Intel Corporation 82567LM Gigabit Network Connection [8086:10f5] (rev 03)
00:1a.0 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 [8086:2937] (rev 03)
00:1a.1 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #5 [8086:2938] (rev 03)
00:1a.2 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #6 [8086:2939] (rev 03)
00:1a.7 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 [8086:293c] (rev 03)
00:1b.0 Audio device [0403]: Intel Corporation 82801I (ICH9 Family) HD Audio Controller [8086:293e] (rev 03)
00:1c.0 PCI bridge [0604]: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 [8086:2940] (rev 03)
00:1c.1 PCI bridge [0604]: Intel Corporation 82801I (ICH9 Family) PCI Express Port 2 [8086:2942] (rev 03)
00:1c.2 PCI bridge [0604]: Intel Corporation 82801I (ICH9 Family) PCI Express Port 3 [8086:2944] (rev 03)
00:1d.0 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 [8086:2934] (rev 03)
00:1d.1 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 [8086:2935] (rev 03)
00:1d.2 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 [8086:2936] (rev 03)
00:1d.7 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 [8086:293a] (rev 03)
00:1e.0 PCI bridge [0604]: Intel Corporation 82801 Mobile PCI Bridge [8086:2448] (rev 93)
00:1f.0 ISA bridge [0601]: Intel Corporation ICH9M-E LPC Interface Controller [8086:2917] (rev 03)
00:1f.2 SATA controller [0106]: Intel Corporation ICH9M/M-E SATA AHCI Controller [8086:2929] (rev 03)
01:00.0 Network controller [0280]: Intel Corporation Wireless WiFi Link 5100 [8086:4232]
05:0b.0 CardBus bridge [0607]: Ricoh Co Ltd RL5c476 II [1180:0476] (rev ba)
05:0b.1 FireWire (IEEE 1394) [0c00]: Ricoh Co Ltd R5C832 IEEE 1394 Controller [1180:0832] (rev 04)
05:0b.2 SD Host controller [0805]: Ricoh Co Ltd R5C822 SD/SDIO/MMC/MS/MSPro Host Adapter [1180:0822] (rev 21)
05:0b.3 System peripheral [0880]: Ricoh Co Ltd R5C843 MMC Host Controller [1180:0843] (rev ff)
05:0b.4 System peripheral [0880]: Ricoh Co Ltd R5C592 Memory Stick Bus Host Adapter [1180:0592] (rev 11)
05:0b.5 System peripheral [0880]: Ricoh Co Ltd xD-Picture Card Controller [1180:0852] (rev 11)
```

## Things that worked out-of-the-box:

### Display/Graphics (Intel GMA 4500M HD)

The integrated graphics chipset, an Intel GMA 4500M HD, works with the
[`xserver-xorg-video-intel`] package and the default X.org configuration. No
custom `/etc/X11/xorg.conf` is necessary. The (IMHO non-reflecting?) display
runs with 1280x800 at 60&nbsp;Hz.

[`xserver-xorg-video-intel`]: {% include pkg name="xserver-xorg-video-intel" %}

### Cable network device

The integrated *Intel 82567LM Gigabit Network device* works with the `e1000e`
kernel module. No customization was necessary.

### Touchpad/Trackpoint

The notebook comes with the so called Toshiba Dual Pointing Device a touchpad
(+2 buttons) and a trackpoint (+2 buttons). Both worked without customization.

### Energy savings/Suspend/Resume

[`apmd`] and `[acpid]` handle this. No problems yet. Suspend/Resume works. I did
not yet test (and I'm not sure if I should) `hibernate` and `uswsusp`.

[`apmd`]: {% include pkg name="apmd" %}
[`acpid`]: {% include pkg name="acpid" %}
[`hibernate`]: {% include pkg name="hibernate" %}
[`uswsusp`]: {% include pkg name="uswsusp" %}

### Webcam

The webcam is a *CNA7157* model or at least detected as such. The `video4linux`
modules handle it and the [`cheese`] application produces pictures.

[`cheese`]: {% include pkg name="cheese" %}

### Volume-control wheel

It works. Module and package information will follow as soon as I figure them
out.

## Things that needed customization

### WLAN (Intel WiFi Link 5100)

The notebook comes with an *Intel WiFi Link 5100* device. It does not work
out-of-the-box. Following [this article] I've installed the
[`firmware-iwlwifi`] package and loaded the `iwlagn` (now `iwlwifi`) module.

[this article]: https://wiki.debian.org/iwlwifi
[`firmware-iwlwifi`]: {% include pkg name="firmware-iwlwifi" %}

### Sound (Intel)

For the sound device to work the `snd_hda_intel` module is necessary. Further
the following lines [must be added] to `/etc/modprobe.d/alsa-base.conf`.

[must be added]: https://wiki.ubuntuusers.de/Soundkarten_installieren/HDA

```console
# not sure about the first line, start adding the second only
options snd-cmipci mpu_port=0x330 fm_port=0x388
options snd-hda-intel index=0 model=toshiba position_fix=1
```

## Unsure/Not yet working

### Temperature sensor

After installing [`sensors-applet`] I got two identical temperature displays.
I'm not sure what they show. Anybody an idea how to examine this?

[`sensors-applet`]: {% include pkg name="sensors-applet" %}

### Modem

The notebook comes with an internal modem device:

```console
00:03.0 Communication controller [0780]: Intel Corporation Mobile 4 Series Chipset MEI Controller [8086:2a44] (rev 07)
```

From what I read I need the [`hsfmodem`] or the [`sl-modem`] packages.
**Unfortunately the latest version is [not available for amd64] from the
archive, although it seems to have been [built].**

[`hsfmodem`]: {% include pkg name="hsfmodem" %}
[`sl-modem`]: {% include pkg name="sl-modem" %}
[not available for amd64]: {% include pkg name="sl-modem" %}
[built]: https://buildd.debian.org/pkg.cgi?pkg=sl-modem

## Untested

I did not yet test

* [<del>Bluetooth</del>][Bluetooth] (icon there, kernel module loaded)
* Firewire (kernel module loaded)
* <del>Card-reader (kernel modules loaded)</del> Card reader works

[Bluetooth]: {% link _posts/2009-11-26-toshiba-tecra-a10-ptsb5e-part-ii.md %}

## Summit

This what <kbd>lspci -k -nn</kbd> tells about the used kernel modules:

```
00:00.0 Host bridge [0600]: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub [8086:2a40] (rev 07)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: agpgart-intel
00:02.0 VGA compatible controller [0300]: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller [8086:2a42] (rev 07)
        Subsystem: Toshiba America Info Systems Device [1179:0004]
00:02.1 Display controller [0380]: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller [8086:2a43] (rev 07)
        Subsystem: Toshiba America Info Systems Device [1179:0004]
00:03.0 Communication controller [0780]: Intel Corporation Mobile 4 Series Chipset MEI Controller [8086:2a44] (rev 07)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
00:19.0 Ethernet controller [0200]: Intel Corporation 82567LM Gigabit Network Connection [8086:10f5] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: e1000e
00:1a.0 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 [8086:2937] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: uhci_hcd
00:1a.1 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #5 [8086:2938] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: uhci_hcd
00:1a.2 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #6 [8086:2939] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: uhci_hcd
00:1a.7 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 [8086:293c] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: ehci_hcd
00:1b.0 Audio device [0403]: Intel Corporation 82801I (ICH9 Family) HD Audio Controller [8086:293e] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: HDA Intel
00:1c.0 PCI bridge [0604]: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 [8086:2940] (rev 03)
        Kernel driver in use: pcieport-driver
00:1c.1 PCI bridge [0604]: Intel Corporation 82801I (ICH9 Family) PCI Express Port 2 [8086:2942] (rev 03)
        Kernel driver in use: pcieport-driver
00:1c.2 PCI bridge [0604]: Intel Corporation 82801I (ICH9 Family) PCI Express Port 3 [8086:2944] (rev 03)
        Kernel driver in use: pcieport-driver
00:1d.0 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 [8086:2934] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: uhci_hcd
00:1d.1 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 [8086:2935] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: uhci_hcd
00:1d.2 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 [8086:2936] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: uhci_hcd
00:1d.7 USB Controller [0c03]: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 [8086:293a] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: ehci_hcd
00:1e.0 PCI bridge [0604]: Intel Corporation 82801 Mobile PCI Bridge [8086:2448] (rev 93)
00:1f.0 ISA bridge [0601]: Intel Corporation ICH9M-E LPC Interface Controller [8086:2917] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
00:1f.2 SATA controller [0106]: Intel Corporation ICH9M/M-E SATA AHCI Controller [8086:2929] (rev 03)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: ahci
01:00.0 Network controller [0280]: Intel Corporation Wireless WiFi Link 5100 [8086:4232]
        Subsystem: Intel Corporation Device [8086:1201]
        Kernel driver in use: iwlagn
05:0b.0 CardBus bridge [0607]: Ricoh Co Ltd RL5c476 II [1180:0476] (rev ba)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: yenta_cardbus
05:0b.1 FireWire (IEEE 1394) [0c00]: Ricoh Co Ltd R5C832 IEEE 1394 Controller [1180:0832] (rev 04)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: firewire_ohci
05:0b.2 SD Host controller [0805]: Ricoh Co Ltd R5C822 SD/SDIO/MMC/MS/MSPro Host Adapter [1180:0822] (rev 21)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
        Kernel driver in use: sdhci-pci
05:0b.3 System peripheral [0880]: Ricoh Co Ltd R5C843 MMC Host Controller [1180:0843] (rev ff)
        Kernel driver in use: ricoh-mmc
05:0b.4 System peripheral [0880]: Ricoh Co Ltd R5C592 Memory Stick Bus Host Adapter [1180:0592] (rev 11)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
05:0b.5 System peripheral [0880]: Ricoh Co Ltd xD-Picture Card Controller [1180:0852] (rev 11)
        Subsystem: Toshiba America Info Systems Device [1179:0001]
```


<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
