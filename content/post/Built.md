+++
author = "Thomas Evensen"
date = "2023-12-23"
title =  "How is RsyncUI built?"
tags = ["built"]
categories = ["general information"]
lastmod = "2023-12-23"
+++
*Under development.* This page is an overview of the main components of RsyncUI. The development of both RsyncOSX and RsyncUI has been an evolving process. The open source community has been and still is a great resource for ideas and how to solve issues. Both apps today are stable and in a state of maintenance. Some numbers:

| App      | Lines of code | Swift files | Version 1.0 |
| ----------- | ----------- |   ----------- | -------- |
| RsyncUI   | about 13.2K     | about 163       | 6 May 2021 |
| RsyncOSX   | about 11K   | about 121      | 14 March 2016 |	

Which application should I use? Both applications do the same job, but RsynUI is more feature-rich, and the GUI, including navigation, is better. **Are you on macOS Sonoma?** Go for RsyncUI. And for the last year and years to come, all development has been and will be within RsyncUI. RsyncOSX is bugfixed only.

# A few words about the code

Even though I am an educated IT person, most of my professional work has been as an IT manager and not a developer. Most of my coding experience is with private projects such as RsyncOSX and RsyncUI. Google is and has been a great resource for research and advice on how to solve specific problems. Reading about other developers code and discussions is always valuable input for me. The MVC pattern and single source of truth are important patterns for both apps. I have also tried to use all Apple Frameworks, utilizing most of the required built-in functions.  And even if there are many lines of code in both apps, I have tried to write as little code as possible. So if you are looking at my code, keep this in mind, my code is only one of many solutions.

And I believe there is no wright or wrong in development. Each developer and team chooses their way to developed based on their skills and what they want to achieve. I know my own code and I have no issues understanding what my code is doing. And as times go on, in my opinion, I do changes in code to the better. But I fully understand other developers might have some issues understanding my code. 

# Why not App Store (yet)

One important requirement for macOS apps on Apple App Store is, quote Apple: *"To distribute a macOS app through the Mac App Store, you must enable the App Sandbox capability."* There are restrictions what an app can do inside the App Sandbox and one restriction is not allowed to access local .dotfiles outside catalogs like the Documents catalog. One important feature for RsyncUI is passwordless login by ssh to remote servers. Passwordless login by ssh is by ssh-keys and default ssh-key is:
```bash
~/.ssh/id_rsa
```
The App Sandbox capability is set off and access local files on. This is the only way to get the latest version of RsyncUI working as expected. The sequrity for RsyncUI not containing malicious code is by [signed and notarized by Apple](/post/notarized/). 

RsyncUI is also storing data in a .dotfile catalog.
```bash
$HOME/.rsyncosx/macserialnumber/configurations.json
```
But there might be a version for RsyncUI on App Store later in 2024. I have commenced the work on integrating SwiftData and a limited version of RsyncUI might find it way to the App Store.

# RsyncUI vs RsyncOSX

Apple is clear: *SwiftUI*, which RsyncUI is developed by, is the future. This means *all new development* is on RsyncUI. The main differences between the two apps are the user interface (UI) and how the UI is built. But there has also been a lot of cleanup and enhancements in code of RsyncUI and not in RsyncOSX. My advice is use RsyncUI. Both apps utilise another great declarative library, Combine, developed by Apple, and JSON files for storing tasks, log records, and user configuration.

| App      | UI | Paradigm |
| ----------- | ----------- |   ----------- |
| RsyncUI   | SwiftUI, Swift | declarativ  |
| RsyncOSX   | Storyboard, Swift  | imperativ |

SwiftUI is the latest declarative framework developed by Apple for views, controls, and layout structures for user interface. 

# SwiftData

*SwiftData* - I have commenced the work in this release to see if SwiftData might be beneficial for RsyncUI. There are only three files saved to storage from RsyncUI, tasks, log records and user settings. Those data might be enabled to utilize SwiftData and if so RsyncUI might be available from the Apple App Store as well. This is due to App Sandbox capability and what is allowed and not allowed inside an App Sandbox. Reading and writing files from a `.dotcatalog` on a users home directory is not allowed which RsyncUI does now. The work is commenced. What is requiered first is to update the internal dataflow before introducing SwiftData for RsyncUI.

If a *SwiftData* version is enabled, there will be two versions of RsyncUI, one for Homebrew as today and one for the App Store utlizing only attached discs and default version of rsync. I have just commenced learning about SwifData and a new version might be ready sometime late in February or March 2024.

- the work on *SwiftData* is commenced, but I have to study what and understand how to use it myself
	- if success on SwiftData there might be a minor version of RsyncUI on App Store, by minor means only default version of rsync on macOS and attached disks only
	- the full version of RsyncUI will always be available on Homebrew

# SwiftUI

*RsyncUI* utilizes *SwiftUI* for the UI. UI components are views, which is a value type `struct` and not a reference type `class`. UI components are added to RsyncUI by code. Every time a property within a SwiftUI view is changed the view is recreated by the runtime. In SwitfUI there are several property wrappers to create bindings to mutable properties.

# Asynchronous execution 

Asynchronous execution is a key component of RsyncUI. Every time a `rsync` synchronize and restore task is executed the termination of the task is not known ahead.  When the *termination signal* is observed some actions are required. Some actions are like send a message about a task is completed, execute next synchronize task, stopping a progressview and do some logging. 

There are two methods for asynchronous execution. *Callback functions* or *completion handlers*, which trigger next action when task is completed, and Swift´s `async` and `await` keywords for asynchronous execution. Utilizing `async` and `await` makes the code simpler and cleaner. Swift concurrency is a seperate and huge topic to discuss. I dont have the details and knowlegde to discuss it. There are structured and unstructered concurrency in Swift. Within RsyncUI there is only one asynchronous execution at any time except for concurrency within the Swift and SwiftUI libraries such as GUI updates. 

# The Process object

The `Process` object is where the real work is done. Input to the `Process` are the command to execute and the parameters for the command. The `Process` object utilizes Combine for monitoring *process termination* and *the output* from the command.  There are two versions of the process object:

- [the process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift)
- [the async process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/Async/RsyncProcessAsync.swift)

The difference between those two objects are minor, the async version marks the function for execution with keyword `async`. Calling the `async` require the `await` keyword. 

RsyncUI is depended to communicate with command line tools within the macOS system. The main command is executing `rsync` with the approriate arguments. But there are also commands executing `rm`, `ssh` and `mkdir`. And the Process object is utilized for all those commands. 

# Combine

Combine, a *declarative* library by Apple, is utilized in several parts of RsyncUI. Before the new `@Observable` macro was introduced Combine was also a requiered part of the property wrapper `@StateObject` in combination with `ObservableObject`. The new macro `@Observable` is not depended upon Combine and the following are examples of utilizing Combine in RsyncUI:

- [read json ](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/ReadConfigurationJSON.swift) configuration file for tasks
- [write json](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/WriteConfigurationJSON.swift) configuration file for tasks
- [observing signals](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/Async/RsyncProcessAsync.swift) within the process object
- debouncing input from user, filter strings and other values which are validated before saving

Combine is utilized in all read and write of data to permanent storage, configurations, logrecords and user configuration. The user input for search or filter is by default a `@State` string variable. The view reacts on the input by every keypress and the filter algorithm is triggered by every keypress. This causes a sluggish user interface, but by debounce input by *a second* causes the filter algorithm only to update the view after the debounce period.

# Start of RsyncUI

The start of RsyncUI conforms to the [App protocol](https://developer.apple.com/documentation/SwiftUI/App). There is only one entrance point, `@main`, in RsyncUI. The `@main` initialises the app, setup of the menubar, and opens the navigation bar which is the main user start for the app.

# The model

SwiftUI views are *value types*, structs, and not *reference types*, classes, as in Storyboard and Swift. The model is responsible for informing the views when there are changes. The memory footprint of tasks is minimal. Data for tasks are kept in memory during the lifetime of RsyncUI. The memory footprint for logrecords will grow over time as new logs are created and stored. Logrecords are only read from the store when viewing and deleting logs. When data about logs is not used, the data is released from memory to keep the memory as low as possible.

# Property wrapper for objects

With Swift 5.9, Xcode 15 and macOS 14 Apple introduced the `@Observable` macro. On previous macOS versions, the property wrapper `@StateObject` in combination with `ObservableObject` and Combine, was used to create binding to mutable properties. The new macro simplifies how to create bindings and there is also quite a boost in performance. The performance part is not that important for RsyncUI, but lesser code is better code.  There is also a new `@Bindable` property wrapper which create bindings to mutable properties of `@Observable` objects. 

# Environment property

Data for *tasks* are read from store and made available for all the views by an Environment property. After the app is initialized and started, it opens the main navigation and read tasks for the default profile and other profiles when selected. Data for tasks is made available for all views  within the view hierarchy by the `.environment` property. The property makes the data global available for views. The `@Bindable` property wrapper is also used for creating bindings to the mutable properties of `@Observable` objects.

All synchronize tasks are executed asynchron. The process object, which is responsible for executing the external rsync tasks, is listening for termination of the external process.  A `@Observable` object, which is created when the SwiftUI view for observing the progress is created, is by the model updated during progress of the task.

# OSLog

Included in Swift 5 there is a unified logging feature `OSLog`. There are several methods for logging and investigate what the application is up to. By using OSLog there is no need for print statements to follow execution. All logging is by utilizing OSLog displayed as part of Xcode. The `Process` objects are where all the real work is done. OSLog is  included in all objects which perform work and it is very easy to check which commands RsyncUI are executing.

OSLog info in Xcode. The logging is displaying commands and arguments as shown below. It makes it convenient to check that RsyncUI is executing the correct command.

{{< figure src="/images/Xcode/Logger.png" alt="" position="center" style="border-radius: 8px;" >}}

And the OSLogs might be read by using the Console app. Be sure to set the Action in Console app menu to `Include Info Messages` and enter `no.blogspot.RsyncUI` as subsystem within the search field.

{{< figure src="/images/Xcode/console.png" alt="" position="center" style="border-radius: 8px;" >}}

# Navigation

The main navigation, when RsyncUI starts, is by a `NavigationSplitView`: *A view that presents views in two or three columns, where selections in leading columns control presentations in subsequent columns.* RsyncUI utilizes two columns. Left column for main functions and the right column for details about each main function.  The details part is computed every time the user select a function like the Synchronize view, Tasks view and so on. The navigation within usersetting is also by `NavigationSplitView`.

Navigation within **all** view is by `NavigationStack`: "*A view that displays a root view and enables you to present additional views over the root view*".  One root view is the tasks view, and the all other views like estimating details, execution of tasks and so on will be presented ontop of the root view. RsyncUI utilizes two APIs of  `NavigationStack`:

The additional view is one view only and it is presented when `$somestate` becomes true.

```bash
@State private var somestate: Bool = false

var body: some View {
 	NavigationStack {
 		...
 		.navigationDestination(isPresented: $somestate) {
                SomeView()
            }
        }
    }
```

The views ontop of the root view are computed depended upon what the user decides to do. Like with the main tasks view, selecting estimate all, push the enum which represent start estimate onto the path and the `NavigationStack` loads that view ontop of the root view.

```bash
@State var path: [Tasks] = []
 
var body: some View {
	NavigationStack(path: $path) {
		...
		.navigationDestination(for: Tasks.self) { which in
                    makeView(view: which.task)
            }
        }
        
    @ViewBuilder
    func makeView(view: DestinationView) -> some View {
        switch view {
        case .executestimatedview:
            ExecuteEstimatedTasksView(selecteduuids: $selecteduuids,
                                      reload: $reload,
                                      path: $path)
                .environmentObject(executeprogressdetails)
        case .executenoestimatetasksview:
           ...
        case .estimatedview:
           ...
        }
    }
}
 
 enum DestinationView: String, Identifiable {
    case executestimatedview, executenoestimatetasksview,
         estimatedview, firsttime, dryrunonetask, alltasksview,
         dryrunonetaskalreadyestimated, viewlogfile
    var id: String { rawValue }
}

struct Tasks: Hashable, Identifiable {
    let id = UUID()
    var task: DestinationView
}
```
# ContentUnavailableView

In macOS 14 and SwiftUI there is a new view `ContentUnavailableView` to notify the user when there is nothing to show. There are several options for informing and within RsyncUI the view is utlized in combination with filter search. One example is search for records in snapshot:

```bash
if logrecords.count == 0,
           selectedconfig != nil,
           selectedconfig?.task == SharedReference.shared.snapshot,
           snapshotdata.snapshotlist == false
        {
            ContentUnavailableView {
                Label("There are no snapshot records by this search string in Date or Tag",
                      systemImage: "doc.richtext.fill")
            } description: {
                Text("Change search string to filter records")
            }
        }
```
{{< figure src="/images/Xcode/contentavailable.png" alt="" position="center" style="border-radius: 8px;" >}}
After filter no records:
{{< figure src="/images/Xcode/contentunavailable.png" alt="" position="center" style="border-radius: 8px;" >}}

# Dataflow in RsyncUI

How is data stored and views updated when data is changed? There are three files on permanent storage; tasks, log records and user settings. All files are JSON files and `Combine` is utilized to read and save data. JSON files are *encoded* before a write operation and *decoded* when read from storage. The encode and decode is requiered to represent JSON data as internal data within RsyncUI. 

When RsyncUI starts it reads *user configuration* and *data about tasks for the default profile*. The object holding data about tasks is an `@Observable` object created when RsyncUI starts.

```bash
var rsyncUIdata: RsyncUIconfigurations {
        let configurationsdata = ReadConfigurationsfromstore(selectedprofile)
        return RsyncUIconfigurations(selectedprofile,
                                     configurationsdata.configurations ?? [],
                                     configurationsdata.validhiddenIDs)
    }
```
All views which require data about tasks get data through a mutable property wrapper `@Bindable var rsyncUIdata: RsyncUIconfigurations`.  Within `RsyncUIconfigurations` there is a observed variable holding the data structure about tasks. When tasks are updated, like timestamp last run, the class which executes the tasks does two jobs when executing tasks is completed. The internal datastructure is always updated. The first job is to send the changed updated datastructure up to the view by an *escaping closure*, `@escaping ([Configuration]) -> Void)`. The view updates the observed variable holding the data structure about tasks and the SwiftUI runtime updates the views. The second job is to write the updates the permanent storage.

# How are tasks executed?

There are several ways to execute tasks:

- two double clicks on a task, first is an estimate run and second is the real run
- select task(s) and either estimate first or execute without estimation
- estimate first all tasks and then execute or execute all tasks without estimation

The following is a brief overview of *estimate first and then execute tasks*. The difference between an estimation run and a real run is; estimation run is a `--dryn-run` and there is no logging. An estimation run is commenced by selecting the *wand and stars* icon or shortcut `⌘E` from the main view. The navigation path for estimate all view is pushed onto the view stack and a progress informes which tasks are estimated. For each task the result of the estimation run is saved. After estimation RsyncUI marks tasks where there is data to synchronize. 

The user then select synchronize tasks and the navigation path for executing tasks including progress of each is pushed onto the view stack. From this view the reference of the class with data from estimation is passed onto the class which executes the tasks. The id for each task is pushed onto a stack and the class executing tasks is not released until the stack is emtpy and a process termination signal is observed from the last task. The progess of synchronizing is communicated to the progress view by an *escaping closure*, `@escaping (Int) -> Void)`. 

```bash
func executemultipleestimatedtasks() {
        var uuids: Set<Configuration.ID>?
        if selecteduuids.count > 0 {
            uuids = selecteduuids
        } else if executeprogressdetails.estimatedlist?.count ?? 0 > 0 {
            let uuidcount = executeprogressdetails.estimatedlist?.compactMap { $0.id }
            uuids = Set<Configuration.ID>()
            for i in 0 ..< (uuidcount?.count ?? 0) where
                executeprogressdetails.estimatedlist?[i].datatosynchronize == true
            {
                uuids?.insert(uuidcount?[i] ?? UUID())
            }
        }
        guard (uuids?.count ?? 0) > 0 else { return }
        if let uuids = uuids {
            multipletaskstate.updatestate(state: .execute)
            ExecuteMultipleTasks(uuids: uuids,
                                 profile: rsyncUIdata.profile,
                                 rsyncuiconfigurations: rsyncUIdata,
                                 multipletaskstateDelegate: multipletaskstate,
                                 executeprogressdetailsDelegate: executeprogressdetails,
                                 filehandler: filehandler,
                                 updateconfigurations: updateconfigurations)
        }
    }
    
     func filehandler(count: Int) {
        progress = Double(count)
    }

    func updateconfigurations(_ configurations: [Configuration]) {
        rsyncUIdata.configurations = configurations
    }
```