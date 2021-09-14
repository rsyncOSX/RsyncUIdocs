+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "The development of RsyncUI"
tags = ["SwiftUI"]
# categories = ["SwiftUI"]
description = "Why is the development of RsyncUI based on SwiftUI?"
lastmod = "2021-03-12"
+++
[SwiftUI](https://developer.apple.com/documentation/swiftui/) was released in 2019 and is a new **declarative framework** for UI development across the various Apple operating systems. It is still young and in development. Developing the UI based on SwiftUI compared to developing utilizing the [Cocoa](https://en.wikipedia.org/wiki/Cocoa_(API)) framework is a huge step forward. The code for the UI utilizing SwiftUI is minimal and easily separated from the Model (MVC). By hiding application logic in properties, functions and closures will simplify the code. The declarative paradigm also makes the code for the UI cleaner and more easy to follow.

[Combine](https://developer.apple.com/documentation/combine) is also a new **declarative framework** from Apple. In RsyncUI it is used for asynchronous tasks like validate user input, listening for notifications from the NotificationCenter, decode and encode JSON data and checking, trimming and verify the output from rsync.

The future of development on the Apple platform is SwiftUI. Not only by SwiftUI, but in companion with the other Swift and Objective-C frameworks.

### My level of coding

If you browse or fork my repositories please be aware of I am not a professional developer nor an expert on Swift. Both RsyncOSX and RsyncUI are projects to learn and keep learning. I try to follow common development paradigms and use the Swift and SwiftUI APIs as they are supposed to be used. I try to utilize all functions the Swift APIs offer and keep the code as small and clean as possible.

## Compile

How to [compile RsyncUI](/post/compile/).

## Resources to learn SwiftUI and Combine

There are a lot of resources to learn SwiftUI. Google, Stack Overflow, YouTube and GitHub are amongst the most used. I am also following a few blogs like:

- [Paul Hudson´s Hacking With Swift](https://www.hackingwithswift.com/)
- [John Sundell´s Swift by Sundell](https://swiftbysundell.com/)
- [Swift with Majid](https://swiftwithmajid.com)
- [Dave Werver´s iOS Dev Weekly](https://iosdevweekly.com/)
- [Apple tutorials about developing in SwiftUI](https://developer.apple.com/tutorials/app-dev-training)

There are also several resources available for the Combine framework. I will like to point the following:

- [Matt Neuburg´s Understanding Combine,](https://www.apeth.com/UnderstandingCombine/)
- [Joseph Heck´s Using Combine](https://heckj.github.io/swiftui-notes/)

RsyncUI is developed in compliance to the Model View Controller (MVC) architecture. Any operations on the data is within the model part. The modelpart is mostly traditional **imperativ** Swift development, with classes and structs. The model classes does also utilize the Combine framework. See the Combine part below for more details. The UI part (view) is **declarative** SwiftUI development, with structs only. The UI is clearly separated from the model. Another important part of SwiftUI is the [single source of truth](https://developer.apple.com/documentation/swiftui/managing-user-interface-state).

## Basic datastructure

The basic datastructures in RsyncUI are two arrays of structs: configurations as Array<[Configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/Configuration.swift)> and logs- and schedules as Array<[ConfigurationSchedule](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/ConfigurationSchedule.swift)>. The actual parameters for a task are [computed](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift) as part of prepare for the run. All parameters are based on data for each configuration. The main [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift) reads all arguments as an Array\<String\> ahead of execution. The [compute](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift) object reads and computes all rsync parameters as Array\<String\> ahead of executing a task.

Any change to the basic data causes RsyncUI to write the complete data to permanent storage and read it again. This is a simple and a kind of "brute force" way to secure that data is consistent and there is no need for functions to handle changed data. Every time there is dirty data, write all data and read it again.

## Permanent storage

RsyncUI saves data on permanent store as files with JSON data. JSON is the preferred format for exchanging data on the Internet and Swift has very good support for decode and encode JSON. See more info about this within the Combine part below. See also where RsyncUI [saves data](/post/configfiles/).

## User settings

Some settings within RsyncUI can be changed by the user. The settings are read by RsyncUI ahead of loading the data. All usersettings are stored within a [singelton object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/SharedReference.swift) which stays alive during the lifetime of RsyncUI. This is the one and only singelton object.

## Reading data

Configurations, logs and scedules are read from permanent store into an `ObservableObject` [RsyncUIdata](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Data/RsyncUIdata.swift). The data is read only and made available for the various views as a `@EnvironmentObject`. Everytime there is a change to the data, the changes are handled by the model, saved to permanent store and reloaded.

## Execution of tasks

Execution of a task is an asynchronous operation. The [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift) is responsible for kicking off tasks. The process object are, by Combine, listening for two notifications:
```bash
Process.didTerminateNotification
NSNotification.Name.NSFileHandleDataAvailable
```
The process object is initialized with two escaping closures:
```bash
processtermination: @escaping () -> Void
filehandler: @escaping () -> Void
```
The closures takes care of whatever action they are set to do any time the notifications are discovered.

## Combine

Combine enables a very good control of asynchronous operations and flow of data. Combine is also used as part of the SwiftUI framework. As an example everytime a SwiftUI `<Binding>` is changed, the UI is updated. And SwiftUI does a lot of UI updates.

The following are parts where Combine is used in RsyncUI:

- validating of input from the user, as example see how SSH settings are added and validated
  - [the SwiftUI code](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Settings/Sshsettings.swift) for the SSH UI
  - [the Swift code](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/ObservableReferenceSSH.swift) for the StateObject validating user input
- [at startup of RsyncUI a check](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Newversion/NewversionJSON.swift) if there is a new version of RsyncUI available
  - there is a [JSON-file](https://github.com/rsyncOSX/RsyncUI/blob/main/versionRsyncUI/versionRsyncUI.json) with versions to update and url-link to the new version
- [reading and decoding JSON data](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/ReadConfigurationJSON.swift) from permanent storage into theire respective datastructures, configurations as Array<[Configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/Configuration.swift)> and schedules as Array<[ConfigurationSchedule](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/ConfigurationSchedule.swift)>
- encoding the above datastructures to [JSON data and writing data](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/WriteConfigurationJSON.swift) to permanent storage
- subscribe, within the [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift), for notifications from the NotificationCenter
- parsing output from the above process object like [trimming and preparing output](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Output/TrimTwo.swift) from a rsync task, this trimming also looks for the string `error` in the output and reports if found
- reading [the user configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Userconfiguration/ReadUserConfigurationPLIST.swift) and setting the values

## Speed

SwiftUI refreshes the view every time there is a change on a `<Binding>`. And there are also several other happenings which causes a refresh of the view. There can be several hundred log records each task. If sorting and filtering of logs are computed properties within a view it can become an speed issue aka *spinning beach ball*. Therefore are all sorting and filtering of logs computed within the [RsyncUIdata](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Data/RsyncUIdata.swift) object and the result is set to the `<Binding>` value after the sort or filtering is completed.

The above also apply to the restore function. Getting the remote filenames of synchcronized data might be huge, several hundred thousand or millions of lines. It is after the completion of getting filenames and filtering, the result is set to a `<Binding>` value which causes a refresh.

## MacOS Monterey

Apple released on 7 Jun 2021 beta of Xcode 13, Swift 5.5, SwiftUI 3 and macOS Monterey (macOS 12). Some of the new features in SwiftUI 3 are already in RsyncUI and most likely will more of the new features, as I learn about them, be integrated. The major part of the new stuff require macOS Monterey. The new stuff in SwiftUI 3 and macOS Monterey makes RsyncUI a more user friendly application. Prereleases of RsyncUI on macOS Monterey will be build when Apple releases public betas of macOS Monterey. The main repository at GitHuB for RsyncUI is updated with latest changes for Xcode 13 and macOS Monterey.

## The @FocusState property

The property toghether with the Combine framework makes it possible to ease and valdidate the input added by the user. There are in the Configurations form three possibilities for actions depended upon the value of the input and the focus. And there is actual no need for neither the tab for advance to next field and the Add button for adding data. The buttons are there, but there is no need to use them.

The following is use of the property within the Configurations form.

### The profile field

Adding data to the profile field will automatically **create** a new profile when the user press **the Enter key** for submitting the name of the profile. The new profile is automatically selected.

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

The `searchable` modifier utilizes a standard method for filter data. The modifier is utilized for filter in **configuration listings**, **log listings** and  **restore files**.

![](/images/macos12/search1.png)
![](/images/macos12/search2.png)

## Settings

The settings is now available from the menu bar only or by the default `⌘,` shortcut for settings.

![](/images/macos12/settings.png)

## The @FocusedBinding property and focusedSceneValue modifier

This property and modifier is utilized to trigger estimation and execution of tasks from the application menu. The property and modifier enables that a value from one view is injected into to the full focused view. By selecting from the application menu, the value of the trigger is changed and injected into either the single task view or multiple task view depended upon which has focus.

![](/images/macos12/shortcuts.png)

## The .swipeActions function

The latest beta of SwiftUI also makes it easy to attach actions to a row in a list and emphasize the role of the button.

![](/images/macos12/slidedelete.png)

## Colours and some other settings

The buttons and menus apply to colour settings within the macOS General settings as well as the icon size sidebar menu. The help menu is linked to default help shortcut and likewise for the settings.

![](/images/macos12/adaptive.png)

## Localization

Xcode 13 is really good at extracting strings from code for localization. In RsyncUI localization is done by the following. The `EditValue` is a simple modifier for a `TextField`. And there are several methods for localization., please see the Apple documentation for more info.

- all strings which require localizations is within one file, as an example [see the German Localizable.strings](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/de.lproj/Localizable.strings)
- strings used like a sample text for a `TextField` is wrapped inside a `NSLocalizedString`
- all strings connected to like a Button or Text is extracted and automatically translated by Xcode
```swift
// String is wrapped inside a NSLocalizedString
EditValue(150, NSLocalizedString("New profile", comment: ""),
                      $newdata.newprofile)
                .focused($focusField, equals: .newprofileField)
                .textContentType(.none)
                .submitLabel(.return)
// String is extracted by Xcode for localization
Button("Create") { createprofile() }
    .buttonStyle(PrimaryButtonStyle())
```
All strings to be translated is looked up by Xcode within the `Localizable.strings` file. Services like Crowdin is great for the actual translation process. Export strings for translation by Xcode, import to Crowdin and after translation import in Xcode.
