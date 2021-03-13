+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "User configuration"
tags = ["userconfig"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
In this view you can let RsyncUI assist in creating ssh-keys and setup global ssh keypath and identityfile, either utilizing default values or set your own. If utilizing default values, [see info about ssh](/post/ssh/).

![](/images/usersettings/ssh.png)

## Local ssh keys found

If `on` RsyncUI has found local ssh keys.

Default values for ssh are `~/.ssh/id_rsa` and portnumber `22`. It is **not required** to set your own values for key path and identityfile if default values are used.

If there are no local ssh keys selecting the `Create` button will create the keys. If ssh keys are found, either default values or by the user set keypath and identityfile, RsyncUI will mark it.

**Caution:** if setting your own values for keypath and identityfile save the values before creating new keys. Creating keys will adding output from the process in the logfile.

Creating default ssh keys.
![](/images/usersettings/ssh3.png)
Creating ssh keys in user set keypath and identityfile.
![](/images/usersettings/ssh4.png)

## Set ssh keypath and identityfile

The user can set a selected ssh keypath and identityfile which applies to all configurations.

- portnumber, which ssh communicates through
- keypath + identityfile, user selected if other than default

If **global values** are set, this is what the ssh parameter within the rsync command looks like.

`-e  "ssh -i ~/.ssh_rsyncosx/rsyncosx -p NN"` where:

- `-i` is the ssh keypath and identityfile
- `-p` is the port number ssh communicates through, default port 22

If global ssh parameters are set, it applies to **all configurations**. It is possible to set other ssh values on each task.

Choosing the `Verify` button present view for copy and paste commands into a terminal view.

![](/images/usersettings/ssh2.png)