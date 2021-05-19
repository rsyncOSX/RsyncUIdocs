+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Encrypted task"
tags = ["encrypt"]
# categories = ["general information"]
description = "How to execute an encrypted copy of data"
lastmod = "2021-03-11"
+++
Rclone is a command line tool to manage files on cloud storage. It can be installed by homebrew or download and install from [Rclone](https://rclone.org/).
```
brew install rclone
```
This guide is not a verification of how strong encryption of data in rclone is or how to setup encryption by rclone. This guide is how to connect a shell script for encrypting data **ahead** of synchronize the encrypted data to a remote server. The shell script encrypts and copy the encrypted data from `/Users/thomas/Documents` to a new local catalog which I have named `/Users/thomas/rcloneencrypted`. Rclone reads the destination and encryption keys from the rclone config file with label `localencrypt`. I have also some exludes which rclone reads from a text file, just like rsync.

The shell script:

```
#!/bin/bash
/usr/local/bin/rclone sync /Users/thomas/Documents  localencrypt: --exclude-from=/Users/thomas/Documents/excludersync/exclude_rclone.txt
```

## How to connect?

In RsyncUI, the connection with the shell script and rsync task is done in the Configurations view. The task is selected and the path for the shell script is set in pre task and enabled.

![](/images/enryptedtask/encryptedtask.png)

There are some limitations with execute shell scripts in RsyncUI. The only way to execute the shell script is select the `Now` button. Any other task just executes the rsync task and not the shell script.

By selecting the `Now` button executes the shell script. RsyncUI waits until the shell script is completed and then executes the rsync task.

![](/images/enryptedtask/encryptedtask2.png)

The above setup does the following when `Now` is selcted:

- the shell script encrypt and copy new files from my Documents catalog to the encrypted catalog on my local disk
- RsyncUI, after the shell script is executed, synchronize data from the encrypted catalog to a remote server
