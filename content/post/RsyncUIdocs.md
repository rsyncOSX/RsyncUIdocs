+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2021-03-13"
description = "If you want some more info about RsyncUI, please start here"
tags = ["summary"]
# categories = ["general information"]
lastmod = "2021-03-14"
+++
This is the documentation of the new app **RsyncUI**, the future version of RsyncOSX. There will also later in 2021, be developed a Sandboxed version for release on Apple Mac Store .

The screenshots are updated with release 1.0.0. Some info may be missing, is incorrect or inaccurate. The info will be updated within the next few weeks. If you miss something, please [create an issue](https://github.com/rsyncOSX/RsyncUIdocs/issues) and let me know.

There is a [changelog](/post/changelog/), please check it before commencing the use of RsyncUI. There is also some [important info](/post/important/) about using RsyncUI.

- RsyncUI and RsyncSchedule are compiled with support for **macOS Big Sur** and later
- the latest [release for download](https://github.com/rsyncOSX/RsyncUI/releases)

RsyncUI is [signed and notarized](/post/notarized/) and built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).

### About RsyncOSX

The development of RsyncOSX is frozen. RsyncOSX is stable and only critical bugs will be fixed. It will be avaliable for download in the future, probably to end of 2022. The main focus now is the new release [RsyncUI](https://github.com/rsyncOSX/RsyncUI).

---

# Using RsyncUI

This section is about using RsyncUI. RsyncUI can be used in **parallel with RsyncOSX**. But that requires **RsyncOSX** to be setup to use **JSON files** and that the files for permanent storage is in the same catalog as RsyncUI.

RsyncUI and RsyncOSX **does not** share the user settings, e.g like  enabling version 3.x of rsync has to be set in both apps.

There are some instructions about [how to setup RsyncOSX utilizing JSON](https://rsyncosx.netlify.app/post/json/). The `About` for both RsyncOSX and RsyncUI shows in bottom of view, where the data is saved. Default catalog for storing files is:

```
$HOME/.rsyncosx/macserialnumber/
```
## The main menu

This is the default view when starting the app. RsyncUI can store configurations in profiles. Select a profile at any time and the app reloads the data. If you are new til RsyncUI, please start with select the `Configurations` task [to add a configuration](/post/addconfigurations/).

![](/images/start/start.png)

## How to setup remote servers

Utilizing RsyncUI to synchronize files to remote servers requires setup of remote connection as [passwordless logins](/post/remotelogins/). There are two options for setup. The advised setup is by utilizing ssh-keys.

- [setup by ssh-keys](/post/ssh/)
- [rsync daemon setup](/post/rsyncdaemon/)

Snapshot is **not** possible with rsync daemon setup.

## How to add and update configurations

It is easy to [add a configuration](/post/addconfigurations/) and execute your first synchronize task.

## RsyncUI settings

The user can [tweak some settings in RsyncUI](/post/settings/)

## Execute tasks

How to execute tasks, either multiple tasks, single task or just a quick task.

- [executing multiple tasks](/post/multipletasks/)
- [executing a single task](/post/singletask/)
- [execute quick task](/post/quicktask/)

## Pre and post task

RsyncUI might [execute a pre- and post shell script](/post/shellout/) connected to a task.

## Restore data

Sometimes you might want to [restore some data](/post/restore/).

## Parameters to rsync

Rsync has a ton of parameters. In [rsync parameters](/post/rsyncparameters/) you can add your own additional parameters to rsync. There is also a set of default rsync parameters.

## Snapshots

[Snapshot is an effective method](/post/snapshots/) for saving previous versions of data and deleted files in case of a restore.

## Verify the synchronized data

Rsync can also [verify the synchronized data](/post/verify/).

## Logging of runs

 [The logrecords](/post/logging/) can be viewed either all or by config.

## Logfile

The `⌘L` shortcut brings up any logging to file. Sometimes `rsync` produces error and output are saved to the logfile for viewing and possible corrections of the task. If `rsync` produces an error RsyncUI will inform about that.

---

# Some technical details about RsyncUI

This section is some technical details about RsyncUI.

## The development of RsyncUI

Why is [RsyncUI based on SwiftUI?](/post/development). There is some more [information about the development](/post/developmentdetails/).

## Compile

And there is some info about [how to compile RsyncUI](/post/compile/).

## Sandboxed version

Later in 2021 there will be released [a sandboxed version of RsyncUI](/post/sandboxversion/).

## Config files

Where does RsyncUI [save the files](/post/configfiles/) to permanent storage?

# Why backup?

The simple answer is recovery of lost data. There might be several reasons to loosing data, and I will not elaborate why you might risk loosing data. Computer crashes or restore deleted files is one obvious reason. But, there is another reason as well; a recovery from a ransomware attack. I have setup RsyncUI to synchronize, both normal synchronize and snapshots. One server is in house, the second is a remote server somewhere on the Internet. Data synchronized to the remote server is encrypyted before data is synchronized.

Once my configurations are setup, I do backups utilizing RsyncUI every day. So, if I by some reason, has to execute a recovery I know where to find the most updated synchronized data for restore.

I will never pay someone money to decrypt any data of mine. So, for your own protection, do regularly backups. There are tons of utilities for backups, RsyncUI is one. It is free and it is based on the rock solid utility `rsync`.
