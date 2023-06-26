+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Execute tasks"
tags = ["execute","delete tasks"]
categories = ["synchronize"]
lastmod = "2021-03-10"
+++
**Caution**: after adding new tasks always verify the result of task by either a double click on task or by opening the Rsync parameters view, select the task and choose the `Verify` button. 

The task view also lets you execute **all** or **selected** tasks in one go. Actions are triggered either by keyboard shortcuts or by buttons. The following are allowed shortcut actions:

- `estimate` - shortcut `⌘E` estimates all tasks
- `execute` - shortcut `⌘R` executes all tasks either direct or after an estimation run
- `show info` - shortcut `⌘I`

## Several tasks

When RsyncUI starts it automatically open this view and by selecting the shortcut action `⌘E` will estimate all tasks. Executing tasks after estimating, either direct by button or by  `⌘R` a progressbar will show progress. 

{{< figure src="/images/tasks/tasks.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/tasks/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

## One task

All of the above can also be utilized for either one and selected tasks. A double click on task executes a `--dry-run`, next double click executes the real run.

## Remote info

Select a task and shortcut `⌘I` will show local and remote info about a task.

{{< figure src="/images/tasks/localremote.png" alt="" position="center" style="border-radius: 8px;" >}}

## Abort

Select Abort will halt any ongoing action.
