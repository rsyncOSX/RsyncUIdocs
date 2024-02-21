+++
author = "Thomas Evensen"
date = "2023-12-23"
title =  "How is RsyncUI built?"
tags = ["built"]
categories = ["general information"]
lastmod = "2024-02-8"
+++
This page is an overview of the main components of RsyncUI. The development of both RsyncOSX and RsyncUI has been an evolving process. The open source community has been and still is a great resource for ideas and how to solve issues. Both apps today are stable and in a state of maintenance. 

Some numbers:

| App      | Storage  | Lines of code | Swift files | Version 1.0 |
| ----------- | ----------- |   ----------- | -------- | -------- |
| RsyncUI  | JSON files |  about 13.3K     | about 162       | 6 May 2021 |
| RsyncOSX  |  JSON files |  about 11K   | about 121      | 14 March 2016 |	

Which application should I use? Both applications do the same job, but RsynUI is more feature-rich, and the GUI, including navigation, is better. **Are you on macOS Sonoma?** Go for RsyncUI. And for the last year and years to come, all development has been and will be within RsyncUI. RsyncOSX is bugfixed only.

# RsyncUI vs RsyncOSX

Apple is clear: *SwiftUI*, which RsyncUI is developed by, is the future. This means *all new development* is on RsyncUI. The main differences between the two apps are the user interface (UI) and how the UI is built. There has also been a lot of cleanup and enhancements in code of RsyncUI. My advice is use RsyncUI. Both apps utilise another great declarative library, Combine, developed by Apple, and JSON files for storing tasks, log records, and user configuration. And the latest development, for test, is a version of RsyncUI using SwiftData instead of JSON files as storage. There is some more info about SwiftData later on this page.

| App      | UI | Paradigm |
| ----------- | ----------- |   ----------- |
| RsyncUI   | SwiftUI, Swift | declarativ  |
| RsyncOSX   | Storyboard, Swift  | imperativ |

# A few words about the code

Even though I am an educated IT person, most of my professional work has been as an IT manager and not a developer. Most of my coding experience is with private projects such as RsyncOSX and RsyncUI. Google is and has been a great resource for research and advice on how to solve specific problems. Reading about other developers code and discussions is always valuable input for me. The MVC pattern and single source of truth are important patterns for both apps. I have also tried to use all Apple Frameworks, utilizing most of the required built-in functions.  And even if there are many lines of code in both apps, I have tried to write as little code as possible. So if you are looking at my code, keep this in mind: my code is only one of many solutions.

I also believe there is no right or wrong in development. Each developer and team chooses their way to develop based on their skills and what they want to achieve. I know my own code, and I have no issues understanding what my code is doing. And as times go on, in my opinion, I make changes to the code for the better. I also fully understand that other developers might have some issues understanding my code. 

What I also experience is how my own understanding of OO, declarative programming, Swift and SwiftUI is growing. I would never write code today, as I did when I commenced my project in 2015 to learn Swift. But still, I am not a professional programmer, and there are several topics within Swift and SwiftUI that I do not understand. But I am capable of learning; if I spend enough time on a topic, there is a good probability that I will get the idea.


# Why not App Store

One important requirement for macOS apps on Apple App Store is quote Apple: *"To distribute a macOS app through the Mac App Store, you must enable the App Sandbox capability."* There are restrictions what an app can do inside the App Sandbox. Execute `rsync`, obvious, and enable passwordless login by ssh to remote servers are two must have features. The Apple Sandbox causes a few issues to both features when switch on. And I have not yet any success when RsyncUI is set to use default rsync in macOS and only attached discs. But I am inveastigating, so there might be an Apple App Store version in the future.

Passwordless login by ssh is by ssh-keys and default ssh-key is:

```bash
$HOME/.ssh/id_rsa
```
The JSON version of RsyncUI is also storing data in a `.dotfile` catalog. This does not apply for the SwiftData version. 

```bash
$HOME/.rsyncosx/macserialnumber/*.json
```
# OSLog

Included in Swift 5 there is a unified logging feature `OSLog`. There are several methods for logging and investigate what the application is up to. By using OSLog there is no need for print statements to follow execution. All logging is by utilizing OSLog displayed as part of Xcode. The `Process` objects are where all the real work is done. OSLog is  included in all objects which perform work and it is very easy to check which commands RsyncUI are executing.

OSLog info in Xcode. The logging is displaying commands and arguments as shown below. It makes it convenient to check that RsyncUI is executing the correct command.

{{< figure src="/images/Xcode/Logger.png" alt="" position="center" style="border-radius: 8px;" >}}

And the OSLogs might be read by using the Console app. Be sure to set the Action in Console app menu to `Include Info Messages` and enter `no.blogspot.RsyncUI` as subsystem within the search field.

{{< figure src="/images/Xcode/console.png" alt="" position="center" style="border-radius: 8px;" >}}

# SwiftUI

SwiftUI is the latest declarative framework developed by Apple for views, controls, and layout structures for user interface. 

RsyncUI utilizes SwiftUI for the UI. UI components are views, which is a value type `struct` and not a reference type `class`. UI components are added to RsyncUI by code. Every time a property within a SwiftUI view is changed the view is recreated by the runtime. In SwitfUI there are several property wrappers to create bindings to mutable properties.

# Start of RsyncUI

The start of RsyncUI conforms to the [App protocol](https://developer.apple.com/documentation/SwiftUI/App). There is only one entrance point, `@main`, in RsyncUI. The `@main` initialises the app, setup of the menubar, and opens the navigation bar which is the main user start for the app.

# The model

SwiftUI views are *value types*, structs, and not *reference types*, classes, as in Storyboard and Swift. The model is responsible for informing the views when there are changes. The memory footprint of tasks is minimal. Data for tasks is kept in memory during the lifetime of RsyncUI. The memory footprint for logrecords will grow over time as new logs are created and stored. Logrecords are only read from the store when viewing and deleting logs. When data about logs is not used, the data is released from memory to keep the memory as low as possible.

# Property wrapper for objects

With Swift 5.9, Xcode 15 and macOS 14 Apple introduced the `@Observable` macro. On previous macOS versions, the property wrapper `@StateObject` in combination with `ObservableObject` and Combine, was used to create binding to mutable properties. The new macro *greatly simplifies* how to create bindings and there is also quite a boost in performance. The performance part is not that important for RsyncUI, but lesser code is better code.  There is also a new `@Bindable` property wrapper which create bindings to mutable properties of `@Observable` objects. 

All old property wrapper `@StateObject` in combination with `ObservableObject` and Combine are converted to the new macro.

# Dataflow in RsyncUI

The flow and handling of data are slightly different in the JSON-file vs SwiftData version.  Using SwiftData in RsyncUI is a test project for learning about SwiftData and check out if SwiftData and RsyncUI is a good match. From Apple Developement Documentations quote Apple: *"Combining Core Data’s proven persistence technology and Swift’s modern concurrency features, SwiftData enables you to add persistence to your app quickly, with minimal code and no external dependencies."*.  

There are *three files* saved to storage: tasks, log records and user settings.

## JSON 

All files are saved as JSON files and `Combine` is utilized to read and save data. JSON files are *encoded* before a write operation and *decoded* when read from storage. The encode and decode is requiered to represent JSON data as internal data within RsyncUI. Both reading data and saving data to JSON-files are explict actions in code.  When RsyncUI starts it reads *user configuration* and *data about tasks for the default profile*. The object holding data about tasks is an `@Observable` object created when RsyncUI starts.

```bash
 var rsyncUIdata: RsyncUIconfigurations {
        return RsyncUIconfigurations(selectedprofile)
    }
```
All views which require data about tasks get data by a mutable property wrapper `@Bindable var rsyncUIdata: RsyncUIconfigurations`.  Within `RsyncUIconfigurations` there is a observed variable holding the data structure about tasks. When tasks are updated, like timestamp last run, the class which executes the tasks does two jobs when executing tasks is completed. The internal datastructure is always updated. The first job is to send the changed updated datastructure up to the view by an *escaping closure*, `@escaping ([SynchronizeConfiguration]) -> Void)`. The view updates the observed variable holding the data structure about tasks and the SwiftUI runtime updates the views. The second job is to write the updates the permanent storage.

When there are changes on data the complete datastructure is written to file, like if there are 2000 logrecords and adding a new log record causes 2001 records to be written to the JSON-file. Data for the views are made avaliable by a `@Bindable` property and an `@Observable` object.  

## SwiftData 

[RsyncUISwiftData](https://github.com/rsyncOSX/RsyncUISwiftData) is the repository for the SwiftData version of RsyncUI.  One of the main differences compared to the JSON-file version of RsyncUI are that read and updates of data is taken care of by SwiftData. Every time a view needs data it is only requiered to use the `@Environment` to get the model and a `@Query` property wrapper to get the actal data data. 

```bash
struct Sidebar: View {
    @Environment(\.modelContext) private var modelContext
    @Query private var configurations: [SynchronizeConfiguration]
```

There are two database operations used, insert and delete. Updates of data is by selecting the record and update, SwiftData takes care of updating the database and informes the views to update. To use SwiftData there is an import of SwiftData Library. The datastructure in RsyncUI is a struct, but SwiftData requiere `@Model final class`, that is the structs holding the datamodels are modified to class:

```bash
import Foundation
import SwiftData

@Model
final class SynchronizeConfiguration: Identifiable {
    var id = UUID()
    var hiddenID: Int
    var task: String
    var localCatalog: String
    var offsiteCatalog: String
    var parameter1: String
    var parameter2: String
    var parameter3: String
    var parameter4: String
    var parameter5: String
    var parameter6: String
    var backupID: String
    var dateRun: String?
    // parameters choosed by user
    var parameter8: String?
    var parameter9: String?
    var parameter10: String?
    var parameter11: String?
    var parameter12: String?
    var parameter13: String?
    var parameter14: String?
    var profile: String = "Default profile"
   }
```
The datamodel is initialized when the app is starting, if first time the datastore is automatically created . 

```bash
 var sharedModelContainer: ModelContainer = {
        let schema = Schema([SynchronizeConfiguration.self,
                             UserConfiguration.self,
                             LogRecords.self,
                             Log.self])

        let storeURL = URL.documentsDirectory.appending(path: "rsyncui.sqlite")
        let configuration = ModelConfiguration(schema: schema, url: storeURL)

        do {
            return try ModelContainer(for: schema, configurations: [configuration])
        } catch {
            fatalError("Could not create ModelContainer: \(error)")
        }
    }()
```
The datamodel is made avaliable for all the views by:
```bash
Window("RsyncUI", id: "main") {
            RsyncUIView()
                .frame(minWidth: 1300, minHeight: 510)
        }
        .modelContainer(sharedModelContainer)
```

You can create relations and much more in SwiftData, but for RsyncUI there is no need for an advanced datamodel. When data is changed, like update timestamp or create a log, the changes are propogated up to the view which initiated the change. The data is updated to the database by SwiftData and SwiftUI updates the views on the fly.  

## Sorting  and filter logs - SwiftData vs JSON

Showing logcrecords by task, sorted by Date is done by getting the data by a `@Query` property using a Sortdescriptor. The View is *initialized* from the parent view sending in the UUID for the selected task, and a Predicate filter shows logs by UUID and a filter by date.

```bash
import SwiftData
import SwiftUI

struct LogRecordsTableByUUIDView: View {
    @Environment(\.modelContext) var modelContext
    @Query(sort: [SortDescriptor(\Log.dateExecuted, order: .reverse)])
    var records: [Log]

    @State private var selectedloguuids = Set<Log.ID>()
    // Alert for delete
    @State private var showAlertfordelete = false
    // Number of logs
    @Binding var number: Int

    var body: some View {
        Table(records, selection: $selectedloguuids) {
            TableColumn("Date") { data in
                let date = data.dateExecuted
                Text(date.en_us_date_from_string().localized_string_from_date())
            }

            TableColumn("Result") { data in
                Text(data.resultExecuted)
            }
        }
        .onAppear {
            number = records.count
        }
        .onDeleteCommand {
            showAlertfordelete = true
        }
        .overlay { if records.count == 0 {
            ContentUnavailableView {
                Label("There are no logs by this filter", systemImage: "doc.richtext.fill")
            } description: {
                Text("Try to search for other filter in Date or Result")
            }
        }
        }
        .sheet(isPresented: $showAlertfordelete) {
            DeleteLogsView(selectedloguuids: $selectedloguuids)
        }
    }

    init(sort: SortDescriptor<Log>, searchString: String, uuid: UUID, _ number: Binding<Int>) {
        _records = Query(filter: #Predicate {
            if searchString.isEmpty {
                return true && $0.logrecord?.id == uuid
            } else {
                return $0.dateExecuted.localizedStandardContains(searchString) && $0.logrecord?.id == uuid
            }
        }, sort: [sort])

        _number = number
    }
}
````
Filter and sort log records in JSON-file version is slightly different. The function get all log records, combine all arrays of records by `flatmap` and uses a standard filter function.

```bash
func updatelogs() async {
        if let logrecords = rsyncUIlogrecords.logrecords {
            if debouncefilterstring != "" {
                if hiddenID == -1 {
                    var merged = [Log]()
                    for i in 0 ..< logrecords.count {
                        merged += [logrecords[i].logrecords ?? []].flatMap { $0 }
                    }
                    // return merged.sorted(by: \.date, using: >)
                    let records = merged.sorted(using: [KeyPathComparator(\Log.date, order: .reverse)])
                    logs = records.filter { ($0.dateExecuted?.en_us_date_from_string().long_localized_string_from_date().contains(debouncefilterstring)) ?? false || ($0.resultExecuted?.contains(debouncefilterstring) ?? false)
                    }
                } else {
                    if let index = logrecords.firstIndex(where: { $0.hiddenID == hiddenID }) {
                        let records = (logrecords[index].logrecords ?? []).sorted(using: [KeyPathComparator(\Log.date, order: .reverse)])
                        logs = records.filter { ($0.dateExecuted?.en_us_date_from_string().long_localized_string_from_date().contains(debouncefilterstring)) ?? false || ($0.resultExecuted?.contains(debouncefilterstring) ?? false)
                        }
                    }
                }
            } else {
                if hiddenID == -1 {
                    var merged = [Log]()
                    for i in 0 ..< logrecords.count {
                        merged += [logrecords[i].logrecords ?? []].flatMap { $0 }
                    }
                    // return merged.sorted(by: \.date, using: >)
                    logs = merged.sorted(using: [KeyPathComparator(\Log.date, order: .reverse)])
                } else {
                    if let index = logrecords.firstIndex(where: { $0.hiddenID == hiddenID }) {
                        logs = (logrecords[index].logrecords ?? []).sorted(using: [KeyPathComparator(\Log.date, order: .reverse)])
                    }
                }
            }
        }
    }
```

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

- [read json ](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/ReadConfigurationJSON.swift) configuration file for tasks, only the JSON version of RsyncUI
- [write json](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/WriteConfigurationJSON.swift) configuration file for tasks, only the JSON version of RsyncUI
- [observing signals](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/Async/RsyncProcessAsync.swift) within the process object,
- debouncing input from user, filter strings and other values which are validated before saving

The user input for search or filter is by default a `@State` string variable. The view reacts on the input by every keypress and the filter algorithm is triggered by every keypress. This causes a sluggish user interface, but by debounce input by *a second* causes the filter algorithm only to update the view after the debounce period.

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

# How are tasks executed?

There are several ways to execute tasks:

- two double clicks on a task, first is an estimate run and second is the real run
- select task(s) and either estimate first or execute without estimation
- estimate first all tasks and then execute or execute all tasks without estimation

The following is a brief overview of *estimate first and then execute tasks*. The difference between an estimation run and a real run is; estimation run is a `--dryn-run` and there is no logging. An estimation run is commenced by selecting the *wand and stars* icon or shortcut `⌘E` from the main view. The navigation path for estimate all view is pushed onto the view stack and a progress informes which tasks are estimated. For each task the result of the estimation run is saved. After estimation RsyncUI marks tasks where there is data to synchronize. 

The user then select synchronize tasks and the navigation path for executing tasks including progress of each is pushed onto the view stack. From this view the reference of the class with data from estimation is passed onto the class which executes the tasks. The id for each task is pushed onto a stack and the class executing tasks is not released until the stack is emtpy and a process termination signal is observed from the last task. The progess of synchronizing is communicated to the progress view by an *escaping closure*, `@escaping (Int) -> Void)`. 

The execution of tasks is equal in both versions, but the update of data is different. That is reflected by the input parameters to `func executemultipleestimatedtasks()` which kicks of synchronization of all estimated tasks and data to be synchronized. 

## JSON

When the execution of tasks are completed the updated data is writen to JSON files from within the `func executemultipleestimatedtasks()`. The updated data is feed back to the `@Bindable` object by the `func updateconfigurations(_ configurations: [SynchronizeConfiguration])` which also causes the UI to be updated by SwiftUI.

```bash
func executemultipleestimatedtasks() {
        var uuids: Set<SynchronizeConfiguration.ID>?
        if selecteduuids.count > 0 {
            uuids = selecteduuids
        } else if executeprogressdetails.estimatedlist?.count ?? 0 > 0 {
            let uuidcount = executeprogressdetails.estimatedlist?.compactMap { $0.id }
            uuids = Set<SynchronizeConfiguration.ID>()
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

    func updateconfigurations(_ configurations: [SynchronizeConfiguration]) {
        rsyncUIdata.configurations = configurations
    }
    
     func filehandler(count: Int) {
        progress = Double(count)
    }
```
## SwiftData

All changes of data, e.g. only the changes, are braught back to the calling view by the two functions `func updatedates(_ configrecords: [Typelogdata])` and  `func updatelogrecords(_ logrecords: [Typelogdata])`. The updates are feed back to the calling view and data is updated on the fly. The update causes the views to update as well by SwiftData.

```bash
func executemultipleestimatedtasks() {
        var uuids: Set<SynchronizeConfiguration.ID>?
        if selecteduuids.count > 0 {
            uuids = selecteduuids
        } else if executeprogressdetails.estimatedlist?.count ?? 0 > 0 {
            let uuidcount = executeprogressdetails.estimatedlist?.compactMap { $0.id }
            uuids = Set<SynchronizeConfiguration.ID>()
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
                                 configurations: configurations,
                                 multipletaskstateDelegate: multipletaskstate,
                                 executeprogressdetailsDelegate: executeprogressdetails,
                                 filehandler: filehandler,
                                 updatedates: updatedates,
                                 updatelogrecords: updatelogrecords)
        }
    }

    func updatedates(_ configrecords: [Typelogdata]) {
        for i in 0 ..< configrecords.count {
            let hiddenID = configrecords[i].0
            let date = configrecords[i].1
            if let index = configurations.firstIndex(where: { $0.hiddenID == hiddenID }) {
                // Caution, snapshotnum already increased before logrecord
                if configurations[index].task == SharedReference.shared.snapshot {
                    if let num = configurations[index].snapshotnum {
                        configurations[index].snapshotnum = num + 1
                    }
                }
                configurations[index].dateRun = date
            }
        }
    }

    func updatelogrecords(_ logrecords: [Typelogdata]) {
        if SharedReference.shared.detailedlogging {
            for i in 0 ..< logrecords.count {
                let hiddenID = logrecords[i].0
                let stats = logrecords[i].1
                let currendate = Date()
                let date = currendate.en_us_string_from_date()
                if let index = configurations.firstIndex(where: { $0.hiddenID == hiddenID }) {
                    var resultannotaded: String?
                    if configurations[index].task == SharedReference.shared.snapshot {
                        if let snapshotnum = configurations[index].snapshotnum {
                            resultannotaded = "(" + String(snapshotnum - 1) + ") " + stats
                        } else {
                            resultannotaded = "(" + "1" + ") " + stats
                        }
                    } else {
                        resultannotaded = stats
                    }
                    var inserted: Bool = addlogexisting(hiddenID,
                                                        resultannotaded ?? "",
                                                        date)
                    // Record does not exist, create new LogRecord (not inserted)
                    if inserted == false {
                        inserted = addlognew(hiddenID, resultannotaded ?? "", date)
                    }
                }
            }
        }
    }
    
     func filehandler(count: Int) {
        progress = Double(count)
    }
```