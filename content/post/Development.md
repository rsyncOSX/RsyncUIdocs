+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "The development of RsyncUI"
tags = ["SwiftUI"]
categories = ["SwiftUI"]
description = "Why is the development of RsyncUI based on SwiftUI?"
lastmod = "2021-03-12"
+++
The development of RsyncUI commenced in December 2020 and will be released sometime in June or July 2021. The name of the next version is **RsyncUI**. It is built for **macOS Big Sur** and later, that is why it will be released as a new appliction and not replace the current version of RsyncOSX.

[SwiftUI](https://developer.apple.com/documentation/swiftui/) is a new **declarative framework** for UI. Developing the UI based on SwiftUI compared to developing utilizing the [Cocoa](https://en.wikipedia.org/wiki/Cocoa_(API)) framework is a huge step forward. And the future of development on the Apple plattform is SwiftUI. Not only by SwiftUI, but in companion with the other Swift and Objective-C frameworks.

[SwiftUI](https://en.wikipedia.org/wiki/Swift_(programming_language)) was released in 2019 and it is still young and in development. The code for the UI utilizing SwiftUI is minimal and easily separated from the Model (MVC). By hiding application logic in properties, functions and closures will simplify the code. The declarative paradigm also makes the code for the UI cleaner and more easy to follow.

[Combine](https://developer.apple.com/documentation/combine) is also a new **declarative framework** from Apple. In RsyncUI it is used primarly for asynchronous tasks like validate input and listening for (two) notifications from the NotificationCenter. Those two notifications are very important for RsyncUI to work. It must be reliable and whenever they are triggered RsyncUI must catch them.

The development of RsyncOSX began early in 2016. RsyncOSX is a pure Swift, Cocoa and Foundation, based application. The future generation of RsyncOSX is RsyncUI, a SwiftUI and Swift (Foundation) based application.

## About the development and progress

There are some more info about the progress in [the todo list](/post/todo/). Also check out the [changelog](/post/changelog/). Most of the core basic functions like executing tasks, compute the parameters to rsync are reused code from the current version. And most of the executing part is stable and working.

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

The following are som high level info about how RsyncUI is developed.

### Basic data structure

The basic datastructures in RsyncUI are two arrays of structs: configurations as Array<[Configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/Configuration.swift)> and logs- and schedules as Array<[ConfigurationSchedule](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/ConfigurationSchedule.swift)>. During start and load of data all rsync parameters for all configurations are [computed](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift). The main [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcessCmdCombineClosure.swift) reads all arguments as an Array\<String\> ahead of execution. The [compute](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift) object reads and prepares all rsync parameters as Array\<String\> as part of start and load of data.

Any change to the basic data structures causes RsyncUI to write data to permanent storage, reload data and recompute rsync parameters.

### MVC architecture

RsyncUI is constructed in compliance to the Model View Controller (MVC) architecture. Any operations on the data is within the model. The modelpart is normal **imperativ** Swift development, with classes and structs. The UI part (view) is **declarative** SwiftUI development, with structs only. The UI is clearly separated from the model. Another important part of SwiftUI is the [single source of truth](https://developer.apple.com/documentation/swiftui/managing-user-interface-state).

### Permanent storage

RsyncUI saves data on permanent store either as PLIST or JSON format. The user can any time convert existing data to either of the formats. There is no preferences of which format to use and default is PLIST. JSON is a preferred format for exchanging data on the Internet and Swift has very good support for encoding and decoding JSON.

Details about JSON encoding and decoding of configurations are [here](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/PersistentStorage/PersistentStorageConfigurationJSON.swift). And details about PLIST encoding and decoding of configurations er [here](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/PersistentStorage/PersistentStorageConfigurationPLIST.swift).

The same is for logs- and schedules. See also where RsyncUI [saves data](/post/configfiles/).

### User settings

Some settings within RsyncUI can be changed by the user. The settings are read by RsyncUI ahead of loading the data. All usersettings are stored within a [singelton object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/SharedReference.swift) which stays alive during the lifetime of RsyncUI. This is the one and only singelton object.

### The UI

Each view is small. By hiding most of the logic within the UI in computed properties, functions and closures, the structure of the UI is easy to follow. The view [AddConfigurationView.swift](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Add/AddConfigurationView.swift) is an example of that. The structure of the view is less than 80 lines of code, the details is within each computed property.

The Add view are put together of two columns and two buttons in right corner. The properties, like `localandremotecatalog` are computed and details about it are hidden within the property itself.

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
                           Button(action: { createprofile() }) { Image(systemName: "plus") }
                           .buttonStyle(GrayCircleButtonStyle())
                           EditValue(100, NSLocalizedString("New profile", comment: "settings"), $newprofile)
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

### Execution of tasks

Execution of a task is an asynchronous operation. The [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcessCmdCombineClosure.swift) is responsible for kicking of the task. Combine is used for listening for two notifications, `Process.didTerminateNotification` and `NSNotification.Name.NSFileHandleDataAvailable`. The process object is initialized with two escaping closures, `processtermination: @escaping () -> Void` and `filehandler: @escaping () -> Void`. Those two closures takes care of whatever action they are set to do any time the notifications are discovered.

### Combine

Combine is used in RsyncUI. It enables a very good control of asynchronous operations and flow of data. As an example of use is validating user data. The Views (SwiftUI) are connected to an `ObservableObject` utilizing Combine and the connection between the `ObservableObject` and the view is by `Binding`. Below is how SSH values are validated. The ObservableObject is a StateObject in the view and by Bindings data is communicated between the view and StateObject.

The [code snippet](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/ObservableReferenceSSH.swift) for the StateObject:

```
import Combine
import Foundation

class ObservableReferenceSSH: ObservableObject {
    // When property is changed set isDirty = true
    @Published var isDirty: Bool = false
    // Global SSH parameters
    // Have to convert String -> Int before saving
    // Set the current value as placeholder text
    @Published var sshport: String = ""
    // SSH keypath and identityfile, the settings View is picking up the current value
    // Set the current value as placeholder text
    @Published var sshkeypathandidentityfile: String = ""
    // If local public sshkeys are present
    @Published var localsshkeys: Bool = SshKeys().validatepublickeypresent()
    // Value to check if input field is changed by user
    @Published var inputchangedbyuser: Bool = false
    // Combine
    var subscriptions = Set<AnyCancellable>()

    init() {
        $inputchangedbyuser
            .sink { _ in
            }.store(in: &subscriptions)
        $sshkeypathandidentityfile
            .debounce(for: .seconds(2), scheduler: globalMainQueue)
            .sink { [unowned self] identityfile in
                sshkeypathandidentiyfile(identityfile)
            }.store(in: &subscriptions)
        $sshport
            .debounce(for: .seconds(2), scheduler: globalMainQueue)
            .sink { [unowned self] port in
                sshport(port)
            }.store(in: &subscriptions)
    }

    // SSH identityfile
    private func checksshkeypathbeforesaving(_ keypath: String) throws -> Bool {
        ..
    }

    func sshkeypathandidentiyfile(_ keypath: String) {
        guard inputchangedbyuser == true else { return }
        // If keypath is empty set it to nil, e.g default value
        guard keypath.isEmpty == false else {
            SharedReference.shared.sshkeypathandidentityfile = nil
            isDirty = true
            return
        }
        do {
            let verified = try checksshkeypathbeforesaving(keypath)
            if verified {
                SharedReference.shared.sshkeypathandidentityfile = keypath
                isDirty = true
            }
        } catch let e {
            let error = e
            self.propogateerror(error: error)
        }
    }

    // SSH port number
    private func checksshport(_ port: String) throws -> Bool {
        ..
    }

    func sshport(_ port: String) {
        guard inputchangedbyuser == true else { return }
        // if port is empty set it to nil, e.g. default value
        guard port.isEmpty == false else {
            SharedReference.shared.sshport = nil
            isDirty = true
            return
        }
        do {
            let verified = try checksshport(port)
            if verified {
                SharedReference.shared.sshport = Int(port)
                isDirty = true
            }
        } catch let e {
            let error = e
            self.propogateerror(error: error)
        }
    }
}
```
and the [code snippet](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Settings/Sshsettings.swift) for the View is:

```
struct Sshsettings: View {
    @EnvironmentObject var rsyncOSXData: RsyncOSXdata
    @StateObject var usersettings = ObservableReferenceSSH()
    @Binding var selectedconfig: Configuration?
    @Binding var reload: Bool

    @State private var selectedlogin: UniqueserversandLogins?
    @State private var showingAlert: Bool = false
    @State private var showsshverifysheet: Bool = false

    var body: some View {
        Form {
            HStack {
                // For center
                Spacer()
                // Column 1
                VStack(alignment: .leading) {
                    HStack {
                        ToggleView(NSLocalizedString("Local ssh keys found", comment: "ssh"), $usersettings.localsshkeys)

                        VStack {
                            Button(NSLocalizedString("Create", comment: "usersetting")) { createkeys() }
                                .buttonStyle(PrimaryButtonStyle())

                            Button(NSLocalizedString("Verify", comment: "usersetting")) { verifyssh() }
                                .buttonStyle(PrimaryButtonStyle())
                        }
                    }

                    Section(header: headerssh) {
                        setsshpath

                        setsshport
                    }

                }.padding()

                // Column 2
                VStack(alignment: .leading) {
                    Section(header: headeruniqueue) {
                        uniqueuserversandloginslist
                    }
                }.padding()

                // For center
                Spacer()
            }
            // Save button right down corner
            Spacer()

            HStack {
                Spacer()

                usersetting
            }
        }
        .lineSpacing(2)
        .padding()
        .sheet(isPresented: $showsshverifysheet) {
            VerifySshView(selectedlogin: $selectedlogin,
                          isPresented: $showsshverifysheet)
        }
    }
```
