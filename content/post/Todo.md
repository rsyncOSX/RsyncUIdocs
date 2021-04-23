+++
author = "Thomas Evensen"
title = "The Todo list"
date = "2021-03-11"
description = "The todo list"
tags = ["todo"]
# categories = ["todo"]
lastmod = "2021-04-21"
+++
Updated: 23 April 2021

The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur.

I am using the app on daily basis myself. From time to time I do a check with RsyncOSX. RsyncUI and RsyncOSX can both be used in parallel, but not at the same time due to locking of files.

# What is in the prerelease

The following is in the prerelase:

- the **execution part** of RsyncUI seems to be quite stable, both single and multiple tasks
- administrate the **user settings**
- **delete and update** configurations
- **add** configurations and **create new profiles**
- **add, stop and delete** scheduled tasks
- **delete logrecords**
- **add and delete parameters** to rsync
- commenced the work on localize RsyncUI to German, Italian and Norwegian
- added **shortcut codes** for estimating and executing multiple and single tasks
  - `⌘E` shortcut for estimate
  - `⌘R` shortcut for synchronize
- added **quick task** option, add a source and a destination and go for it
  - default is a `synchronize` task
  - can also be set as a `syncremote` task, pull data from a remote server
- **restore** of data
- RsyncUI will from **version 0.49 inform** when there is a new update
- execution of **shellout tasks**, configurations with pre and post shell scripts
- `RsyncSchedule` - the menu app for RsyncUI executing **scheduled tasks**
  - it is based on current version
  - start and stop of the menu app for scheduling of tasks
  - utilizing Combine in new version
  - utilizing SwiftUI will be developed sometime later this year

The **error handling** is better in this version. If e.g rsync produces the word `error` in the output,  an alert will inform about it. If a validate of input, when adding new configurations, fails an alert will inform about the error.

# In code but not in prerelease

The release of version 1.0.0 is closing. The following is in code but not in the prerelase:

- view for rsync parameters is reworked into two views
- view for schedules is reworked into two views

# Not yet implemented

The following is **not yet** implemented:

- actual function for **delete** of snapshots
- local and remote info about synchronized data
