+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Synchronize data"
tags = ["synchronize"]
categories = ["synchronize"]
lastmod = "2023-12-18"
+++
Always verify, by a `--dry-run`,  the result of a new task before executing it. The *easiest* way to verify a task, select the task and then the shortcut `⌘E` for estimate.

The main task view lets you execute *all* or *selected* tasks in one go. A *double click* on a task wil execute a `--dry-run`, the *next double click* will execute the real run. 

The following are allowed shortcut actions:

- `Estimate` - `⌘E` estimates all tasks
- `Synchronize` - `⌘R` synchronize all tasks 
- `Abort` - `⌘K` abort and halt any ongoing task

When RsyncUI starts it automatically open the main view. By selecting *wand and stars*  (shortcut `⌘E`) from the toolbar will estimate all tasks.

{{< figure src="/images/tasks/tasks.png" alt="" position="center" style="border-radius: 8px;" >}}

The result of an estimate, blue numbers indicates there is data to synchronize.  Execute the real run either direct from the summarized estimated view or by *left arrow* (shortcut `⌘R`) on the toolbar. To se details from the estimate, select a row and details are presented. 

{{< figure src="/images/tasks/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

Selecting a row presents the details.

{{< figure src="/images/tasks/details.png" alt="" position="center" style="border-radius: 8px;" >}}
