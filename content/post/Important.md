+++
author = "Thomas Evensen"
title = "Important info about using RsyncUI"
date = "2021-03-10"
description = "Important info about using RsyncUI"
tags = ["important"]
categories = ["general information"]
lastmod = "2021-01-14"
+++
There are some important information about using RsyncUI if you are new to the command line tool `rsync`. RsyncUI is only a GUI on top of it and it is `rsync` which does actual work, not RsyncUI.

## The --delete parameter and new tasks

The `--delete` parameter is a default parameter. The parameter instructs rsync too keep the **source** and **destination** in sync. The parameter instructs rsync to **delete** all files in the destination which are not present in the source. Every time you add a **new task** to RsyncUI, execute an estimation run and inspect the result before executing a real run. If you by accident set an empty catalog as source, RsyncUI (rsync) will delete all files in the destination.

## RsyncUI as your main tool for backup

RsyncUI is not developed to be an easy to use synchronize and backup tool. The main purpose is to assist and ease the use of `rsync` to synchronize files on your Mac to remote FreeBSD and Linux servers or to a local attached disk. And of course restore files if required.

The UI of RsyncUI can for users who dont know rsync, be difficult or complex to understand. The main objective is to ease the use of `rsync`, not teach macOS users how to use it. That is beyond the scope. Setting wrong parameters to rsync can result in deleted data. And RsyncUI will not stop you for doing so. That is why it is very important to execute a simulated run (`--dry-run`) and inspect what happens before a real run.
