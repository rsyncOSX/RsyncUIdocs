+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Rsync and other settings"
tags = ["userconfig"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
This view includes the most normal settings to tweak.

![](/images/usersettings/settings.png)

## Rsync version and path

 - Rsync version 3.x to `on` - set optional path if **NOT** in /usr/local/bin
   	- any version of rsync should work, but only version 2.6.9, 3.1.3 and 3.2.x are tested and verified
    - [utilizing the snapshot feature](/post/snapshots/) require either version 3.1.3 or 3.2.x of rsync
- path for rsync:
    - if other version of rsync is installed in other path than /usr/local/bin it must be set here
- path for restore:
    - preset temporary path for restoring single files and catalogs
    - preset temporary path for a full restore

If there is a not valid rsync path is set an error is presented.

## Log to file

If None is switch `on` there is no log to file. If `off` there is either a minimum or full log to file.

- either Min (last 10 lines) or Ful logging of output from rsync, be carful not logging everything, the log file might be big
- the log file can be inspected by `⌘L` shortcut or bu the File menu
- the log file is stored at `$HOME/.rsyncosx/macserial/rsynclog.txt`

## Level log

If Detailed is `on` there is a separate log for each run. If `off` only date for last run is saved on the configuration.

## Mark days

Tasks with older execute date than number of days are marked red.

## Monitor network

RsyncUI can monitor the network connection during execution of tasks. If a network connection is dropped during execution, RsyncUI sends an interrupt signal to the task and it halts with an error.

## Check input

By setting check data, RsyncUI will check and if required clean logs. The check data flag is **not** persistent and have to be set each time.
