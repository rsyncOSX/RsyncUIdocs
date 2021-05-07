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

![](/images/singletask/singletask.png)

The following actions are possible within this view:

- `Estimate` - estimate the selected task, after estimating the label changes to `Execute`
- `Now` - execute the selected task, no estimation

The buttons to right:

- `View` - after estimaten, view result
- `Abort` - abort the ongoing task
