+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "RsyncUI config files"
tags = ["config file"]
# categories = ["general information"]
description = "Where does RsyncUI store the configuration files?"
lastmod = "2020-10-23"
+++
RsyncUI stores configurations, schedules and log records for tasks as [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) files. The storage of those files are:
```
$HOME/.rsyncosx/macserialnumber/
```
In the `About` the used path for configuration files is shown. RsyncUI evaluates the computer mac serial number at startup.

## Configuration files
```
$HOME/.rsyncosx/macserialnumber/configurations.json
```
If profile:
```
$HOME/.rsyncosx/macserialnumber/profile/configurations.json
```
## Schedules and log records
```
$HOME/.rsyncosx/macserialnumber/macserialnumber/schedules.json
```
If profile:
```
$HOME/.rsyncosx/macserialnumber/profile/schedules.json
```

## User configurations

The [user configurations](/post/userconfiguration/) are stored as a PLIST file in:
```
$HOME/.rsyncosx/macserialnumber/rsyncuiconfig.plist
```
The user settings applies to all profiles.
