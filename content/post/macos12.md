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
Apple released on 7 Jun 2021 beta of Xcode 13, Swift 5.5, SwiftUI and macOS 12. Some of the new features in SwiftUI are already in RsyncUI and most likely will more of the new features, as I learn about them, be integrated in RsyncUI. The major part of the new features in SwiftUI require macOS 12. Next major update of RsyncUI will be built for macOS 12 only.

And there are a few significant changes in SwiftUI and macOS 12 which makes RsyncUI a more user friendly application. The downside is there will be no release until the final version of Xcode 13 and macOS 12 is here.

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

The `searchable` modifier utilizes a standard method for filter data. The modifier is utilized in configuration listings and log listings.

![](/images/macos12/search1.png)
![](/images/macos12/search2.png)

## Settings

The settings is now available from the menu bar only.

![](/images/macos12/settings.png)

## The @FocusedBinding property and focusedSceneValue modifier

This property and modifier is utilized to trigger estimation and execution of tasks from the application menu. The property and modifier enables that a value from one view is injected into to the full focused view. By selecting from the application menu, the value of the trigger is changed and injected into either the single task view or multiple task view depended upon which has focus.

![](/images/macos12/shortcuts.png)

## Colours and some other settings

The buttons and menus apply to colour settings within the macOS General settings as well as the icon size sidebar menu. The help menu is linked to default help shortcut and likewise for the settings.

![](/images/macos12/adaptive.png)
![](/images/macos12/adaptive2.png)
