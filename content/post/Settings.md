+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "RsyncUI settings"
description = "Some settings in RsyncUI can be tweaked by the user"
tags = ["usersettings"]
# categories = ["general information"]
lastmod = "2021-03-12"
+++
There are a few settings to be tweaked. Settings are saved to permanent store. The settings are dividede into three parts. When the user has changed a setting it is marked with a change on the `Save` button. The `Save` button is disabled until a change has happend.

You can any time save the current configuration files by the `Backup` button. The backup button executes a copy of all configuration files into your Documents catalog and postfixes the copy with a timestamp (`-month-day-year/hour/minute`).
```
$HOME/Documents/RsyncUIcopy-05-06-2021/08/21
```
**Caution**: when opening the catalog it might be seen as empty. The copy is a `.catalog` and your filebrowser might not see such catalogs.

![](/images/usersettings/save.png)

- [Rsync](/post/normalsettings/) - rsync and other settings
- [Ssh](/post/sshsettings) - SSH settings
- [Paths](/post/pathsettings/) - path to applications and environment
