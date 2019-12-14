---
title: Network doesn't come up after update to udev 0.140
date: '2009-03-31T21:01:00.000+02:00'
tags:
  - bug
  - debian
  - software
last_modified_at: false
redirect_from:
  - /2009/03/network-doesnt-come-up-after-update-to.html
---

The recent update to `udev 0.140-1` leads to a system without network access to
me. The error messages were:

```console
Running 0dns-down to make sure resolv.conf is ok...done.
Setting up networking....
Configuring network interfaces...
ioctl[SIOCGIFFLAGS]: No such device
Could not get interface 'ath0' flags
ioctl[SIOCSIWPMKSA]: No such device
ioctl[SIOCSIWMODE]: No such device
Could not configure driver to use managed mode
ioctl[SIOCGIWRANGE]: No such device
ioctl[SIOCGIFINDEX]: No such device
ioctl[SIOCSIWENCODEEXT]: No such device
ioctl[SIOCSIWENCODE]: No such device
ioctl[SIOCSIWENCODEEXT]: No such device
ioctl[SIOCSIWENCODE]: No such device
ioctl[SIOCSIWENCODEEXT]: No such device
ioctl[SIOCSIWENCODE]: No such device
ioctl[SIOCSIWENCODEEXT]: No such device
ioctl[SIOCSIWENCODE]: No such device
ioctl[SIOCSIWAP]: No such device
ioctl[SIOCGIFFLAGS]: No such device
wpa_supplicant: /sbin/wpa_supplicant daemon failed to start
/etc/network/if-pre-up.d/wpasupplicant exited with return code 1
SIOCSIFADDR: No such device
ath0: ERROR while getting interface flags: No such device
SIOCSIFNETMASK: No such device
SIOCSIFBRDADDR: No such device
ath0: ERROR while getting interface flags: No such device
ath0: ERROR while getting interface flags: No such device
Failed to bring up ath0.
done.
```

It seems, the update added rules to `/etc/udev/rules.d/70-persistent-net.rules`
by increasing the device number and applying the last applicable NAME directive
instead of the first one. This lead to the following file here:

```
SUBSYSTEM=="net", DRIVERS=="?*", ATTRS{address}=="XX:XX:XX:XX:XX:a7", ATTRS{type}=="1", NAME="ath0"
SUBSYSTEM=="net", DRIVERS=="?*", ATTRS{address}=="XX:XX:XX:XX:XX:18", NAME="eth0"
SUBSYSTEM=="net", DRIVERS=="?*", ATTRS{address}=="XX:XX:XX:XX:XX:XX", NAME="eth1"
# PCI device 0x10ec:0x8139 (8139too)
SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="XX:XX:XX:XX:XX:18", ATTR{type}=="1", KERNEL=="eth*", NAME="eth2"
# PCI device 0x168c:0x0013 (ath_pci)
SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="XX:XX:XX:XX:XX:a7", ATTR{type}=="1", KERNEL=="ath*", NAME="ath1"
```

So the devices created were <code>eth2</code> and <code>ath1</code> but
`/etc/network/interfaces` contained entries for <code>eth0</code> and
<code>ath0</code>. So I fixed `/etc/udev/rules.d/70-persistent-net.rules` and
rebooted.

**&lt;rant&gt;Is it really necessary to break network access with an
update???&lt;/rant&gt;**

## Update

I forgot this one: [#521521].

[#521521]: {% include bts bug="521521" %}

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
