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

{{< image src="/images/add/add.png.png" alt="" position="center" style="border-radius: 8px;" >}}

## The buttons:

The following actions within this view:

- `Add` - will add a new configuration
- `Update` - the `Add` button will change when a configuration is selected

### Task

- synchronize, which is default and keeps source and destination in sync
- [snapshots](/post/snapshots/), save changes and deletes ahead of a synchronize
- syncremote, remote is source, synchronize a remote source to a local volume
- **Dont´t add**: `/`
  - by default a trailing `/` is added to both source and destination

### Catalog parameters
- **Local catalog**: required field
- **Remote catalog**: required field
  - the backup catalog might also be a local catalog on a local attached disk


### Remote parameters
- **Remote username**:
  - username for login to remote server
- **Remote server**:
  - either server name or IP-address for remote server
- **Backup ID**:
  - informal tag for the configuration

### Task
- **Type**: there are three types of tasks, `synchronize` which is default, `snapshots` or `syncremote`.

## Add configurations

Select the `Add` button when completed and configuration is added to RsyncUI. RsyncUI adds a trailing / character to both local and remote volume. After selecting the Add button another configuration might be added. Any changes (edit or delete) to configurations are done from the Synchronize view. Additional parameters to rsync might be added utilizing the Parameter button.

## Update configuration

To update a configuration select it and update. After changes either save or select another task to abandon the update.
