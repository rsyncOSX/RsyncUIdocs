+++
author = "Thomas Evensen"
date = "2022-05-01"
title =  "How are the apps built?"
tags = ["built"]
categories = ["general information"]
lastmod = "2023-01-03"
+++
*Under development.* This page is an overview of the main components of RsyncOSX and RsyncUI. The development of the apps has been an evolving process. The open source community has been and still is a great resource for ideas and how to solve specific tasks. Both apps today are stable and in a state of maintenance. Some numbers:

| App      | Lines of code | Swift files | Version 1.0 |
| ----------- | ----------- |   ----------- | -------- |
| RsyncUI   | about 15,5K     | about 175       | 6 May 2021 |
| RsyncOSX   | about 11K   | about 121      | 14 March 2016 |	

Which application to use? Both applications does the same job. They read and update the same files for tasks and logs which means you can use both apps, but not at the same time due to locking of files. 

## A few words about the code

Even though I am an educated IT person, most of my professional work has been as an IT manager and not a developer. Most of my coding experience is with private projects such as RsyncOSX and RsyncUI. Google is and has been a great resource for research and advice on how to solve specific problems. Reading other developers' code and discussing it is always valuable input for my code. The MVC pattern and single source of truth are important patterns for both apps. I have also tried to use all Apple Frameworks, utilising most of the required built-in functions, like sorting or filter algorithms. And even if there are many lines of code in both apps, I have tried to write as little code as possible. So if you are looking at my code, keep this in mind: my code is only one of probably many ways to solve a problem.

## RsyncUI vs RsyncOSX

For the moment, there are more users of RsyncOSX than RsyncUI. But the number of users of RsyncUI is growing. And Apple is clear: SwiftUI, which RsyncUI is developed by, is the future. This means that most of my development is on RsyncUI. RsyncOSX is still supported, but only issues are fixed and no new features are added. RsyncUI and RsyncOSX share most of the code for the model components. The main differences between the two apps are the user interface (UI) and how the UI is built. RsyncUI is developed using SwiftUI. RsyncOSX is developed using storyboards. Both apps utilise another great declarative library, Combine, developed by Apple, and JSON files for storing tasks, log records, and user configuration.

| App      | Code | Paradigm |
| ----------- | ----------- |   ----------- |
| RsyncUI   | SwiftUI, Swift | declarativ  |
| RsyncOSX   | Storyboard, Swift  | imperativ |

SwiftUI is the latest declarative framework developed by Apple for views, controls, and layout structures for user interface. 

### RsyncUI, SwiftUI

*RsyncUI* utilizes *SwiftUI* for the UI. UI components are views, which is a value type `struct` and not a reference type `class`. UI components are added to RsyncUI by code. Every time a property within a SwiftUI view is changed the view is recreated by the runtime. In SwitfUI there are property wrappers to create bindings to mutable properties.

### RsyncOSX, Storyboard

*RsyncOSX* utilizes *Storyboard*, which is a tool for graphical design of views. UI components like buttons, tables and other UI components are added and placed within the view by the developer utilizing Xcode. After design all UI components are connected by creating bindings to Swift code. The developer manually adds a reference to the Swift source code for every view  within the Storyboard. If the developer misses to bind a UI component, the app will crash with an nil pointer exception every time that view is exposed.

Storyboard for the tab views:
{{< figure src="/images/Xcode/storyboard1.png" alt="" position="center" style="border-radius: 8px;" >}}

Storyboard for the sheetviews:
{{< figure src="/images/Xcode/storyboard2.png" alt="" position="center" style="border-radius: 8px;" >}}

## Asynchronous execution 

Asynchronous execution of tasks are key components of both apps. Every time a `rsync` synchronize and restore task is executed the termination of the task is not known ahead.  When the *termination signal* is observed some actions are required. Some actions are like stopping a progressview, send a message about task is completed, do some logging and execute next synchronize task.

There are two methods for asynchronous execution. One is utilizing *callback functions* or *completion handlers*, which trigger next action when task is completed. The second is utilize Swift´s `async` and `await` utilities for asynchronous execution. Utilizing `async` and `await` makes the code simpler and cleaner. The need for *completion handlers* are reduced.  And lesser code is better code. Swift concurrency is a seperate and huge topic to discuss. I am not in a position to discuss it. There are structured and unstructered concurrency in Swift. Within RsyncUI and RsyncOSX there are only one asynchronous execution at any time except for concurrency within the Swift and SwiftUI libraries such as GUI updates. 

All code which utilizes asynchronous execution are shared between the two apps. The `Process` object is where the real work is done. Input to the `Process` are the command to execute and the parameters for the command. The `Process` object utilizes Combine for monitoring *process termination* and output, when needed by the apps, from the command.  There are two versions of the process object:

- [the process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift)
- [the async process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/Async/RsyncProcessAsync.swift)

The difference between those two objects are minor, the async version marks the function for execution with keyword `async`. Calling the `async` require the `await` keyword. 

## The Process object

Without communicating to the macOS system, RsyncUI is *nothing*. Every command within RsyncUI, except administration of tasks and logs, are commands to be executed by the macOS system. The main commands are executing `rsync` with the approriate arguments. But there are also commands executing `rm`, `ssh` and `mkdir`. And the Process object is utilized for all those commands. 

## Combine

Combine, a *declarative* library by Apple, makes the code easy to write and easy to read. In the Combine code for encode and write data to JSON file, the publisher require *macOS BigSur* and later. The following are examples of utilizing Combine:

- [read](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/ReadConfigurationJSON.swift) configurations for tasks
- [write](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/WriteConfigurationJSON.swift) configurations for tasks
- [the process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/Async/RsyncProcessAsync.swift) for executing tasks

## Start of RsyncOSX

The start of RsyncOSX starts with the attribute `@NSApplicationMain` which kicks off everything. Within the Storyboard, the entry point is marked, and the view is binded with the Switf code to start the application. The Toolbar is programmatically constructed, which makes it easier to change vs. designing it on the Storyboard.

## Start of RsyncUI

The start of RsyncUI conforms to the [App protocol](https://developer.apple.com/documentation/SwiftUI/App). There is only one entrance point, `@main`, in RsyncUI. The `@main` initialises the app, setup of the menubar, and opens the navigation bar which is the main user start for the app.

# The model

Parts of the model is equal, but there are some differences due to the fact that SwiftUI views are value types (structs) and not reference types (classes) as in Storyboard and Swift. The model is also responsible for informing the views when there are changes. Both apps share basic functions like reading and writing data from the store, updating the model, and so on. The memory footprint of tasks is minimal. Data for tasks are kept in memory for both apps during their lifetime. The memory footprint for logs will grow over time as new logs are created and stored. But logs are only read from the store when viewing and deleting logs. When data about logs is not used, the data is released from memory to keep the memory as low as possible.

# SwiftUI

The following are for RsyncUI and SwiftUI.

## Property wrapper for objects

With Swift 5.9, Xcode 15 and macOS 14 Apple introduced the `@Observable` macro. On previous macOS versions, the property wrapper `@StateObject` in combination with `ObservableObject` and Combine, are used to create binding to mutable properties. The new macro simplifies how to create bindings and there is also quite a boost in performance. The performance part is not that important for RsyncUI, but lesser code is better code.  There is also a new `@Bindable` property wrapper which create bindings to mutable properties of `@Observable` objects. 

## Environment property

Data for tasks are read from store and made available for all the views by an Environment property. After the app is initialized and started, it opens the main navigation and read tasks for the default profile and other profiles when selected. Data for tasks is made available for all views  within the view hierarchy by the `.environment` property on *macOS Sonoma* and  by the `.environmentObject` property on *macOS Ventura* and *Monterey*. The property makes the data global available for views. The `@Bindable` property wrapper is also, on macOS Sonoma, used for creating bindings to the mutable properties of observable objects.

All synchronize tasks are executed asynchron. The process object, which is responsible for executing the external rsync tasks, is listening for termination of the external process.  A `@StateObject` or `@State` on macOS Sonoma, which is created when the SwiftUI view for observing the progress is created, is by the model updated during progress of the task.

### Breaking change

The `@Observable` macro is a breaking change. It is not possible to include the new macro in code and support older macOS versions as Monterey and Ventura. There are also som other changes and new properties which also makes it difficult to include new features in code and still support previous versions of macOS. The new Observation framework is a new implementation of the observer design pattern and removes the need for including Combine. Combine itself is still used in the RsyncUI.

### Combine and SwiftUI

There is no need for Combine in combination with the new  `@Observable` macro, but Combine is used in a couple of SwiftUI views to debounce text input from the user. The user input is a search or filter string and by default the userinput is a `@State` string variable. The view reacts on the input by every keypress and the filter algorithm is triggered by every keypress. This causes a sluggish user interface, but by debounce input by *one second* causes the filter algorithm only update after the *one second* debounce.

## OSLog

Included in Swift 5 there is a unified logging feature `OSLog`. There are several methods for logging and investigate what the application is up to. By using OSLog there is no need for print statements to follow execution. All logging is by utilizing OSLog displayed as part of Xcode. The `Process` objects are where all the real work is done. OSLog is  included in all objects which perform work and it is very easy to check which commands RsyncUI are executing.

OSLog info in Xcode. The logging is displaying commands and arguments as shown below. It makes it convenient to check that RsyncUI is executing the correct command.

{{< figure src="/images/Xcode/Logger.png" alt="" position="center" style="border-radius: 8px;" >}}

And the OSLogs might be read by using the Console app. Be sure to set the Action in Console app menu to `Include Info Messages` and enter `no.blogspot.RsyncUI` as subsystem within the search field.

{{< figure src="/images/Xcode/console.png" alt="" position="center" style="border-radius: 8px;" >}}

## Navigation

The main navigation, when RsyncUI starts, is by a `NavigationSplitView`: *A view that presents views in two or three columns, where selections in leading columns control presentations in subsequent columns.* RsyncUI utilizes two columns. Left column for main functions and the right column for details about each main function.  The details part is computed every time the user select a function like the Synchronize view, Tasks view and so on. 

By each view functions are avaliable by the Toolbar and for many functions by keyboard shortcuts as well. Some functions by each view is also connected to Buttons within the view. Actions by buttons could also be by the Toolbar, but to many functions by the Toolbar might confuse the user.

### Sheet views and NavigationStack

The user may select either pop-up views, sheets, or emedded views by `NavigationStack`. It is for the user to decide which type to prefer. Views by `NavigationStack` are views embedded and ontop of the root view. An arrow left on the Toolbar shows when it is a view over the main view. A pop-up view hast to be closed by a Button to continue.

The main root view

{{< figure src="/images/Xcode/taskview.png" alt="" position="center" style="border-radius: 8px;" >}}

Estimate by `NavigationStack`

{{< figure src="/images/Xcode/navestimate.png" alt="" position="center" style="border-radius: 8px;" >}}

Details by `NavigationStack`

{{< figure src="/images/Xcode/navdetails.png" alt="" position="center" style="border-radius: 8px;" >}}

Estimate by sheet view

{{< figure src="/images/Xcode/sheetestimate.png" alt="" position="center" style="border-radius: 8px;" >}}

Details by sheet view

{{< figure src="/images/Xcode/sheetdetails.png" alt="" position="center" style="border-radius: 8px;" >}}



