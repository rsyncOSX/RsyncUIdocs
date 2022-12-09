+++
author = "Thomas Evensen"
title = "How to use RsyncUI"
date = "2022-05-17"
tags = ["overview"]
categories = ["general information"]
lastmod = "2021-12-09"
+++
RsyncUI is a [signed and notarized](/post/notarized/) SwiftUI based GUI on top of the command line utility `rsync`, which is a file based tool for synchronization of files. RsyncUI is built as a Universal macOS Binary which means it runs natively on Apple Silicon and Intel based Mac computers.

- the [latest version](https://github.com/rsyncOSX/RsyncUI/releases) of RsyncUI is compiled for **macOS Monterey** and later
- the [changelog](/post/changelog/)

## First start

The first time RsyncUI is started a Welcome message is presented. Please read the [important words to read](/post/important/) and when ready to add tasks select the Dismiss button which opens the [add a task](/post/addconfigurations/). Also please see info about [the latest version of rsync](/post/rsync/) to install.

{{< image src="/images/start/firsttask.png" alt="" position="center" style="border-radius: 8px;" >}}

RsyncUI can be used in parallel with RsyncOSX. Catalog for storing configuration files is `$HOME/.rsyncosx/macserialnumber/`. RsyncUI and RsyncOSX does not share the user settings, e.g like enabling version 3.x of rsync has to be set in both apps.

### Aborting task

Please be aware it is an external task or process which actually executes the command line tool `rsync`.RsyncUI is monitoring the external task for counting progress and termination. The user can abort a tasks at any time. Please let the abort to finish and cleanup properly before starting a new task. It might take a few seconds. If not the apps might become unresponsive.

One advantage of utilizing `rsync` is that it can restart the synchronize task from where it was aborted.

### How to verify a new task - important

After adding [a task](/post/addconfigurations/), within the main view, select the task and choose `DryRun` button to verify the the output from rsync. A verification of a new task might also be executed by opening the Rsync parameters view, select the task and choose the `Verify` button.

For more experienced users of rsync, form within the Rsync parameters view, select the new task. Copy and paste the `Synchronize` string into a terminal view. The rsync command includes the `dryrun` parameter as default within this view.

## Synchronize data

After [adding a task](/post/addconfigurations/) you are ready to execute your first synchronize data task.

- execute a [synchronize data task](/post/tasks/)
- execute a [quick task](/post/quicktask/)

**Always** verify, by a `dryrun`,  the result of a **new** task before executing it.

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

## Logfile

The `⌘O` shortcut brings up any logging to file. Sometimes `rsync` produces error and output are saved to the logfile for viewing and possible corrections of the task. If `rsync` produces an error RsyncUI will inform about that.

## Config files

Where does RsyncUI save [the files](/post/configfiles/) to permanent storage?
