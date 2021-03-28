+++
author = "Thomas Evensen"
title = "The Todo list"
date = "2021-03-11"
description = "Todo"
tags = ["todo"]
categories = ["todo"]
lastmod = "2021-03-28"
+++
Updated: 28 March 2021

The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur.

I am using the app it on daily basis myself. From time to time I do a check with RsyncOSX. RsyncUI and RsyncOSX can both be used in parallel, but not at the same time due to locking of files. Also check out the [changelog](/post/changelog/).

[Combine](https://developer.apple.com/documentation/combine) is new and a declarative framework from Apple. I am using it primarly for asynchronous tasks like validate input from the user and listening for (two) notifications from the NotificationCenter. Those two notifications are very important for RsyncUI to work. They must be reliable and whenever they are triggered RsyncUI must catch them.

## What is working

The following is the prerelase:

- the **execution part** of RsyncUI seems to be quite stable, both single and multiple tasks
- administrate the **user settings**
- **delete and update** configurations
- **add** configurations and **create new profiles**
- **add and delete schedules** are working, but there is no link to the schedule app yet.
- **delete logrecords**
- **add and delete parameters** to rsync
- commenced the work on localize RsyncUI to German, Italian and Norwegian

The **error handling** is better in this version. If e.g rsync produces the word `error` in the output,  an alert will inform about it. If a validate of input, when adding new configurations, fails an alert will inform about the error.

## Not yet implemented

The following is **not yet** implemented:

- **restore** of data
- execution of **shellout tasks**, configurations with pre and post shell scripts
- administration of snapshot tasks
- shortcut codes for various tasks
- no start or stop of the menu app for scheduling of tasks
- not yet localized, but prepared for it
- local and remote info about synchronized data
- delete snapshots
