+++
author = "Thomas Evensen"
date = "2021-03-11"
title =  "RsyncUI and macOS 12?"
tags = ["macos12"]
# categories = ["sequrity"]
description = "Some info about what is new in RsyncUI on macOS 12"
lastmod = "2021-06-15"
toc = true
+++
Apple released on 7 Jun 2021 beta of the above including a lot of new features in SwiftUI. Some of the new stuff in SwiftUI, like the `@FocusState` property, require macOS 12. Some of the features will be integrated in next version of RsyncUI, e.g. the property `@FocusState` is great for guiding the user in input forms.

## App protocol

The current version of RsyncUI is utilizing the AppDelegate protocol to kick of the application, which is how a Swift and Storyboard macOS is starting up. The default start for a SwiftUI application is by the [App protocol](https://developer.apple.com/documentation/swiftui/app-structure-and-behavior). This is now changed in code.

## The @FocusState property

The property enables a detailed guide and possibilities depended upon the flow of input and the value of the input. There are in the Configurations form three possibilities for actions depended upon the value of the input and where the focus is. And there is actual no need for neither the tab and the Add button. Both the tab and Add button is there, but there is no need to use them.

### The profile field

Adding data to the profile field will automatically **create a new profile** when the user press **the Enter key for submitting** the name of the profile. The new profile is automatically selected.

### Configurations

There are two options here:

- add a local catalog to synchronize, a **local attached disk** as remote catalog, and a synchronization ID
- add a local catalog to synchronize, a **remote catalog on a remote server** as remote catalog, a synchronization ID, a remote user and a remote server

The start is selecting focus in the local catalog. After submitting data by **the Enter key** the focus is automatically advanced to remote catalog.

When the synchronize ID is submitted, by the Enter key, the Form is validating if **the remote catalog** is on a **local attached disk**. If this is validated the Form will automatically add a new configuration by the Enter key. If not validated the Form expect it is s remote catalog and the focus is advanced to remote user and server. After submitting a remote server the Form will automatically add a new configuration.

![](/images/macos12/newadd.png)

And it is likewise for the pre- and post shell scripts. There is **no need** to explicit toggle the pre- and post shell scripts on. By the Enter key add pre and post, the Form will automatically switch the toggles on.

![](/images/macos12/newpreandpost.png)

## The searchable modifier

The `searchable` modifier utilizes a standard method for filter data. The modifier is added to configuration listings and log listings. 

![](/images/macos12/search1.png)
![](/images/macos12/search2.png)

## Settings

The settings is now available from the menu bar only.

![](/images/macos12/settings.png)
