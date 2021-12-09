+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Pre- and post shell scripts"
description = "It is possible to set a pre and post shell script"
tags = ["shellout"]
categories = ["synchronize"]
lastmod = "2021-04-16"
+++
You can connect shell scripts to a task. A shell script can e.g. be mounting (pre) and unmounting (post) of a remote storage. Or you can execute a shell script to encrypyt your data ahead of synchronizing the data.  It is **only** possible to execute the shell scripts utilizing Single task and the `Now` button. Tasks are marked if there are shell scripts connected to the task.

The shell scripts names and locations is selected by the user.

- **pretask**: attach optional pre shell script to the synchronize command, the shell script is executed **ahead** of the synchronize command
  - switch execute shell script on/off
- **posttask**: attach optional post shell script to the synchronize command, the shell script is executed **after** the synchronize command
  - switch execute shell script on/off
- **Halt on error**: if the phrase "error" occurs in the output from the `pre.sh` command, if `on` the execution of synchronize command is aborted

{{< image src="/images/shellout/shellout1.png" alt="" position="center" style="border-radius: 8px;" >}}

Shell tasks has to be `Enabled` before they are active.

{{< image src="/images/shellout/shellout2.png" alt="" position="center" style="border-radius: 8px;" >}}
