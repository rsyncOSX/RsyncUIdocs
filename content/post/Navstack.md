+++
author = "Thomas Evensen"
date = "2023-11-10"
title =  "What is NavigationStack?"
tags = ["navigationstack"]
categories = ["general information"]
lastmod = "2023-11-12"
+++
There are several methods for navigation within SwiftUI, and one method is utilizing `NavigationStack`: "*A view that displays a root view and enables you to present additional views over the root view*". 

The root view is the tasks view, and the all other views like estimating details, execution of tasks and so on will be presented ontop of the root view. No more pop up views and I think the presentation of the other views connected to execution of tasks will be smoother and better.   The user might choose to use the new  `NavigationStack` or stay by default. 

Using `NavigationStack` is only enabled on macOS 14 due to use of the new `Observable` macro which require macOS 14.

## Synchronize data by shortcuts

The synchronization of data is not changed much after introduction of navigation by NavigationStack. By using NavigationStack there are no popups or sheetviews. The following is my procedure for synchronizing data to my backup server. And all tasks are executed by shortcuts on the keyboard. 

### Estimate  `⌘E`

New task are added, for demo purpose only. After adding tasks the main or root view looks like this.  Either by shortcut `⌘E` or by selecting the toolbar "Wand and Stars" starts the estimate.

{{< figure src="/images/navstack/addtasks.png" alt="" position="center" style="border-radius: 8px;" >}}

The estimate view is immidiatly opened and a rotating progress wheel is shown during the process of estimating all tasks. After estimating is completed the summarized result is presented. Blue numbers indicates there is data to be synchronized. 

{{< figure src="/images/navstack/estimatetasks.png" alt="" position="center" style="border-radius: 8px;" >}}

Selecting a row presents the details from the estimate run. Selecting the left arrow left on toolbar returns to the estimate view.

{{< figure src="/images/navstack/detailstask.png" alt="" position="center" style="border-radius: 8px;" >}}

### Synchronize  `⌘R`

Either by shortcut `⌘R` or by selecting  "Arrowshape" right on the toolbar starts the real synchronization of data.

{{< figure src="/images/navstack/estimatetasks.png" alt="" position="center" style="border-radius: 8px;" >}}

And if tasks are estimated there is a progressview for all tasks.

{{< figure src="/images/navstack/executetask1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/navstack/executetask2.png" alt="" position="center" style="border-radius: 8px;" >}}

### The logs view

The logs view shows how much data is synchronized and time used. The values are copied from rsync output.

{{< figure src="/images/navstack/logtasks.png" alt="" position="center" style="border-radius: 8px;" >}}

### The root view 

And after synchronization of data the tasks or root view is updated.

{{< figure src="/images/navstack/tasks.png" alt="" position="center" style="border-radius: 8px;" >}}

### Enable `NavigationStack` and confetti

Enable or disable `NavigationStack`.

{{< figure src="/images/navstack/settings.png" alt="" position="center" style="border-radius: 8px;" >}}

First time info for new users of RsyncUI, with confetti.

{{< figure src="/images/navstack/confetti.png" alt="" position="center" style="border-radius: 8px;" >}}


