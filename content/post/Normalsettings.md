+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Rsync and other settings"
tags = ["userconfig"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
You can any time backup the current setup, configurations and logs including all profiles by the `wrench` icon on the toolbar. The backup executes a copy to your Documents catalog and postfixes the copy with a timestamp `-month-day-year/hour/minute`.

`$HOME/Documents/RsyncUIcopy-05-06-2021/08/21`

When opening the catalog it might be seen as empty. The copy is a `.catalog` and your filebrowser might not see such catalogs.

{{< figure src="/images/usersettings/settings.png" alt="" position="center" style="border-radius: 8px;" >}}

## Rsync version and path

It is adviced to install rsync as part of Homebrew. RsyncUI discover what type of Mac you are on. The path for Homebrew is: 

- Intel based Mac is: `/usr/local/bin`
- on the Apple Silicon: `/opt/homebrew/bin`.

The path is set if not changed by the user.

 - Rsync v3.x to `on` - set optional path if **NOT** by Homebrew
   	- any version of rsync should work, but only version 2.6.9 and 3.2.x are tested and verified
    - [utilizing the snapshot feature](/post/snapshots/) require version 3.2.x of rsync
- rsync version and path:
    - if utilized version of rsync is **not** installed by Homebrew set path to rsync
- path for restore:
    - preset temporary path for restoring single files and catalogs
    - preset temporary path for a full restore

If there is a not valid rsync path is set an error is presented.

## Mark days

Tasks with older execute date than number of days are marked red.

## Log to file

There is three choices for logging, none, min and full and they are mutually exclusive. The following are settings for logging:

- none - there is no logging
- min - last 10 lines of output is logged
- full - everything is logged

The log file is stored at `$HOME/.rsyncosx/macserial/rsyncui.txt`. The logfile can be opened from the main view.

## Other settings

- Detailed log level
    - if Detailed is `on` there is a separate log for each run, if `off` only date for last run is saved on the task
- Monitor network
    - monitor the network connection during execution of tasks
    - if a network connection is dropped during execution, RsyncUI sends an interrupt signal to the task and it halts with an error
- Check for error in output
    - if the word `error` is discovered in output from rsync it is notified
- Confirm execute
    - see below
    

### Error output rsync

Sample of error in output from rsync. If switch `Check for error in output` is on RsyncUI writes the output to logfile and Alerts the user about error in rsync.

{{< figure src="/images/usersettings/errorinrsync.png" alt="" position="center" style="border-radius: 8px;" >}}

### Confirm execute

The new confirm dialog if number of files to synchronize is like a new task. Sometimes a remote server or local disk is unavailable or forgotten to attach. If you commence a synchronize task unaware of destination resource is not available, rsync might believe this is a new full synchronize and a dialog confirms synchronize or abort
- if a remote server is unavailable rsync will *most likely* complain and throw an error, if `check for error in output` in user settings is enabled, the rsync error messages written to log and an Alert informing about it will occur
- if a local disk is not attached rsync will try to synchronize data to `/Volumes/` catalog on your mac, this catalog is normally where macOS mounts local attached disks
```bash
/dev/disk5s2 on /Volumes/Import bilder (apfs, local, nodev, nosuid, journaled, noowners)
/dev/disk6s1 on /Volumes/Backups (apfs, local, nodev, nosuid, journaled, noowners)
```
Below the local attached volume is not connected, the estimate may think there is a new synchronize task. If you just forgot to attach the disk you dont want RsyncUI to synchronize data to the `/Volume` catalog. 
{{< figure src="/images/usersettings/summarizedview.png" alt="" position="center" style="border-radius: 8px;" >}}
When the switch is on RsyncUI ask to confirm synchronize. 
{{< figure src="/images/usersettings/confirmdialog.png" alt="" position="center" style="border-radius: 8px;" >}}

