---
lang: en
title: Etch, sftp and the rssh shell
date: '2007-05-14T23:12:00.000+02:00'
category:
  - debian
  - software
  - planet-debian
tags:
  - english
  - dist-upgrade
redirect_from:
  - /2007/05/etch-sftp-and-rssh-shell.html
---

I discovered an issue. SFTP did not work anymore. The debug session showed:

```console
[..]
debug1: Sending subsystem: sftp
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
debug1: channel 0: free: client-session, nchannels 1
debug1: Transferred: stdin 0, stdout 0, stderr 0 bytes in 0.2 seconds
debug1: Bytes per second: stdin 0.0, stdout 0.0, stderr 0.0
debug1: Exit status 0
```
{: title="console output running sftp debug session"}

The user only has the RSSH (<tt>sftp</tt> enabled) and he is further limited by
the following entry in <tt>.ssh/authorized\_keys</tt>:

```shell
command="/usr/lib/sftp-server" ...key...
```
{: title="excerpt from the user's .ssh/authorized_keys"}

But this doesn't work anymore. <tt>/usr/lib/sftp-server</tt> now is a symlink
to <tt>/usr/lib/openssh/sftp-server</tt> and I had to change the
<tt>.ssh/authorized\_keys</tt> for the user to:

```shell
command="/usr/lib/openssh/sftp-server" ...key...
```

and access is granted again.

## Update

This can be found in <tt>syslog</tt>:

```console
rssh[xxx]: user XXX attempted to execute forbidden commands
rssh[xxx]: command: /usr/lib/sftp-server
```
{: title="excerpt from /var/log/syslog"}

*[SFTP]: Secure FTP (File Transfer Protocol)
*[RSSH]: Restricted shell for use with OpenSSH

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
