+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Add and update configurations"
description = "How to enter synchronize tasks into RsyncUI."
tags = ["add configurations"]
# categories = ["configurations"]
lastmod = "2021-03-25"
+++
A configuration require minimum a **local catalog** and a **remote catalog**. After entering information about a configuration select the `Add` button to add it to RsyncUI. Continue adding new configurations until completed and configurations are saved to permanent storage after each entry. Select local catalog either by drag and drop or by enter text directly. For remote catalogs only drag and drop for local attached volumes. For remote server catalogs enter by text only.

![](/images/add/add.png)

## The buttons:

The following actions within this view:

- `Add` - will add a new configuration
- `Select` - will select a configuration for update, the Add label will change to `Update`
- `Profile` - create a new profile, add and select the profile
- `Delete` - delete the selected profile, default profile cannot be deleted

## Sample configuration

Local catalog and Remote catalog are added either by using drag and drop from filemanager or by text only. If enter by text please remember to add the full path. Remote catalogs is entered either by full paths or use the `~` character to expand remote user home catalog. The `red` text is sample values.

### Task

- synchronize, which is default and keeps source and destination in sync
- [snapshots](/post/snapshots/), save changes and deletes ahead of a synchronize
- syncremote, remote is source, synchronize a remote source to a local volume
- **Dont´t add**: `/`
  - by default a trailing `/` is added to both source and destination

### Catalog parameters
- **Local catalog**: required field `/Users/thomas/Documents/`
  - my Documents catalog in my home catalog
- **Remote catalog**: required field `~/Documents/`
  - the `~` is expanded as the home catalog with full path by the remote operating system
  - the remote catalog might also be added by full path, depends where the backup catalog is placed on remote server
  - the backup catalog might also be a local catalog on a local attached disk


### Remote parameters
- **Remote username**: `thomas`
  - username for login to remote server
- **Remote server**: `10.0.0.57`
  - either server name or IP-address for remote server
- **Backup ID**: `My docs catalog`
  - informal tag for the configuration

### Task
- **Type**: there are four types of tasks, `synchronize` which is default, `snapshots`, `syncremote` and `single file`.

## Add configurations

Select the `Add` button when completed and configuration is added to RsyncUI. RsyncUI adds a trailing / character to both local and remote volume. After selecting the Add button another configuration might be added. Any changes (edit or delete) to configurations are done from the Synchronize view. Additional parameters to rsync might be added utilizing the Parameter button.

## Update configuration

To update a configuration use the `Select` button and choose which configuration to update.

![](/images/add/select.png)

After changes either save or select another task to abandon the update.

![](/images/add/update.png)
