+++
author = "Thomas Evensen"
title = "RsyncUI - a GUI for rsync"
date = "2023-06-10"
tags = ["overview"]
categories = ["general information"]
lastmod = "2023-06-10"
+++

RsyncUI is a pure *SwiftUI* based macOS application utilizing the command line tool `rsync` for synchronizing files. It is `rsync` which executes the real synchronizing task, not RsyncUI. RsyncUI is a GUI only on top of rsync. RsyncUI is signed and notarized by Apple. There are no third party libraries included in the code. It is thought three source codes not developed by me are included in the code. The third part of the source code is only for support and not critical if removed.

Check out  [the tags](/tags) and [the categories](/categories) for information about other topics not linked to on this page.

## Before commencing use of RsyncUI

RsyncUI is compiled for macOS Monterey and later. See the changelog for updates. RsyncUI is built as a Universal macOS Binary, which means it runs natively on Apple Silicon and Intel-based Mac computers. RsyncUI can be installed by homebrew by command:

```bash
brew install --cask rsyncui
```

or by downloading  [the latest version](https://github.com/rsyncOSX/RsyncUI/releases). If installed by homebrew, the shasum is automatically verified. If downloaded from GitHub please verify the shasum.

## MacOS 13 (Ventura) and later

With every new release of macOS and SwiftUI there are new features only available for the latest version of both. RsyncUI is compiled for macOS12 and later. And double clicking on a row is only available on macOS 13 and later.

Swift 5.9, Xcode 15 and macOS Sonoma (macOS 14) are all in beta. In Swift 5.9, the new `Observable` macro replaces the `@StateObject` propertywrapper. This is a kind of *breaking* change, but the release of RsyncUI when Sonoma is public will be with the @StateObject propertywrapper. But one branch of source was converted to the new macro. The users will not experience any change, the change only matters for developers.

## MacOS 12 Monterey

Buttons are removed from the main view, and functions for estimate, execute, and so on are enabled by the new toolbar. On macOS 12, double-clicking on task is not available. The only way to check the output from an estimation run within the main view on macOS 12 is to estimate all tasks, dismiss the estimated view, and check the output from rsync the i from the toolbar main view.

## Remote servers, passwordless logins and local disks

RsyncUI can synchronize your data to either remote servers on the Internet and local LAN, or to local attached disks. If you only want to synchronize data to local disks, connect the external disk and just add the source and destination and you are ready for your first task. If you want to synchronize data to remote servers there is some more setup to do. If you already have enabled passwordless login by ssh you only have to add login id and servername, the source and destination and you are ready. If you have not enabled passwordless login, there are some more actions required before your first task.

## New users

The first time RsyncUI starts, it presents a link to [important](/post/important/) information. There is also info about the [latest version of rsync](/post/rsync/) of rsync to install.

{{< figure src="/images/start/firsttask.png" alt="" position="center" style="border-radius: 8px;" >}}

RsyncUI can be used in parallel with RsyncOSX. The catalog for storing configuration files is `$HOME/.rsyncosx/macserialnumber/`. RsyncUI and RsyncOSX do not share user settings, e.g, like enabling version 3.x of rsync, has to be set in both apps.

## Aborting a task

Please be aware it is an external task not controlled by RsyncUI, which executes the command line tool `rsync`. RsyncUI is monitoring the task for progress and termination. The user can at any time abort a task. Please let the abort to finish and cleanup properly before starting a new task. It might take a few seconds. If not, the apps might become unresponsive.

## RsyncUI vs RsyncOSX

For the moment, there are more users of RsyncOSX than RsyncUI. But the number of users of RsyncUI is growing. And Apple is clear, SwiftUI, which RsyncUI is developed by, is the future. This means that most of my development is now on RsyncUI. RsyncOSX is still supported, but only issues are fixed and no new features.

RsyncUI and RsyncOSX share most of the code for the model components. The main differences between the two apps are the user interface (UI) and how the UI is built. RsyncUI is developed utilizing SwiftUI. RsyncOSX is developed utilizing storyboards. Both apps utilize another great declarative library, Combine, developed by Apple and JSON files for storing tasks, logrecords and user configuration.

## New tasks; verifying and synchronizing data

After  [adding](/post/addconfigurations/) a task within the main view,  *a double click* on [task](/post/tasks/) executes a dryrun and the second double click executes the real run. A verification of a new task might also be executed by opening the Rsync parameters view, selecting the task and choosing the Verify button.

For more experienced users of rsync, from within the Rsync parameters view, select the new task. Copy and paste the *synchronization* string into a terminal view. The rsync command includes the `--dry-run` parameter as default within this view. Always verify, by a `--dry-run`, the result of a new task before executing it.
