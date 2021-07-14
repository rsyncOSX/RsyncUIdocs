+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Restore data"
tags = ["restore"]
# categories = ["synchronize"]
description = "You might want to restore som data?"
lastmod = "2021-03-18"
+++
Restore either files or complete synchronized files is easy in RsyncUI. A restore has to be executed to a **temporary restore path**. This is to secure not destroying any original data. A restore session might be as follows.

### Selecting and filtering

First of all select from which configuration to restore from. After selection RsyncUI automatically collects filenames of all synchronized files. The list might be huge and it is adviced to filter data before viewing retrieved filelist if there are several hundred thousand of lines.  

![](/images/restore/restore.png)

A filter will narrow down the filelist to only filenames including the filter.

### Files to restore

There are two types of restore, either a full restore or by file. If a restore is from a `snapshot` task, a full restore is from the latest snapshot.

- full restore - set `./.` within the select files field
- restore by files - open the View of files and select - the file name must be on the form `./folder/filename`, e.g `./` +  `folder/filename`

Select the View button and select a file or folder to restore. Behind the scenes rsync is used for collecting the synchronized list of files.

Select the file or folder and the name is automatically set as file to restore. Default restore is a `--dry-run` action. Before executing the real restore view the result from the `--dry-run` action.
