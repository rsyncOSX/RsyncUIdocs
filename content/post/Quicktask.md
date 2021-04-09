+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Quicktask"
tags = ["quick task"]
categories = ["synchronize"]
description = "How to just execute a quick task?"
lastmod = "2021-03-18"
+++
Use RsyncUI for quickly synchronize files to either local or remote storage. If synchronizing to a remote storage require setup of [passwordless login](/post/remotelogins/).

![](/images/quicktask/quicktask.png)

After entering data, default is a `--dry-run` task. It is adviced to inspect the result before the real run. 

#### Catalog parameters
- **Local catalog**: required field `/Users/thomas/Documents/`
  - my Documents catalog in my home catalog
- **Remote catalog**: required field `~/Documents/`
  - the `~` is expanded as the home catalog with full path by the remote operating system
  - the remote catalog might also be added by full path, depends where the backup catalog is placed on remote server
  - the backup catalog might also be a local catalog on a local attached disk

#### Remote parameters
- **Remote username**: `thomas`
  - username for login to remote server
- **Remote server**: `10.0.0.57`
  - either server name or IP-address for remote server
