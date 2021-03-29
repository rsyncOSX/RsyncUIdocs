+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "JSON and backup"
description = "Use JSON as storage format?"
tags = ["usersettings"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
In this view you can backup configurations and, if wanted transform existing configurations to either JSON or PLIST.

![](/images/usersettings/json.png)

## JSON or PLIST

See [JSON support](/post/json/) for more info about JSON support. Default is PLIST.

## Enable JSON

PLIST is default.

RsyncUI can store configurations and schedules in either JSON or PLIST format. If JSON is `off` PLIST is selected. See [JSON support](/post/json/) for more info about JSON support.

## Backup

The `Backup` button copies all configurations and logs as a backup to your `$HOME/Documents/RsyncOSXcopy-$date-suffix`. Viewing the catalog in Finder might show an empty catalog. The catalog is not empty, the configurations are saved as `.rsyncosx/macserialnumber` and Finder might not show `.` catalogs.

## Returning to previous format

If you decide to return to previous format just do the process once more.
