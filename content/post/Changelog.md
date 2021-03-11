+++
author = "Thomas Evensen"
title = "The RsyncUI changelog"
date = "2021-03-11"
description = "Changelog"
tags = ["RsyncUI"]
categories = ["changelog"]
lastmod = "2021-03-11"
+++
If you are utilizing a local version of rsync, execute the rsync utility in a terminal window before using RsyncUI. There is a process of granting access for the rsync utility before using it by RsyncUI. MacOS will also ask permission for accessing your home catalog the first time you start RsyncUI. If you also utilize the menu-app (RsyncUIsched), be aware of you might have to force quit RsyncUI the first time you start the menu-app. This is because the macOS asks for permissions when starting the menu-app for the first time and RsyncUI is not closed automatically when starting the menu-app. This might happen only once first time start.

RsyncUI is [signed and notarized](/post/notarized/). Please see info about [the latest version of rsync in install](/post/rsync/).

Using RsyncUI requires some knowledge of `rsync`. The main objective for RsyncUI is to ease the use of `rsync`, not teach macOS users how to use `rsync`. That is beyond the scope of RsyncUI. Setting the wrong parameters to rsync can result in deleted data. And RsyncUI will not stop you for doing so. That is why it is very important to execute a simulated run (`--dry-run`) and inspect what happens before a real run.   

## Prerelase

To be released before Easter 2021.

## Progress of development

The UI will change as the development continues. But the overall structure and navigation will be like the views below. The screenshots and info are updated **10 March 2021**. There will probably be a testversion within a week or two.

## Error handling

The error handling is better in this version. If e.g rsync produces the word `error` in the output,  an alert will inform about it. If a validate of input, when adding new configurations, fails an alert will inform about the error. And so on...

## Start

The default view when starting the app. Select a profile at any time and the app reloads the data. The start might be `Multiple tasks`. The main view informs about which version of rsync is utilized and if JSON or PLIST is used for storing configurations and schedules.

## Multiple tasks

Choose `Estimate` and then `Execute` after estimation is completed. The estimation marks tasks with data for synchronizing. Or just go for all tasks, no estimation and execute direct. An example of how easy it is too create the UI is [the multiple tasks view](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Multipletasks/MultipletasksView.swift). There are approx only 60 lines of code for the layout of the estimation view (below).

The view also includes a **delete function** for configurations.

## Single task

If you want more control, select `Single task`. Choose either `Estimate` and `Execute` or `Now`, which executes without estimation.

## Schedules

Adding schedules and deleting tasks and logs.

The following is work todo:

- some more QA and work is required

## Parameters to rsync and the command

Viewing the actual rsync command and parameters to rsync for one task. The user can (when the app is released) set any parameter to rsync. The `Copy` button copy the actual rsync command (--dry-run) to memory for possible paste it into a terminal view.

The following is work todo:

- administrating parameters to rsync
- setting parameters for backup and backup catalog of changed data before synchronizing
- disable and enable default parameters to rsync

## Add and edit configurations

Within the `Add or edit` menu, either update data about an existing task or add new tasks. The user can change all basic data about a task. The user **cannot** change the above for snapshot tasks.

There is also function for adding profiles.

## Administrate snapshots

RsyncOSX supports snapshot tasks. It is important to administrate (delete) older snapshots not needed. RsyncOSX supports a couple of plans to assist in which snapshoots to keep and which to delete.

The following is work todo:

- delete snapshots

## Not yet implemented

The following is **not yet** implemented:

- **restore** of data
- execution of **shellout tasks**, configurations with pre and post shell scripts
- administration of parameters to rsync
- administration of snapshot tasks
- shortcut codes for various tasks
- no start or stop of the menu app for scheduling of tasks
- not yet localized, but prepared for it
