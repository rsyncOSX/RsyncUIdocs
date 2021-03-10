+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "RsyncUI config files"
tags = ["config file"]
categories = ["general information"]
description = "Where does RsyncUI stores the various configuration files."
lastmod = "2020-10-23"
+++
RsyncUI stores its configurations, schedules and log records either as [property list files](https://en.wikipedia.org/wiki/Property_list) or [JSON](https://en.wikipedia.org/wiki/JSON) files. Default format is property list files, the user can change [the format to JSON](/post/json/).

The storage of config files is default in `$HOME/.RsyncUI/macserialnumber`. Existing users of previous versions of RsyncUI can move configfiles from old localization (`Documents/Rsync/macserialnumber`) to new by selecting `Move` from the `File` menu of RsyncUI.  In the `About` the used path for configuration files is shown.

Configuration files are store in `$HOME/.RsyncUI/macserialnumber`. RsyncUI evaluates the computer mac serial number at startup.

## Configurations as plist

The default format is plist:

### Configuration files

Default profile stores all configurations in:
```
$HOME/.rsyncosx/macserialnumber/configRsync.plist
```
If profile is utilized:
```
$HOME/.rsyncosx/macserialnumber/profile/configRsync.plist
```
where `profile` is a sub catalog.

### Schedules and log records

Default profile stores all Schedules and log records in:
```
$HOME/.rsyncosx/macserialnumber/macserialnumber/scheduleRsync.plist
```
If profile is utilized:
```
$HOME/.rsyncosx/macserialnumber/profile/scheduleRsync.plist
```

## Configurations as JSON

The user can [change format to JSON](/post/json/):

### Configuration files
```
$HOME/.rsyncosx/macserialnumber/configurations.json
```
If profile is utilized:
```
$HOME/.rsyncosx/macserialnumber/profile/configurations.json
```
### Schedules and log records
```
$HOME/.rsyncosx/macserialnumber/macserialnumber/schedules.json
```
If profile is utilized:
```
$HOME/.rsyncosx/macserialnumber/profile/schedules.json
```

## User configurations and Assist

The [user configurations](/post/userconfiguration/) and [Assist](/post/addconfigurations/#assist) data are stored as plist in:
```
$HOME/.rsyncosx/macserialnumber/config.plist
$HOME/.rsyncosx/macserialnumber/assist.plist
```
The user settings applies to all profiles.
