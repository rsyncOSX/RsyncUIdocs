+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Convert from PLIST to JSON"
tags = ["plist"]
# categories = ["sequrity"]
description = "Some info about converting PLIST to JSON"
lastmod = "2021-05-25"
+++
This function are for **existing users of RsyncOSX** who wants start using RsyncUI. RsyncUI read and write configurations and logs as [JSON](https://en.wikipedia.org/wiki/JSON) files. The user will have the option to convert **RsyncOSX** [plist configuration files](https://en.wikipedia.org/wiki/Property_list) to JSON. Before converting to JSON make a backup of the current configuration files. The current configurations is backed up in the Documents catalog.

- sample JSON data for [configurations](https://raw.githubusercontent.com/rsyncOSX/RsyncUI/main/samplejsondata/configurations.json)
- sample JSON data for [schedules](https://raw.githubusercontent.com/rsyncOSX/RsyncUI/main/samplejsondata/schedules.json)

If you **don´t** see any configurations in RsyncUI, RsyncOSX is not setup to use JSON files. This will convert existing PLIST configurations and logs to JSON files which RsyncUI can read.

Start RsyncUI, select the **correct profile** or use **default**, select Settings and the Paths tab.

In the Paths tab select the PLIST button:

![](/images/plist/plist1.png)

If there is JSON files, RsyncUI will inform about it. To continue select the Confirm switch. If there are no JSON files, the Alert will not be presented.

![](/images/plist/plist2.png)

To continue, do a backup of existing configurations. Choose convert and that is it.

![](/images/plist/plist3.png)
