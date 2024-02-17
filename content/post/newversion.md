+++
author = "Thomas Evensen"
date = "2023-12-01"
title =  "Next version 1.8.7 (b95)"
tags = ["next version"]
categories = ["synchronize"]
lastmod = "2024-02-17"
+++
Date: 17 Feb 2024

Some info about next version 1.8.7 (build 95). To be relased in som days.

There are quite a few internal changes in code. I got some ideas by doing the SwiftData project for RsyncUI. The changes are mostly simplifying and deleting code. And there is updates within the demo data as well. The demo data now includes some data about snapshots. Snapshot is an effective method for saving old and deleted files ahead of a synchronizing task. By the restore view,  restore any file from any snapshot. 

Loading Demo data is marked in some of the views.

{{< figure src="/images/newversion/nr1.png" alt="" position="center" style="border-radius: 8px;" >}}

Selecting the snapshot task in Demo. The Demo just copies some data from GitHub to simulate the snapshot function. For a real snapshot task this view collects data about all stored snapshots.

{{< figure src="/images/newversion/nr2.png" alt="" position="center" style="border-radius: 8px;" >}}

Tagging, by the Snapshot menu or shortcut `⌘T` marks which snapshots should be deleted. Read more [about snapshots](/post/snapshots/) in user doc. All snapshots every Sunday every week are marked for KEEP.

{{< figure src="/images/newversion/nr3.png" alt="" position="center" style="border-radius: 8px;" >}}

Changing keep Sunday to keep Thursday causes some changes in tagging.  After changing day to keep refresh tagging by shortcut `⌘T`.

{{< figure src="/images/newversion/nr4.png" alt="" position="center" style="border-radius: 8px;" >}}

Quick task is moved to a button within main Synchronize view. See first image in this page, the hare icon.

{{< figure src="/images/newversion/nr5.png" alt="" position="center" style="border-radius: 8px;" >}}
