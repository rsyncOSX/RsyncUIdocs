+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-13"
description = "If you want some more info about RsyncUI there are some resources here"
tags = ["summary"]
categories = ["general information"]
lastmod = "2021-03-14"
toc = "true"
+++
This is the documentation of the new app RsyncUI, the next and future release of RsyncOSX. My main focus after releasing RsyncUI will be to enhance and continue the development of it. There will also be developed a Sandboxed version of it for release on Apple Mac Store later this year. And there will also be a menu app for executing scheduled tasks.

The documentation will be updated as the development is going forward. The prerelease is a version for **test** and **preview** of what is coming. It is work in progress and bugs might occur.

There is a [changelog](/post/changelog/) and a [todo list](/post/todo/), please check both before commencing the use of the prerelease.

- RsyncUI is compiled with support for **macOS Big Sur** only
- the latest prerelase (test) is [released here](https://github.com/rsyncOSX/RsyncUI/releases)

RsyncUI is [signed and notarized](/post/notarized/) and built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

---
---

## Using RsyncUI

This section is about using RsyncUI.

### The main menu

The default view when starting the app. RsyncUI can store configurations in profiles. Select a profile at any time and the app reloads the data. The main view informs about which version of rsync is utilized and if JSON or PLIST is used for storing configurations and schedules.

The screenshots may be slightly different from what is in the current prerelease. The prerelease is still in development.

![](/images/start/start.png)

### How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires setup of remote connection as [passwordless logins](/post/remotelogins/). There are two options for setup. The advised setup is by utilizing ssh-keys.

- [setup by ssh-keys](/post/ssh/)
- [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is **not** possible with rsync daemon setup.

### How to add and update

It is easy to [add a configuration](/post/addconfigurations/) and execute your first synchronize task.

### RsyncUI settings

The user can [tweak some settings in RsyncUI](/post/settings/)

### Execute tasks

How to execute tasks, either multiple tasks, single task or just a quick task.

- [executing multiple tasks](/post/multipletasks/)
- [executing a single task](/post/singletask/)
- [execute quick task](/post/quicktask/)

### Pre and post task

RsyncUI might [execute a pre- and post shell script](/post/shellout/) connected to a task.

### Restore data

Sometimes you might want to [restore some data](/post/restore/).

### Parameters to rsync

Rsync has a ton of parameters. In [user selected parameters](/post/rsyncparameters) you can add your own additional parameters to rsync. There is also a set of default rsync parameters.

### Verify the synchronized data

Rsync can also [verify the synchronized data](/post/verify/).

### Log files

The [logfiles](/post/logging/) can be viewed either all or by config.

---
---

## Some technical details about RsyncUI

This section is some technical details about RsyncUI.

### Config files

Where does RsyncUI [save the files](/post/configfiles/) to permanent storage?

### The development of RsyncUI

Why is [RsyncUI based on SwiftUI?](/post/development)

### Compile

And there is some info about [how to compile RsyncUI](/post/compile/).
