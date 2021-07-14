+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Execute multiple tasks"
tags = ["multiple task","delete tasks"]
# categories = ["synchronize"]
description = "Execute multiple tasks."
lastmod = "2021-03-10"
+++
The multiple tasks view will probably be the most used view after adding the tasks. Select the `Execute` button and let RsyncUI find all tasks with data to be synchcronized.  To delete one or more task, select and `Delete`.

Estimate and execute might be triggered by shortcuts when view is opened:

- `Estimate` - shortcut `⌘E`
- `Execute` - shortcut `⌘R`

![](/images/multipletasks/multipletasks.png)

The following actions are possible within this view:

- `Estimate` - only estimate all tasks, view result after estimate is completed
- `Execute` - first it estimates all tasks and then automatically executes all tasks with data to synchronize

The buttons to right:

- `View` - after a estimate run, view result
- `Select` - select tasks for either estimate and execute, or delete
- `Delete` - select a task for delete
- `Abort` - abort the ongoing task

## Logs

Every time executing a synchronized tasks adds a log record. Either view all logs or logs by configuration.

![](/images/logs/all.png)
![](/images/logs/byconfig.png)
