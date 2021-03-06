+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Remote servers and passwordless logins"
tags = ["passwordless"]
# categories = ["remotelogins"]
description = "There are two ways to setup passwordless logins to remote servers."
lastmod = "2021-03-10"
+++
There are two ways to setup passwordless logins to a remote server and RsyncUI supports both. It is advised to use ssh and ssh-keys because the traffic is encrypted and it is considered more secure.

## Encrypted protocol by ssh and ssh-keys

Using [ssh-keys](https://wiki.archlinux.org/index.php/SSH_keys) is in general considered more safe than standard password solutions (single factor authentication). Ssh-keys is based upon [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography).

- RsyncUI can assist you [in setting up passwordless logins](/post/ssh/)

Rsync transfer data between client and server by tunneling transfer of data in an encrypted ssh tunnel.

## Not encrypted protocol by rsync daemon

There is also possible to setup RsyncUI utilizing a **rsync daemon** setup for synchronizing files to remote servers.

- this is a special setup and require some [tweaking](/post/rsyncdaemon/)

Rsync is reading a local file with password information when connecting to the server side rsync daemon. The transfer of data between client and server is **not** encrypted.
