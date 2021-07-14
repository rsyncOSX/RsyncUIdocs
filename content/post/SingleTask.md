+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Execute single tasks"
tags = ["single task"]
# categories = ["synchronize"]
description = "Execute single task, first a verify run and then the real run."
lastmod = "2021-03-10"
+++
Execute single tasks is a two step operation, one for estimation (dry-run) and one for the real task. The output from rsync can be presented after each run.

Estimate and execute might be triggered by shortcuts when view is opened:

- `Estimate` - shortcut `⌘E`
- `Execute` - shortcut `⌘R`

![](/images/singletask/singletask.png)

The following actions are possible within this view:

- `Estimate` - only estimate the selected tasks, view result after estimate is completed
- `Execute` - first it estimates the selected task and then automatically executes the estimate task

The buttons to right:

- `View` - after estimaten, view result
- `Abort` - abort the ongoing task

## Logs

Every time executing a synchronized tasks adds a log record. Either view all logs or logs by configuration.

![](/images/logs/all.png)
![](/images/logs/byconfig.png)
