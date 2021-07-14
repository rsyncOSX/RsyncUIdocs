+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "RsyncUI settings"
description = "Some settings in RsyncUI can be tweaked by the user"
tags = ["usersettings"]
# categories = ["general information"]
lastmod = "2021-03-12"
+++
There are a few settings to be tweaked. Settings are saved to permanent store. The settings are dividede into three parts. When the user has changed a setting it is marked with a change on the `Save` button. The Save button is disabled until a change has happend.

Usersettings might be opened by the default `⌘,` shortcut for settings.

You can any time save the current configuration files by the `Backup` button. The backup button executes a copy of all configuration files into your Documents catalog and postfixes the copy with a timestamp (`-month-day-year/hour/minute`).
```bash
$HOME/Documents/RsyncUIcopy-05-06-2021/08/21
```
**Caution**: when opening the catalog it might be seen as empty. The copy is a `.catalog` and your filebrowser might not see such catalogs.

- [Rsync](/post/normalsettings/) - rsync and other settings
- [Ssh](/post/sshsettings) - SSH settings
- [Paths](/post/pathsettings/) - path to applications and environment

The info tab shows which version of rsync in use and the path for storing and reading configurations to permanent store.

![](/images/usersettings/info.png)
