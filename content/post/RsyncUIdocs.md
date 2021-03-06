+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-13"
description = "If you want some more info about RsyncUI, please start here"
tags = ["summary"]
# categories = ["general information"]
lastmod = "2021-03-14"
+++
This is the documentation of the new and SwiftUI based app **RsyncUI**. There is a [changelog](/post/changelog/), please check it before commencing the use of RsyncUI. There is also some [important info](/post/important/) about using RsyncUI.

- RsyncUI is built with support for **macOS Monterey**
- the latest [release for download](https://github.com/rsyncOSX/RsyncUI/releases)

RsyncUI is [signed and notarized](/post/notarized/) and built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

# Development

The target for RsyncUI is macOS Monterey. There is more info about [the development](/post/development/) of RsyncUI.

# Using RsyncUI

RsyncUI can be used in **parallel with RsyncOSX**. Default catalog for storing configuration files is:

```bash
$HOME/.rsyncosx/macserialnumber/
```

RsyncUI and RsyncOSX **does not** share the user settings, e.g like enabling version 3.x of rsync has to be set in both apps.

## The main menu

This is the default view when starting the app. RsyncUI can store configurations in profiles. If you are new til RsyncUI, please start with select the `Configurations` task to [add a configuration](/post/addconfigurations/).

![](/images/start/start.png)

## How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires setup of remote connection as [passwordless logins](/post/remotelogins/). There are two options for setup. The advised setup is by utilizing ssh-keys.

- by [ssh-keys](/post/ssh/)
- by [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is **not** possible with rsync daemon setup.

## How to add and update configurations

It is easy to [add and update configurations](/post/addconfigurations/).

## RsyncUI settings

The user can [tweak some settings in RsyncUI](/post/settings/)

## Execute tasks

How to execute tasks, either multiple tasks, single task or just a quick task.

- execute [multiple tasks](/post/multipletasks/)
- execute a [single task](/post/singletask/)
- execute a [quick task](/post/quicktask/)

## Pre and post shell scripts

RsyncUI might execute a [pre and post shell script](/post/shellout/) connected to a task.

## Restore data

Sometimes you might want to [restore some data](/post/restore/).

## Parameters to rsync

Rsync has a ton of parameters. In [rsync parameters](/post/rsyncparameters/) you can add your own additional parameters to rsync. There is also a set of default rsync parameters.

## Snapshots

[Snapshot is an effective method](/post/snapshots/) for saving previous versions of data and deleted files in case of a restore.

## Verify the synchronized data

Rsync can also verify [the synchronized data](/post/verify/).

## Logfile

The `???O` shortcut brings up any logging to file. Sometimes `rsync` produces error and output are saved to the logfile for viewing and possible corrections of the task. If `rsync` produces an error RsyncUI will inform about that.

## Config files

Where does RsyncUI save [the files](/post/configfiles/) to permanent storage?

## Why backup?

The simple answer is recovery of lost data. There might be several reasons to loosing data, and I will not elaborate why you might risk loosing data. Computer crashes or restore deleted files is one obvious reason. But, there is another reason as well; a recovery from a ransomware attack. I have setup RsyncUI to synchronize, both normal synchronize and snapshots. One server is in house, the second is a remote server somewhere on the Internet. Data synchronized to the remote server is encrypyted before data is synchronized.

Once my configurations are setup, I do backups utilizing RsyncUI every day. So, if I by some reason, has to execute a recovery I know where to find the most updated synchronized data for restore. So, for your own protection, do regularly backups. There are tons of utilities for backups, RsyncUI is one. It is free and it is based on the rock solid utility `rsync`.

There is a short guide [how to use RsyncUI to synchronize encrypted data](/post/encryptedtask/) to a remote server.
