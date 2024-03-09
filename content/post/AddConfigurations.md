+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Add and update tasks"
tags = ["add","profile"]
categories = ["synchronize"]
lastmod = "2023-12-18"
+++
Always verify, by a `--dry-run`,  the result of a new task before executing it. 

A task require minimum a *local catalog* and a *remote catalog*. After entering information about a task, select the `+` icon upper right to add it to RsyncUI. Continue adding new tasks until completed and tasks are saved to permanent storage after each entry.

{{< figure src="/images/add/add.png" alt="" position="center" style="border-radius: 8px;" >}}

Just press the Enter key will automatically enter a new task. The Enter key will advance to next field. If the local catalog and remote catalog are local attached catalogs the Enter key will automatically add it after the Synchronize ID. Or  `+` will add a new task. To update a task select it and to save changes press the `+`, which has changed to an update icon.

## Copy and paste

Shortcuts for copy and paste are `⌘C` and  `⌘V` or from the Edit menu. The copy and paste makes a copy of selected tasks and marks them with copy. The copy inlcudes all parameters of the copied tasks.

{{< figure src="/images/add/copy.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/add/paste.png" alt="" position="center" style="border-radius: 8px;" >}}

## Delete

Select tasks to be deleted and delete from the Edit menu or the `backspace` button.

{{< figure src="/images/add/delete.png" alt="" position="center" style="border-radius: 8px;" >}}

## Data about tasks

The following are data about tasks:

### Task

- `synchronize`, which is default and keeps source and destination in sync
- `snapshot`, save changes and deletes ahead of a synchronize
- `syncremote`, remote is source, synchronize a remote source to a local volume
- Dont´t add `/`
  - by default a trailing `/` is added to both source and destination

### Catalog parameters
- Local catalog: required field
- Remote catalog: required field
  - the backup catalog might also be a local catalog on a local attached disk

### Synchronize ID

- Synchronize ID:
  - informal tag for the task

### Remote parameters
- Remote username:
  - username for login to remote server
- Remote server:
  - either server name or IP-address for remote server
  
## Catalogs

Selecting the `Home` icon lists all catalogs from your `$Home`. If there is attached a local disk, the first name of volume is automatically copied to the destination.

{{< figure src="/images/add/homecatalogs.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/add/volumes.png" alt="" position="center" style="border-radius: 8px;" >}}

## Profiles

Either add or delete profiles. A profile is only a catalog where data about tasks are saved. See tag about `config-file` where RsyncUI stores files.

{{< figure src="/images/add/profiles.png" alt="" position="center" style="border-radius: 8px;" >}}
