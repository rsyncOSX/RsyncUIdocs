+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "Restore data"
tags = ["restore"]
categories = ["synchronize"]
lastmod = "2021-03-18"
+++
Restore either files or complete synchronized files is easy in RsyncUI. A restore has to be executed to a **temporary restore path**. This is to secure not destroying any original data. A restore session might be as follows.

### Selecting and filtering

First of all select from which configuration to restore from. After selection select the Files button nd RsyncUI collects filenames of all synchronized data. Filter of data either by adding filter in top right search field before selecting the Files button or within the Files view.

{{< image src="/images/restore/restore_filter.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< image src="/images/restore/restore_select.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< image src="/images/restore/restore_dryrun.png" alt="" position="center" style="border-radius: 8px;" >}}

A filter will narrow down the filelist to only filenames including the filter.

### Files to restore

There are two types of restore, either a full restore or by file. If a restore is from a `snapshot` task, a full restore is from the latest snapshot.

- full restore - set `./.` within the select files field
- restore by files - open the View of files and select - the file name must be on the form `./folder/filename`, e.g `./` +  `folder/filename`

Select the file or folder to restore. Default restore is a `--dry-run` action. Before executing the real restore view the result from the `--dry-run` action.
