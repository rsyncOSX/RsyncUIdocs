+++
author = "Thomas Evensen"
title = "RsyncUI - a GUI for rsync"
date = "2022-05-17"
tags = ["overview"]
categories = ["general information"]
lastmod = "2021-12-09"
+++

RsyncUI is a pure SwiftUI and Swift based macOS application utilizing the command line tool `rsync` for synchronizing files. It is `rsync` which executes the actual synchronize task. RsyncUI is a GUI only ontop of `rsync`. RsyncUI is signed and notarized by Apple. Apple has verified it for not containing malicious code and digitally signed. 

`rsync` is a file based tool for synchronization of files.

#  Before commenze use of RsyncUI

[RsyncUI](https://github.com/rsyncOSX/RsyncUI/releases) is compiled for **macOS Monterey** and later. See [the changelog](/post/changelog/) for updates. RsyncUI is built as a Universal macOS Binary which means it runs natively on Apple Silicon and Intel based Mac computers.

RsyncUI can be installed by homebrew by command `brew install --cask rsyncui` or by download [the latest version](https://github.com/rsyncOSX/RsyncUI/releases).  If installed by homebrew the shasum is automatically verified. If downloaded from GitHub please verify the shasum.

## Remote servers, passwordless logins and local disks

RsyncUI can synchronize your data to either remote servers on Internet and local LAN, or to local attached disks. If you only want to synchronize data to local disks, connect the external disk and just add the source and destination and you are ready for your first task. 

If you want to synchronize data to remote servers there are some more setup to do. If you already have enabled **passwordless login** by `ssh` you only have to add login id and servername, the source and destination and you are ready.  If you have not enabled  passwordless login there are some more actions requiered before your first task. See chapter *Remote servers* below.

## First time

The first time RsyncUI starts it presents a link to [important](/post/important/) information. There is also info about the latest [version of rsync](/post/rsync/) to install.

{{< figure src="/images/start/firsttask.png" alt="" position="center" style="border-radius: 8px;" >}}

RsyncUI can be used in parallel with RsyncOSX. Catalog for storing configuration files is `$HOME/.rsyncosx/macserialnumber/`. RsyncUI and RsyncOSX does not share the user settings, e.g like enabling version 3.x of rsync has to be set in both apps.

## Aborting a task

Please be aware it is an external task not controlled by RsyncUI which executes the command line tool `rsync`. RsyncUI is monitoring the task for progress and termination. The user can at any time abort a task. Please let the abort to finish and cleanup properly before starting a new task. It might take a few seconds. If not the apps might become unresponsive.

One of many advantages of utilizing `rsync` is that it can restart and continue the synchronize task from where it was aborted.

##  RsyncUI vs RsyncOSX

RsyncUI and RsyncOSX shares most of the code for *the model components*.  The main differences between the two apps are the user interface (UI) and how the UI is built. RsyncUI is deveoped by utilizing **SwiftUI** and Swift.  RsyncOSX is developed by utilizing **Storyboards** and Swift.  Both apps utilizes another great **declarative** library, Combine, developed by Apple and JSON files for storing tasks, logrecords and user configuration. RsyncUI will in the future become the primary application of the two.

| App      | Code | Paradigm | Version 1.0 |
| ----------- | ----------- |   ----------- | ----------- |
| RsyncUI   | SwiftUI, Swift | declarativ  (SwiftUI)     | 6 May 2021 |
| RsyncOSX   | Swift, Storyboard   | imperativ (Swift)    | 14 March 2016 |	

## Disqus

At the bottom of the page you can use Disqus to ask questions, suggest enhancments and report bugs. 

# Ready to start using RsyncUI

## New tasks, verify and synchronize data

After adding [a task](/post/addconfigurations/), within the main view, select the task and choose [dryrun](/post/tasks/) to verify the the output from rsync. A verification of a new task might also be executed by opening the Rsync parameters view, select the task and choose the `Verify` button. 

For more experienced users of rsync, form within the Rsync parameters view, select the new task. Copy and paste the `Synchronize` string into a terminal view. The rsync command includes the `dryrun` parameter as default within this view. **Always** verify, by a `dryrun`,  the result of a **new** task before executing it.

## Remote servers and passwordless logins

There are two ways to setup passwordless logins to a remote server. RsyncOSX supports both. It is **strongly** advised to use ssh and ssh-keys because the traffic is encrypted and it is considered more secure.

### Encrypted protocol by ssh and ssh-keys

Using [ssh-keys](https://wiki.archlinux.org/index.php/SSH_keys) is in general considered more safe than standard password solutions (single factor authentication). Ssh-keys are based upon [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography).

- RsyncUI can assist you [in setting up passwordless logins](/post/ssh/)

Rsync transfer data between client and server by tunneling transfer of data in an encrypted ssh tunnel.

### Not encrypted protocol by rsync daemon

There is also possible to setup RsyncUI utilizing a rsync daemon setup for synchronizing files to remote servers.

- this is a special setup and require [some tweaking](/post/rsyncdaemon/)

Rsync is reading a local file with password information when connecting to the server side rsync daemon. The transfer of data between client and server is not encrypted.

Snapshots is **not** possible with rsync daemon setup.

## Snapshots

[Snapshot is an effective method](/post/snapshots/) for saving previous versions of data and deleted files in case of a restore.

## RsyncUI settings

The user can [tweak some settings in RsyncUI](/post/settings/)

## Parameters to rsync

Rsync has a ton of parameters. In [rsync parameters](/post/rsyncparameters/) you can add your own additional parameters to rsync. There is also a set of default rsync parameters. Default parameters might be deleted if wanted. Default parameters are added to all new tasks.

## Pre and post shell scripts

RsyncUI might execute a [pre and post shell script](/post/shellout/) connected to a task.

## Restore data

Sometimes you might want to [restore some data](/post/restore/).

## Logfile

The `⌘O` shortcut brings up any logging to file. Sometimes `rsync` produces error and output are saved to the logfile for viewing and possible corrections of the task. If `rsync` produces an error RsyncUI will inform about that.

## Config files

Where does RsyncUI save [the files](/post/configfiles/) to permanent storage?
