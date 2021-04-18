+++
author = "Thomas Evensen"
title = "The Todo list"
date = "2021-03-11"
description = "The todo list"
tags = ["todo"]
# categories = ["todo"]
lastmod = "2021-04-12"
+++
Updated: 14 April 2021

The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur.

I am using the app on daily basis myself. From time to time I do a check with RsyncOSX. RsyncUI and RsyncOSX can both be used in parallel, but not at the same time due to locking of files.

# What is in the prerelease

The following is in the prerelase:

- the **execution part** of RsyncUI seems to be quite stable, both single and multiple tasks
- administrate the **user settings**
- **delete and update** configurations
- **add** configurations and **create new profiles**
- **add and delete schedules** are working, but there is no link to the schedule app yet.
- **delete logrecords**
- **add and delete parameters** to rsync
- commenced the work on localize RsyncUI to German, Italian and Norwegian
- added **shortcut codes** for estimating and executing multiple and single tasks
  - `⌘E` shortcut for estimate
  - `⌘R` shortcut for synchronize
- added a **quick task** option, add a source and a destination and go for it
- **restore** of data
- RsyncUI will from **version 0.49 inform** when there is a new update

## In code

Updated 18 April 2021.

The following is in code but not yet in the prerelase, soon to be released as prerelase:

- execution of **shellout tasks**, configurations with pre and post shell scripts
- `RsyncSchedule` - **the menu app for RsyncUI executing scheduled tasks**, is based on current version
  - start and stop of the menu app for scheduling of tasks
  - utilizing Combine in new version
  - utilizing SwiftUI for the few UI

The **error handling** is better in this version. If e.g rsync produces the word `error` in the output,  an alert will inform about it. If a validate of input, when adding new configurations, fails an alert will inform about the error.

# Not yet implemented

The following is **not yet** implemented:

- actual function for **delete** of snapshots

- local and remote info about synchronized data
