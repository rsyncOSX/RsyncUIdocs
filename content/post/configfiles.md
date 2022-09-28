+++
author = "Thomas Evensen"
date = "2021-04-16"
title =  "RsyncUI configuration files"
tags = ["config file"]
categories = ["general information"]
lastmod = "2020-10-23"
+++
RsyncUI stores its configurations, schedules and log records and user configurations as [JSON](https://en.wikipedia.org/wiki/JSON) files. The storage of those files is:

`$HOME/.rsyncosx/macserialnumber`

In the `About` the used path for configuration files is shown. RsyncOSX evaluates the computer mac serial number at startup.

## Configuration files

`$HOME/.rsyncosx/macserialnumber/configurations.json`
If profile is utilized:

`$HOME/.rsyncosx/macserialnumber/profile/configurations.json`

## Log records

`$HOME/.rsyncosx/macserialnumber/schedules.json`

If profile is utilized:

`$HOME/.rsyncosx/macserialnumber/profile/schedules.json`

## User configurations

The [user configuration](/post/settings/) is stored as:

`$HOME/.rsyncosx/macserialnumber/rsyncuiconfig.json`

The user settings applies to all profiles.
