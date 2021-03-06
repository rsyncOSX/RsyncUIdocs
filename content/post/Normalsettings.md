+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Rsync and other settings"
description = "Which version of rsync to use?"
tags = ["usersettings"]
# categories = ["general information"]
lastmod = "2021-03-11"
+++
You can any time save the current configuration files by the `Backup` button. The backup button executes a copy of all configuration files into your Documents catalog and postfixes the copy with a timestamp `-month-day-year/hour/minute`.
```bash
$HOME/Documents/RsyncUIcopy-05-06-2021/08/21
```
**Caution**: when opening the catalog it might be seen as empty. The copy is a `.catalog` and your filebrowser might not see such catalogs.

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

There is three choices for logging, none, min and full and they are mutually exclusive. The following are settings for logging:

- none - there is no logging
- min - last 10 lines of output is logged
- full - everything is logged

The log file can be inspected by `⌘O` shortcut or by the File menu. The log file is stored at `$HOME/.rsyncosx/macserial/rsynclog.txt`.

## Level log

If Detailed is `on` there is a separate log for each run. If `off` only date for last run is saved on the configuration.

## Mark days

Tasks with older execute date than number of days are marked red.

## Monitor network

RsyncUI can monitor the network connection during execution of tasks. If a network connection is dropped during execution, RsyncUI sends an interrupt signal to the task and it halts with an error.

## Check input

By setting check data, RsyncUI will check and if required clean logs. The check data flag is **not** persistent and have to be set each time.
