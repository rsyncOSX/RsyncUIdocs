+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-13"
description = "If you want some more info about RsyncUI there are some resources here."
tags = ["summary"]
categories = ["general information"]
lastmod = "2021-03-14"
+++
This site is the new site for documentation of RsyncUI, the next release of RsyncOSX. The documentation will be updated as the development of next release is progressing.

**THIS SITE IS WORK IN PROGRESS**

The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur. There is a [changelog](/post/changelog/) and a [todo list](/post/todo/), please check both before commencing the use of the prerelease.

- RsyncUI is compiled with support for **macOS Big Sur** only
- the latest prerelase (test) is [released here](https://github.com/rsyncOSX/RsyncUI/releases)

RsyncUI is [signed and notarized](/post/notarized/) and it is built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

## The main menu

This is the default view when starting the app. RsyncUI can store configurations in profiles. Select a profile at any time and the app reloads the data. The main view informs about which version of rsync is utilized and if JSON or PLIST is used for storing configurations and schedules.

![](/images/start/start.png)

## How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires some setup. There are two options to setup [passwordless logins](/post/remotelogins/). The advised setup is by utilizing ssh-keys.

- [setup by ssh-keys](/post/ssh/)
- [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is **not** possible with rsync daemon setup.

## How to add and update

It is easy to add a first configuration and execute your first synchronize task.

- [add configurations](/post/addconfigurations/)

## The user configuration

Some info about user settings:

- some info about [the user settings](/post/userconfiguration/)

## Execute tasks

How to execute tasks, either multiple tasks or single task.

- [executing multiple tasks](/post/multipletasks/)
- [executing single tasks](/post/singletask/)

## Log files

The [logfiles](/post/logging/) can bi viewed either all or by config.

## How to add parameters to rsync

Rsync has a ton of parameters. In user selected parameters you can add your own additional parameters to rsync. There is also a set of default rsync parameters.

- [user selected parameters](/post/userparameters/)
- [default parameters](/post/rsyncparameters)

## Compile

And there is some info about [how to compile RsyncUI](/post/compile/).
