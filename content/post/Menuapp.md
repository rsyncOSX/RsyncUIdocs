+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Menuapp"
tags = ["scheduling","menu app"]
description = "The menu app for executing scheduled tasks."
lastmod = "2021-03-10"
+++
The menu app is available for download together with RsyncUI. The menu app is a scaled down and minimal app for executing scheduled tasks in RsyncUI. It executes as a menu app and keeps track on next task to execute. The app is monitoring all schedules in all profiles. Scheduled tasks are added in RsyncUI.

RsyncUI does **not** execute scheduled tasks. Scheduled tasks are only added and deleted within RsyncUI. The menu app is a simple app with a few screens. Every time a task is completed a notification is submitted. The menu app executes tasks applying all user selected rsync parameters to the task.

Menu app keeps track of the first task
|---|
The menu app does not check if two or more tasks are set to be executed at the same time. Only one task is executed at a time. After each execution is completed a recalculation of the schedule is done. The menu app then keeps track of the next and first task to be executed.


## Start

The menu app should normally be started from RsyncUI. If the menu app is installed in other catalog than `/Applications`, alternative catalogs has to be set in user configuration.  If there are tasks waiting for executing there is a green statuslight.

Selecting the Home icon quits the menu app and automatically opens RsyncUI. The arrow icon executes the selected task now.

The menu app submits a notification when a scheduled tasks are completed. A scheduled task is either of type once, daily or weekly. If there are tasks waiting to be executed, the status light will be green. Both `synchronize`and `snapshot` tasks can be executed as scheduled tasks.

![](/images/menuapp/menuapp1.png)

## Active tasks

Active scheduled tasks.

![](/images/menuapp/menuapp3.png)

## Logging

There is a minimal logging in the menu app. The menu app logs the major actions within the menu app.

![](/images/menuapp/menuapp2.png)