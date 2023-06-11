+++
author = "Thomas Evensen"
title = "Issue"
date = "2023-06-01"
tags = ["important"]
categories = ["general information"]
lastmod = "2023-06-01"
+++
**To be updated**.

This page demonstrates the current issue with a view which is not refreshed after update of data. The issue  applies only to the current view. Updates will force a refresh of data and  all other views are updated but not the current view. The model data, tasks and log data, are read into an `ObservableObject` object which publish, by  the  property wrapper `@Published` , all changes to data. The data is made avaliable for all views by the `.environmentObject(rsyncUIdata)` property wrapper. And this works very well.

The view presenting tasks as table data is [very simple](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Configurations/ListofTasksLightView.swift) and the view should pick up when updates to data is published.

This is the view for adding parameters to rsync. 
 
{{< figure src="/images/temp/before.png" alt="" position="center" style="border-radius: 8px;" >}}

As an example adding FreeBSD suffix as parameter to rsync. After selecting button FreeBSD and then Save button updates the model data. But the current view is not updated.

{{< figure src="/images/temp/addingsuffix.png" alt="" position="center" style="border-radius: 8px;" >}}

After update the current view is nor updated or selecting row. The table view utilizes a `@Binding var selecteduuids: Set<Configuration.ID>` which is a UUID property for selection. After update and no reload of data in view the selection of a row does not work,

{{< figure src="/images/temp/currentview.png" alt="" position="center" style="border-radius: 8px;" >}}

Selecte the Default parameter view and data is properly updated.

{{< figure src="/images/temp/otherview.png" alt="" position="center" style="border-radius: 8px;" >}}

And the workauround is select any other view and return, the view is also properly updated.

{{< figure src="/images/temp/changeandcurrent.png" alt="" position="center" style="border-radius: 8px;" >}}

