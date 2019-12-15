---
title: Abit AirPace, ath5k and eduroam
date: '2009-04-10T22:05:00.000+02:00'
tags:
  - driver
  - hardware
  - atheros
  - debian
last_modified_at: false
redirect_from:
  - /2009/04/abit-airpace-ath5k-and-eduroam.html
---

I tried to connect my university workstation to the wireless [eduroam] network
on the campus. The workstation was delivered with an *Abit AirPace* wifi card
(probably an *Atheros 5006* chipset). The first thing necessary was the
<code>ath5k</code> kernel module (my first shot using <code>ndiswrapper</code>
didn't work). Both [Debian Lenny] and [Ubuntu intrepid-updates] provide it.

Now there are generally 3 ways to connect to the AP. All making use of
[`wpasupplicant`]. Further the [certificate] (may differ for the universities) is necessary.

## `/etc/wpa_supplicant/wpa_supplicant.conf`

This is [described] at the sites of my university. It's written in German, but
it should still be easy to understand. Let's just mention the snippet for
`/etc/wpa_supplicant/wpa_supplicant.conf`:

```
ctrl_interface=/var/run/wpa_supplicant
ctrl_interface_group=0
eapol_version=2
ap_scan=1
fast_reauth=1

network={
        ssid="eduroam"
        key_mgmt=WPA-EAP
        proto=RSN
        pairwise=CCMP
        group=TKIP
        eap=TTLS
        anonymous_identity="anonymous@tu-dresden.de"
        identity="****@tu-dresden.de"
        password="****"
        ca_cert="/etc/wpa_supplicant/TUD-CACert.pem"
        phase2="auth=PAP"

}
```
{: title="snippet for /etc/wpa_supplicant/wpa_supplicant.conf"}

Instead of the script suggested at the site above, you can also use this
snippet in `/etc/network/interfaces`:

```
auto wlan0
iface wlan0 inet dhcp
        wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```
{: title="snippet for /etc/network/interfaces"}

## `/etc/network/interfaces`

It is also possible to put the values directly into `/etc/network/interfaces`:

```
auto wlan0
iface wlan0 inet dhcp
        wpa-ssid eduroam
        wpa-proto RSN
        wpa-group CCMP TKIP
        wpa-pairwise CCMP TKIP
        wpa-key-mgmt WPA-EAP
        wpa-eap TTLS
        wpa-ca-cert /etc/wpa_supplicant/TUD-CACert.pem
        wpa-phase2 "auth=PAP"
        wpa-anonymous-identity anonymous@tu-dresden.de
        wpa-identity ****@tu-dresden.de
        wpa-password ****
```
{: title="snippet for /etc/network/interfaces using thw wpa values directly"}


## `network-manager`

Here is a screenshot of the authentication dialog:

{% include figure image_path="https://www2.wgdd.de/nm_eduroam.png" alt="Screenshot of the authentication dialog of network-manager" caption="Authentication Dialog of network-manager" %}

So now everybody at the University of Dresden wanting to use **eduroam** should
hopefully be able to configure this connection on his [Debian] or [Ubuntu]
system.

[eduroam]: http://www.eduroam.de/
[Debian Lenny]: http://packages.debian.org/stable/linux-image
[Ubuntu intrepid-updates]: http://packages.ubuntu.com/intrepid-updates/linux-image
[`wpasupplicant`]: {% include pkg name="wpasupplicant" %}
[certificate]: http://www.inf.tu-dresden.de/content/units/frzneu/Dienste/WLAN/TUD-CACert.pem
[described]: http://www.inf.tu-dresden.de/index.php?node_id=2009&amp;ln=en
[Debian]: https://www.debian.org/
[Ubuntu]: https://www.ubuntu.com/

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
