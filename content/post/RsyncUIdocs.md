+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-13"
description = "If you want some more info about RsyncUI, please start here"
tags = ["summary"]
# categories = ["general information"]
lastmod = "2021-03-14"
+++
RsyncUI is a SwiftUI based GUI on top of the command line utility `rsync` which is a file based tool for synchronization of files. RsyncUI is [signed and notarized](/post/notarized/) and built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

- RsyncUI is built with support for **macOS Monterey**
- the latest [release for download](https://github.com/rsyncOSX/RsyncUI/releases)

The first time RsyncUI is started the Welcome message is presented. Please read the info and when ready to add tasks select the Dismiss button which opens the [add a configuration](/post/addconfigurations/) view. Before commencing use of RsyncOSX there are a few [important words to read](/post/important/).

{{< image src="/images/start/firsttask.png" alt="" position="center" style="border-radius: 8px;" >}}

## The changelog

There is a [changelog](/post/changelog/). Also please see info about [the latest version of rsync](/post/rsync/) to install.

RsyncUI can be used in **parallel with RsyncOSX**. Default catalog for storing configuration files is:

```bash
$HOME/.rsyncosx/macserialnumber/
```
RsyncUI and RsyncOSX **does not** share the user settings, e.g like enabling version 3.x of rsync has to be set in both apps.

## Synchronize data

How to synchronize data or just execute a quick task.

- execute a synchronize data [task](/post/tasks/)
- execute a [quick task](/post/quicktask/)

## How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires setup of remote connection as [passwordless logins](/post/remotelogins/). There are two options for setup. The advised setup is by utilizing ssh-keys.

- by [ssh-keys](/post/ssh/)
- by [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is **not** possible with rsync daemon setup.

## How to add and update configurations

It is easy to [add and update configurations](/post/addconfigurations/).

## RsyncUI settings

The user can [tweak some settings in RsyncUI](/post/settings/)

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

The `⌘O` shortcut brings up any logging to file. Sometimes `rsync` produces error and output are saved to the logfile for viewing and possible corrections of the task. If `rsync` produces an error RsyncUI will inform about that.

## Config files

Where does RsyncUI save [the files](/post/configfiles/) to permanent storage?

# Development

The target for RsyncUI is macOS Monterey. There is more info about [the development](/post/development/) of RsyncUI.

# Encrypted backup?

There is a short guide [how to use RsyncUI to synchronize encrypted data](/post/encryptedtask/) to a remote server.
