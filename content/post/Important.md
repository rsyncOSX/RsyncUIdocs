+++
author = "Thomas Evensen"
title = "Important"
date = "2021-03-10"
tags = ["important"]
categories = ["general information"]
lastmod = "2021-01-14"
+++
If you are new to the command line tool `rsync` and RsyncUI please read this information. RsyncUI is a GUI only on top of the command line tool. It is `rsync` which does the actual work, not RsyncUI

## The --delete parameter and new tasks

The `--delete` parameter is a *default parameter* set by RsyncUI to `rsync`. The parameter instructs rsync too keep the *source* and *destination* in sync. The parameter instructs rsync to *delete* all files in the destination which are not present in the source. Every time you add a *new task* to RsyncUI execute an estimation run and inspect the result before executing a real run. If you by accident set an empty catalog as source, RsyncUI, `rsync`, will delete all files in the destination.

Default parameters set by RsyncUI to `rsync` can be disabled task by task. If you decide to disable a default parameter, be sure you understand what the result is. A disabled default parameter can be enabled again.

## Aborting tasks

Please be aware it is an external task not controlled by RsyncUI, which executes the command line tool `rsync`. RsyncUI is monitoring the task for progress and termination. The user can abort a tasks at any time. Please let the abort to finish and cleanup before starting a new task. It might take a few seconds. If not RsyncUI might become unresponsive.

## RsyncUI as your main tool for backup

RsyncUI is not developed to be an easy to use synchronize and backup tool. The main purpose is to assist and ease the use of `rsync` to synchronize files on your Mac to remote FreeBSD and Linux servers or to a local attached disk. And of course restore files if required.

The User Interface of RsyncUI can for users who dont know `rsync`, be difficult or complex to understand. The main objective is to ease the use of `rsync`, not teach macOS users how to use it. That is beyond the scope. Setting wrong parameters to rsync can result in deleted data. And RsyncUI will not stop you for doing so. That is why it is very important to execute a simulated run, `--dry-run`, and inspect what happens before a real run.
