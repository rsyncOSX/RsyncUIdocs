+++
author = "Thomas Evensen"
title = "Important info about using RsyncUI"
date = "2021-03-10"
description = "Important info about using RsyncUI"
tags = ["important"]
categories = ["general information"]
lastmod = "2021-01-14"
+++
RsyncUI is not developed to be an easy to use synchronize and backup tool. The main purpose is to assist and ease the use of `rsync` to synchronize files on your Mac to remote FreeBSD and Linux servers. And of course restore files from those remote servers.

The UI of RsyncUI can for users who dont know rsync, be difficult or complex to understand. Using RsyncUI requires some knowledge of `rsync`. The main objective for RsyncUI is to ease the use of `rsync`, not teach macOS users how to use `rsync`. That is beyond the scope of RsyncUI. Setting the wrong parameters to rsync can result in deleted data. And RsyncUI will not stop you for doing so. That is why it is very important to execute a simulated run (`--dry-run`) and inspect what happens before a real run.

RsyncUI supports **synchronize** and **snapshots** of files.

## RsyncUI as your main tool for backup

If your plan is to use RsyncUI as your main tool for backup of files, please investigate and understand the limits of it. RsyncUI is quite powerful, but it is might not the primary backup tool for the average user of macOS.

## The --delete parameter

Caution about RsyncUI and the `--delete` parameter. The parameter is a default parameter. The parameter instructs rsync to keep the source and destination synchronized (in sync). The parameter instructs rsync to delete all files in the destination which are not present in the source.

Every time you add a **new task** to RsyncUI, execute an estimation run (`--dry-run`) and inspect the result before executing a real run. If you by accident set an empty catalog as source RsyncUI (rsync) will delete all files in the destination.
