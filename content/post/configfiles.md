+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "RsyncUI config files"
tags = ["config file"]
# categories = ["general information"]
description = "Where does RsyncUI store the configuration files?"
lastmod = "2020-10-23"
+++
RsyncUI stores its configurations, schedules and log records as [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) files. The storage of config files is in:
```
$HOME/.rsyncosx/macserialnumber/
```
In the `About` the used path for configuration files is shown. RsyncUI evaluates the computer mac serial number at startup.

## Configuration files
```
$HOME/.rsyncosx/macserialnumber/configurations.json
```
If profile is utilized:
```
$HOME/.rsyncosx/macserialnumber/profile/configurations.json
```
## Schedules and log records
```
$HOME/.rsyncosx/macserialnumber/macserialnumber/schedules.json
```
If profile is utilized:
```
$HOME/.rsyncosx/macserialnumber/profile/schedules.json
```

## User configurations (as a PLIST file)

The [user configurations](/post/userconfiguration/) are stored as PLIST in:
```
$HOME/.rsyncosx/macserialnumber/config.plist
```
The user settings applies to all profiles.
