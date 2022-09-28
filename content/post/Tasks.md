+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Execute tasks"
tags = ["execute","delete tasks"]
categories = ["synchronize"]
lastmod = "2021-03-10"
+++
The task view either lets you:

- execute **all** or **selected** (by shortcut `⌘T`) tasks in one go
- for **one** task, estimate and view the detailed output from rsync before executing the real run

All actions are triggered either by keyboard shortcuts or by buttons. The following are allowed shortcut actions:

- `estimate` - shortcut `⌘E`
- `execute` - shortcut `⌘R`
- `select task` - shortcut `⌘T`

## Several tasks

This is most likely the most used action after adding and verifying the task. When RsyncUI starts it automatically open this view and by selecting the shortcut action `⌘R` will commence estimating and execute all tasks. If you only want to do this for some of the tasks, select the tasks and choose the action.

{{< image src="/images/tasks/estimateall.png" alt="" position="center" style="border-radius: 8px;" >}}

The `Log` button presents a summarized output from all rsync tasks.

{{< image src="/images/tasks/summarizedoutput.png" alt="" position="center" style="border-radius: 8px;" >}}

## One task

**Choose** (not select) a task when the task view is opened and select (or by shortcut) the Estimate button.

{{< image src="/images/tasks/selectone.png" alt="" position="center" style="border-radius: 8px;" >}}

A summarized view of an estimation run:

{{< image src="/images/tasks/estimateone.png" alt="" position="center" style="border-radius: 8px;" >}}

The `Log` button presents a detailed output from rsync.

{{< image src="/images/tasks/detailedoutput.png" alt="" position="center" style="border-radius: 8px;" >}}

## Delete

Select a configuration and slide left for delete.

## Abort

Select Abort will halt any ongoing action.
