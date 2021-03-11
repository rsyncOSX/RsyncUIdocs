+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-11"
description = "If you want some more info about RsyncUI there are some resources here."
tags = ["summary"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
RsyncUI is a GUI ontop of the command line utility `rsync`, no more no less. Rsync is a file-based tool for transferring and synchronization of files. RsyncUI supports both synchronize and snapshot tasks. There is no custom solution for the synchronized archive. And you can quit utilizing RsyncUI (and rsync) at any time and still have access to all synchronized files.

- RsyncUI is compiled with support for **macOS Big Sur** only
  - the latest version is [released here](https://github.com/RsyncUI/RsyncUI/releases)
  - RsyncUI can also be installed by homebrew - `brew install --cask RsyncUI`
- RsyncUI is built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

All releases of RsyncUI are [signed and notarized](/post/notarized/). And there [is a short about me](/about).

**THIS SITE IS WORK IN PROGRESS**

## The changelog

There is a [changelog](/post/changelog/). Also please see info about [the latest version of rsync to install.](/post/rsync/)

## A few important words about RsyncUI

Before commencing use of RsyncUI [there are a few important words to read](/post/important/).

## How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires some setup. There are two options to setup [passwordless logins](/post/remotelogins/). The advised setup is by utilizing ssh-keys.

- [setup by ssh-keys](/post/ssh/)
- [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is not possible with [rsync daemon setup](/post/rsyncdaemon/).

## How to add and execute single tasks

It is easy to add a first configuration and execute your first synchronize task.

- [add configurations](/post/addconfigurations/)
- [executing single tasks](/post/singletask/)

## How to add parameters to rsync

Rsync has a ton of parameters. In user selected parameters you can add your own additional parameters to rsync. There is also a set of default rsync parameters.

- [user selected parameters](/post/userparameters/)
- [default parameters](/post/rsyncparameters)

## Snapshots, quick backup and scheduling

Snapshot is an effective method for saving changes and deleted files. You can also execute a group of tasks. If you want to schedule daily or weekly synchronize or snapshot tasks, add a schedule in RsyncUI and execute by the menu app.

- utilizing the [snapshot feature](/post/snapshots/)
- utilizing the [quick synchronize feature](/post/quickbackup/)
- [scheduling of tasks](/post/scheduletasks/)

## How to restore

Sometimes you need to restore files. Either execute [a full restore or file by file](/post/restore/).

## Logging, configuration, config files, check

There are some info about logging and where RsyncUI store files. There are a few user selected options. And sometimes you should execute a verify of synchronized files.

- some info about [logging execution of tasks](/post/logging/)
- some info about [user configuration](/post/userconfiguration/)
- where does RsyncUI [stores the config files](/post/configfiles/)
- how to [check synchronized data](/post/check/)

## Compile

And there is some info about [how to compile RsyncUI](/post/compile/).
