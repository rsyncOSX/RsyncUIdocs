+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "The development of RsyncUI"
tags = ["SwiftUI"]
categories = ["SwiftUI"]
description = "Why is the development of RsyncUI based on SwiftUI?"
lastmod = "2021-03-12"
+++
The development of RsyncUI commenced in December 2020 and the release of RsyncUI will be sometime before summer 2021. The name of the next version is **RsyncUI**. It is built for **macOS Big Sur** and later, that is why it will be released as a new appliction and not replace the current version of RsyncOSX.

[SwiftUI](https://developer.apple.com/documentation/swiftui/) is a new **declarative framwork** for UI. Compared to a Swift, Storyboard and View Controllers application, the numbers of codelines to create the UI with SwiftUI is minimal.

The future of development on the Apple plattform is SwiftUI. [SwiftUI](https://en.wikipedia.org/wiki/Swift_(programming_language)) was released in 2019. The code for the UI utilizing SwiftUI is minimal and easily separated from the Model (MVC). By hiding application logic and actions in properties, functions and closures will simplify the code and make more easy to read. The declarative paradigm makes the code for the UI cleaner and more easy to follow.

[Combine](https://developer.apple.com/documentation/combine) is also a new **declarative framework** from Apple. I am using it primarly for asynchronous tasks like validate input and listening for (two) notifications from the NotificationCenter. Those two notifications are very important for RsyncUI to work. They must be reliable and whenever they are triggered RsyncUI must catch them.

The development of RsyncOSX began early in 2016 in it is a pure Swift (Cocoa and Foundation) based application. RsyncUI is a SwiftUI and Swift based application. Developing the UI in SwiftUI is giant step forward compared to how it the UI is implemented in Swift.

## About the development and progress

There are some more info about the progress in [the todo list](/post/todo/). Also check out the [changelog](/post/changelog/).

The final version will be released sometime closer to summer 2021. Most of the core basic functions like executing tasks, compute the parameters to rsync are reused code from the current version. And most of the executing part is stable and working.

## The source code

The source is available on my [GitHub account](https://github.com/rsyncOSX/RsyncUI). If you have any comments or ideas please use [the discussion part for RsyncUI](https://github.com/rsyncOSX/RsyncUI/discussions).

## Resources to learn SwiftUI

There are a lot of resources to learn SwiftUI. Google, Stack Overflow, YouTube and GitHub are amongst the most used resources. I am also following a few blogs like:

- Paul Hudson´s [Hacking With Swift](https://www.hackingwithswift.com/)
- John Sundell´s [Swift by Sundell](https://swiftbysundell.com/)
- Dave Werver´s [iOS Dev Weekly](https://iosdevweekly.com/)
- PhysicsNerd´s [YouTube SwiftUI channel](https://www.youtube.com/c/PhysicsNerdDev/featured)
- [Apple tutorials about developing in SwiftUI](https://developer.apple.com/tutorials/app-dev-training)

## How is RsyncUI developed?

The following are som high level info about how RsyncUI is constructed and operates.

### Basic data structure

The basic datastructure in RsyncUI is two arrays of structs: configurations as Array<[Configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/Configuration.swift)> and logs- and schedules as Array<[ConfigurationSchedule](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/ConfigurationSchedule.swift)>. During start and load of data all rsync parameters for all configurations are [computed](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift). The main [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcessCmdCombineClosure.swift) reads all arguments an Array\<String\> ahead of exection. The [compute](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift) object reads and prepares all rsync parameters as Array\<String\> as part of start and load of data.

Any change to the basic data structures causes RsyncUI to write data to permanent storage, reload data and recompute rsync parameters.

### MVC model

RsyncUI is constructed in compliance to the Model View Controller (MVC) architecture. Any operation on the data is within the model. The modelpart is normal **imperativ** Swift development, with classes and structs. The UI part (view) is **declarative** SwiftUI development, with structs only. And the view is clearly separated from the model. Another important part of the UI (and SwiftUI) is the [single source of truth](https://developer.apple.com/documentation/swiftui/managing-user-interface-state). Single source of truth is also part of the MVC architecture.

### The UI

The UI is SwiftUI. Each view is small and by hiding most of the logic within the UI in computed properties and actions, the structure of the UI is easy to follow. The view [AddConfigurationView.swift](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Add/AddConfigurationView.swift) is an example of that. The structure of the view is less than 80 lines of code, the details is within each computed property.

The Add view are put together of two columns and two buttons in right corner. And the structure of the view is very easy to follow. The properties, like `localandremotecatalog` are computed and details about it are hidden within the property itself.

![](/images/development/add.png)

```
var body: some View {
       Form {
           ZStack {
               HStack {
                   // For center
                   Spacer()
                   // Column 1
                   VStack(alignment: .leading) {
                       pickerselecttypeoftask
                       VStack(alignment: .leading) { localandremotecatalog }
                       VStack(alignment: .leading) { backupid }
                       VStack(alignment: .leading) { remoteuserandserver }
                   }
                   // Column 2
                   VStack(alignment: .leading) {
                       ToggleView(NSLocalizedString("Don´t add /", comment: "settings"), $donotaddtrailingslash)
                       HStack {
                           EditValue(100, NSLocalizedString("New profile", comment: "settings"), $newprofile)
                           Button(action: { createprofile() }) { Image(systemName: "plus") }
                           .buttonStyle(GrayCircleButtonStyle())
                       }
                   }
                   // For center
                   Spacer()
               }
               HStack {
                   // Present when either added, updated or profile created
                   if added == true { notifyadded }
                   if updated == true { notifyupdated }
                   if created == true { notifycreated }
               }
           }
           VStack {
               HStack {
                   Spacer()
                   // Add or Update button
                   if selectedconfig == nil {
                       Button(NSLocalizedString("Add", comment: "Add button")) { addconfig() }
                           .buttonStyle(PrimaryButtonStyle())
                   } else {
                       Button(NSLocalizedString("Update", comment: "Update button")) { validateandupdate() }
                           .buttonStyle(PrimaryButtonStyle())
                           .overlay(
                               RoundedRectangle(cornerRadius: 20)
                                   .stroke(Color.red, lineWidth: 5)
                           )
                   }

                   Button(NSLocalizedString("Select", comment: "Select button")) { selectconfig() }
                       .buttonStyle(PrimaryButtonStyle())
               }
           }
       }
       .lineSpacing(2)
       .padding()
       .sheet(isPresented: $presentsheet) { configsheet }
   }
```
### Reading data

Configurations, logs and scedules are read from permanent store into an `ObservableObject` [RsyncOSXdata](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Data/RsyncOSXdata.swift). The data is read only and made available for the various views as a `@EnvironmentObject`. Everytime there is a change to the data, the changes are handled by the model, saved to permanent store and reloaded. 
