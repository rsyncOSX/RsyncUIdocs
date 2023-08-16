+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Execute tasks"
tags = ["execute","delete tasks"]
categories = ["synchronize"]
lastmod = "2021-03-10"
+++
After adding new tasks always verify the result of task by either a double click on task or by opening the Rsync parameters view, select the task and choose `Verify`.  The main task view also lets you execute *all* or *selected* tasks in one go. Actions are triggered either by shortcuts or by toolbar. The following are allowed shortcut actions:

- `Estimate` - `⌘E` estimates all tasks
- `Execute` - `⌘R` executes all tasks 
- `show info` - `⌘I`

## All tasks in one go

When RsyncUI starts it automatically open the main view. By selecting *wand and stars*  (shortcut `⌘E`) from the toolbar will estimate all tasks. Execute the real run either direct from the summarized estimated view or by *left arrow* (shortcut `⌘R`). 

{{< figure src="/images/tasks/tasks.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/tasks/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

When a task is estimated the progress column will show  a *green* bullet. Select the task and choose the *i* from toolbar will show the output from rsync. 

{{< figure src="/images/tasks/details.png" alt="" position="center" style="border-radius: 8px;" >}}

## Selected tasks

All of the above can also be utilized for either one and selected tasks. A double click on task executes a `--dry-run`, next double click executes the real run.

## Remote info

Select a task and shortcut `⌘I` will show local and remote info about a task.

{{< figure src="/images/tasks/localremote.png" alt="" position="center" style="border-radius: 8px;" >}}

## Abort

Select Abort will halt any ongoing action.
