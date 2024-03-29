+++
author = "Thomas Evensen"
title = "RsyncUI - a GUI for rsync"
date = "2023-12-25"
tags = ["overview"]
categories = ["general information"]
lastmod ="2023-12-25"
+++

RsyncUI is a pure *SwiftUI* based macOS application utilizing the command line tool `rsync` for synchronizing files. It is `rsync` which executes the real synchronizing task, not RsyncUI. RsyncUI is a GUI only on top of rsync. RsyncUI is signed and notarized by Apple.  RsyncUI is built for *macOS Sonoma* only.

## Before commencing use of RsyncUI

See [the changelog](/post/changelog/) for updates. RsyncUI is built as a Universal macOS Binary, which means it runs nativly on Apple Silicon and Intel-based Mac computers.  RsyncUI can be installed by Homebrew by command

```bash
brew install --cask rsyncui
```
or by  [download from GitHub](https://github.com/rsyncOSX/RsyncUI/releases). If installed by Homebrew, the shasum is automatically verified. If downloaded from GitHub please verify the shasum.

##  Local attached disks, remote servers and passwordless logins

RsyncUI can synchronize your data to local attached disk, remote servers on the Internet and servers on your local LAN. If you only want to synchronize data to a local attached disk, connect the disk, add source and destination and you are ready for your first task. If you want to synchronize data to a server, on Internet or your local LAN, there is some more setup to do. If you have enabled passwordless login by ssh-keys you only have to add source, destination, login id and servername and you are ready to synchronize. If you have not enabled passwordless login, there are some more actions required before your first task.

## New users

The first time RsyncUI starts, it presents a link to [important](/post/important/) information. There is also info about the [latest version of rsync](/post/rsync/) to install.

{{< figure src="/images/start/firsttask.png" alt="" position="center" style="border-radius: 8px;" >}}

The catalog for [storing configuration](/post/configfiles/) files is `$HOME/.rsyncosx/macserialnumber/`. 

## Aborting a task

Please be aware it is an external task not controlled by RsyncUI, which executes the command line tool `rsync`. RsyncUI is monitoring the task for progress and termination. The user can at any time abort a task. Please let the abort to finish and cleanup properly before starting a new task. It might take a few seconds. If not, the apps might become unresponsive.

## RsyncUI vs RsyncOSX

Which application should I use? **Are you on macOS Sonoma?** Go for RsyncUI. All new development has for the last year been within RsyncUI and will be for the future as well. RsyncOSX is bug fixed only. There is some info about how [RsyncUI is built](/post/built/).

## New tasks, verify task and synchronizing data

After  [adding](/post/addconfigurations/) a task, in the main view,  *a double click* on the task executes a dryrun and the second double click executes the real run. A verification of a new task might also be executed by opening the Rsync parameters view, selecting the task and choosing the Verify button.

For more experienced users of rsync, from within the Rsync parameters view, select the new task. Copy and paste the *synchronization* string into a terminal view. The rsync command includes the `--dry-run` parameter as default within this view. Always verify, by a `--dry-run`, the result of a new task before executing it.
