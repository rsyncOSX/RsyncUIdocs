+++
author = "Thomas Evensen"
title = "The Todo list"
date = "2021-03-11"
description = "Todo"
tags = ["todo"]
categories = ["todo"]
lastmod = "2021-03-11"
+++
Updated: 18 March 2021

The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur.

---

The prerelease v036(build 10) is now very close, by functions, to the current release of RsyncOSX. But it is still in development and bugs might occur. There are still some major functions missing, but the gap is closing. I am using the prerelase only, and from time to time checking with current release.

---

I am using the app it on daily basis myself. From time to time I do a check with RsyncOSX. RsyncUI and RsyncOSX can both be used in parallel, but not at the same time due to locking of files.

Also check out the [changelog](/post/changelog/).

[Combine](https://developer.apple.com/documentation/combine) is a declarative framework. I am using some of it in RsyncUI, but there is potensial for more use. To understand what Combine is and how to use it takes time and the plan is to use more of it in RsyncUI after the first release. But I need to spend time to learn it now.

## What is working

The **execution part** of RsyncUI seems to be quite stable. The **user settings** are working. **Delete and update** configurations are working. **Adding** configurations and **create new profiles** are working. **Adding and delete schedules** are working, but there is no link to the schedule app yet. **Deleting logrecords** are working.

The **error handling** is better in this version. If e.g rsync produces the word `error` in the output,  an alert will inform about it. If a validate of input, when adding new configurations, fails an alert will inform about the error.

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
- enable rsync daemon setup

## Administrate snapshots

RsyncUI supports snapshot tasks. It is important to administrate (delete) older snapshots not needed. RsyncUI supports a couple of plans to assist in which snapshoots to keep and which to delete.

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
