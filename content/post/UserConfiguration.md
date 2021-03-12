+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "User configuration"
tags = ["userconfig"]
categories = ["general information"]
astmod = "2020-08-24"
+++
There are a few parameters to choose in user configuration. Parameters are saved to permanent store. The settings is dividede into four parts.

## Settings

This view includes the most normal settings to tweak.

![](/images/usersettings/settings.png)

### Rsync

 - Rsync version and path - set optional path if **NOT** in /usr/local/bin
   	- any version of rsync should work, but only version 2.6.9, 3.1.3 and 3.2.x are tested and verified
    - [utilizing the snapshot feature](/post/snapshots/) require either version 3.1.3 or 3.2.x of rsync
- path for rsync:
    - if other version of rsync is installed in other path than /usr/local/bin it must be set here
- path for restore:
    - preset temporary path for restoring single files and catalogs
    - preset temporary path for a full restore

If there is a not valid rsync path is set an error is presented.

### Log to file

If None is switch off there is no log to file. If on there is either a minimum or full log to file.

- either minimum (last 10 lines) or full logging of output from rsync, be carful not logging everything, the log file might be big
- the log file can be inspected by open the output
- the log file is stored at `$HOME/.rsyncosx/macserial/rsynclog.txt`

### Level log

If Detailed is on there is a separate log for each run. If off only date for last run is saved on the configuration.

### Mark days

- in Synchronize view tasks older than number of days are marked red

### Monitor connection

RsyncUI can monitor the network connection during execution of tasks. If a network connection is dropped during execution, RsyncUI sends an interrupt signal to the task and it halts with an error.

### Check input

By setting check data, RsyncUI will check and if required clean logs. The check data flag is **not** persistent and have to be set each time.

### Enable JSON

RsyncUI can store configurations and schedules in either JSON or PLIST format. If JSON is off PLIST is selected.

## SSH settings

In this view you can let RsyncUI assist in creating ssh-keys and setup global ssh keypath and identityfile.

![](/images/usersettings/ssh.png)

### Ssh parameters (global)

The user can set a selected ssh keypath and identityfile. Default values for ssh are `~/.ssh/id_rsa` and portnumber `22`. It is not required to set if default values are used.

- portnumber, which ssh communicates through
- keypath + identityfile, user selected if other than default

If global values are set, this is what the ssh parameter within the rsync command looks like.

`-e  "ssh -i ~/.ssh_rsyncosx/rsyncosx -p NN"` where:

- `-i` is the ssh keypath and identityfile
- `-p` is the port number ssh communicates through, default port 22

If global ssh parameters are set, it applies to **all configurations**. It is possible to set other ssh values on each task.

## Paths and environment

In this view set alternative path to apps and environment.

![](/images/usersettings/paths.png)

### Paths for RsyncUI and RsyncOSXsched

If both apps are installed in `/Applications` there is no need for setting paths.

- path RsyncUI
- path RsyncOSXsched

### Environment

Enable environment:

It is possible to enter an environment variable to the process which executes the synchronize task. An example of such is :

`"SSH_AUTH_SOCK": "/Users/username/.gnupg/S.gpg-agent.ssh"`

## Backup, JSON and PLIST

In this view you can backup configurations and, if wanted transform existing configurations to either JSON or PLIST.

![](/images/usersettings/json.png)

### Backup

The `Backup` function copies all configurations and logs as a backup to your `$HOME/Documents/RsyncOSXcopy-$date-suffix`. Viewing the catalog in Finder might show an empty catalog. The catalog is not empty, the configurations are saved as `.rsyncosx/macserialnumber` and Finder might not show `.` catalogs.

### JSON

See [JSON support](/post/json/)
