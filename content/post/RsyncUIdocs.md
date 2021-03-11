+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-11"
description = "If you want some more info about RsyncUI there are some resources here."
tags = ["summary"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
This site is the new site for documentation of RsyncUI, the next release of RsyncOSX. Most of the pages are copy of the information from the previous version. The documentation will be updated as the development of next release is progressing.

**THIS SITE IS WORK IN PROGRESS**

RsyncUI is a GUI ontop of the command line utility `rsync`, no more no less. Rsync is a file-based tool for transferring and synchronization of files. RsyncUI supports both synchronize and snapshot tasks. There is no custom solution for the synchronized archive. And you can quit utilizing RsyncUI (and rsync) at any time and still have access to all synchronized files.

- RsyncUI is compiled with support for **macOS Big Sur** only
  - the latest version is [released here](https://github.com/rsyncOSX/RsyncUI/releases)
- RsyncUI is built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

RsyncUI is [signed and notarized](/post/notarized/).There is a [changelog](/post/changelog/) and a [todo list](/post/todo/).

## A few important words about RsyncUI

Before commencing use of RsyncUI [there are a few important words to read](/post/important/).

## The main menu

Tis is the default view when starting the app. RsyncUI can store configurations in profiles. Select a profile at any time and the app reloads the data. The start might be `Multiple tasks`. The main view informs about which version of rsync is utilized and if JSON or PLIST is used for storing configurations and schedules.

![](/images/start/start.png)

## How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires some setup. There are two options to setup [passwordless logins](/post/remotelogins/). The advised setup is by utilizing ssh-keys.

- [setup by ssh-keys](/post/ssh/)
- [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is not possible with [rsync daemon setup](/post/rsyncdaemon/).

## How to add and update

It is easy to add a first configuration and execute your first synchronize task.

- [add configurations](/post/addconfigurations/)

## Execute tasks

How to execute tasks, either multiple tasks or single task.

- [executing multiple tasks](/post/multipletasks/)
- [executing single tasks](/post/singletask/)

## The user configuration

Some info about user settings:

- some info about [the user settings](/post/userconfiguration/)

## How to add parameters to rsync

Rsync has a ton of parameters. In user selected parameters you can add your own additional parameters to rsync. There is also a set of default rsync parameters.

- [user selected parameters](/post/userparameters/)
- [default parameters](/post/rsyncparameters)

## Compile

And there is some info about [how to compile RsyncUI](/post/compile/).
