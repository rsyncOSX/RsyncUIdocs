+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Execute multiple tasks"
tags = ["multiple task","delete tasks"]
# categories = ["synchronize"]
description = "Execute multiple tasks."
lastmod = "2021-03-10"
+++
The multiple tasks view will probably be the most used view after adding the tasks. Select the `Execute` button and let RsyncUI find all tasks with data to be synchcronized. Estimate and execute might be triggered by shortcuts when view is opened.

{{< image src="/images/multipletasks/multipletasks.png" alt="" position="center" style="border-radius: 8px;" >}}

The following actions are possible within this view:

- `Estimate` (shortcut `⌘E`), only **estimate** all tasks, view result after estimate is completed
- `Execute` (shortcut `⌘R`), estimate and execute all tasks with data to synchronize

The buttons to the right:

- `View` - after a estimate run, view result
- `Select` - select tasks for either estimate and execute, or delete
- `Abort` - abort the ongoing task

## Delete

Select a configuration and slide left for delete.

## Logs

Every time executing a synchronized tasks adds a log record. Either view all logs or logs by configuration.

{{< image src="/images/logs/all.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< image src="/images/logs/byconfig.png" alt="" position="center" style="border-radius: 8px;" >}}
