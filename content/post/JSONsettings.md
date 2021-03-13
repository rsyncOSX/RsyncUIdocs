+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "JSON and backup"
tags = ["userconfig"]
categories = ["general information"]
lastmod = "2021-03-11"
+++
In this view you can backup configurations and, if wanted transform existing configurations to either JSON or PLIST.

![](/images/usersettings/json.png)

## JSON or PLIST

See [JSON support](/post/json/) for more info about JSON support. Default is PLIST.

## Backup

The `Backup` button copies all configurations and logs as a backup to your `$HOME/Documents/RsyncOSXcopy-$date-suffix`. Viewing the catalog in Finder might show an empty catalog. The catalog is not empty, the configurations are saved as `.rsyncosx/macserialnumber` and Finder might not show `.` catalogs.

## JSON

See [JSON support](/post/json/)
