---
vim: tw=79:ts=2:sw=2:ai:si:et
title: Toshiba Tecra A10 (PTSB5E) - Part II
description: >
  I recently bought a new Toshiba laptop model Tecra A10 (PTSB5E) which comes
  without any operating system. Naturally I went for installing a recent Debian
  Squeeze. Parts of the laptop worked out of the box without any further
  customization. Some parts needed manual work and a few things are still
  untested. This is the second post of the series and describes how to enable
  Bluetooth and Virtualization technologies.
date: '2009-11-26T21:21:00.000+01:00'
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
last_modified_at: '2015-02-11T21:17:59.830+01:00'
redirect_from:
- /2009/11/toshiba-tecra-a10-ptsb5e-part-ii.html
---

So I got a little bit further with my [little toy].

## Bluetooth

Bluetooth works. The packages [`gnome-bluetooth`] and [`bluez`] are installed
and the kernel module `bluetooth` is loaded. <kbd>hciconfig</kbd> reports this:

[`gnome-bluetooth`]: {% include pkg name="gnome-bluetooth" %}
[`bluez`]: {% include pkg name="bluez" %}

```console
# hciconfig
hci0:   Type: USB
        BD Address: XX:XX:XX:XX:XX:XX ACL MTU: 310:10 SCO MTU: 64:8
        UP RUNNING PSCAN
        RX bytes:11354 acl:105 sco:0 events:286 errors:0
        TX bytes:4012 acl:99 sco:0 commands:66 errors:0
```

I tried to connect a SAMSUNG and a NOKIA mobile phone. After enabling
visibility of the phone the `bluetooth-applet` showed the device. However I got
an error saying <samp>The name org.openobex was not provided by any .service
files</samp> when trying to access the mobile device. This was solved by
installing [`obexd-server`] <del>[`obex-data-server`]</del>. Then I was able to access
the phone contents via Bluetooth.

[`obexd-server`]: {% include pkg name="obexd-server" %}
[`obex-data-server`]: {% include pkg name="obexd-data-server" %}


## Virtualization

I recently tried to debug the [`mopac7`][`mopac7`] [build error]. I installed the
[`qemu(-kvm)`] emulator. Loading of the `kvm_intel` module failed with
<samp>kvm: disabled by bios</samp>. But this was easy to solve by enabling the
Intel virtualization technology in the BIOS: push and hold the <kbd>ESC</kbd>
key during startup until the laptop tells you to press the <kbd>F1</kbd> key.
Then enable the related BIOS option and you are done.

[little toy]: {% link _posts/2009-11-03-toshiba-tecra-a10-ptsb5e-part-i.md %}
[`mopac7`]: {% include pkg src="mopac7" %}
[build error]: {% include bts bug="517707" %}
[`qemu(-kvm)`]: {% include pkg name="qemu-kvm" %}
