+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "RsyncUI config files"
tags = ["config file"]
categories = ["general information"]
description = "Where does RsyncUI store the configuration files?"
lastmod = "2020-10-23"
+++
RsyncUI stores its configurations, schedules and log records either as [property list files (PLIST)](https://en.wikipedia.org/wiki/Property_list) or [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) files. Default format is PLIST files. The user can [change the format to JSON](/post/json/). The storage of config files is in:
```
$HOME/.rsyncosx/macserialnumber/
```
In the `About` the used path for configuration files is shown. RsyncUI evaluates the computer mac serial number at startup.

## Configurations as PLIST

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

## User configurations

The [user configurations](/post/userconfiguration/) are stored as PLIST in:
```
$HOME/.rsyncosx/macserialnumber/config.plist
```
The user settings applies to all profiles.
