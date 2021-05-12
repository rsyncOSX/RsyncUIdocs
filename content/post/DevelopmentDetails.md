+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "Development details"
tags = ["SwiftUI"]
# categories = ["SwiftUI"]
description = "How is RsyncUI developed?"
lastmod = "2021-03-12"
+++
RsyncUI is developed in compliance to the Model View Controller (MVC) architecture. Any operations on the data is within the model part. The modelpart is mostly traditional **imperativ** Swift development, with classes and structs. The model classes does also utilize the Combine framework. See the Combine part below for more details. The UI part (view) is **declarative** SwiftUI development, with structs only. The UI is clearly separated from the model. Another important part of SwiftUI is the [single source of truth](https://developer.apple.com/documentation/swiftui/managing-user-interface-state).

## Basic datastructure

The basic datastructures in RsyncUI are two arrays of structs: configurations as Array<[Configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/Configuration.swift)> and logs- and schedules as Array<[ConfigurationSchedule](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/ConfigurationSchedule.swift)>. The actual parameters for a task are [computed](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift) as part of prepare for the run. All parameters are based on data for each configuration. The main [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift) reads all arguments as an Array\<String\> ahead of execution. The [compute](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/ComputeParametersRsync/ComputeRsyncParameters.swift) object reads and computes all rsync parameters as Array\<String\> ahead of executing a task.

Any change to the basic data causes RsyncUI to write the complete data to permanent storage and read it again. This is a simple and a kind of "brute force" way to secure that data is consistent and there is no need for functions to handle changed data. Every time there is dirty data, write all data and read it again.

## Permanent storage

RsyncUI saves data on permanent store as files with JSON data. JSON is the preferred format for exchanging data on the Internet and Swift has very good support for decode and encode JSON. See more info about this within the Combine part below. See also where RsyncUI [saves data](/post/configfiles/).

## User settings

Some settings within RsyncUI can be changed by the user. The settings are read by RsyncUI ahead of loading the data. All usersettings are stored within a [singelton object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/SharedReference.swift) which stays alive during the lifetime of RsyncUI. This is the one and only singelton object.

## The UI

Each view is small. By hiding most of the logic within the UI in computed properties, functions and closures, the structure of the UI is easy to follow. See sample of [code snippet for the add view](/post/codesnippetview/).

## Reading data

Configurations, logs and scedules are read from permanent store into an `ObservableObject` [RsyncUIdata](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Data/RsyncUIdata.swift). The data is read only and made available for the various views as a `@EnvironmentObject`. Everytime there is a change to the data, the changes are handled by the model, saved to permanent store and reloaded.

## Execution of tasks

Execution of a task is an asynchronous operation. The [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift) is responsible for kicking of the task. Combine is used for listening for two notifications, `Process.didTerminateNotification` and `NSNotification.Name.NSFileHandleDataAvailable`. The process object is initialized with two escaping closures, `processtermination: @escaping () -> Void` and `filehandler: @escaping () -> Void`. Those two closures takes care of whatever action they are set to do any time the notifications are discovered.

## Combine

Combine enables a very good control of asynchronous operations and flow of data. As an example of use is validating of input from the user. The SwiftUI views are connected to an `ObservableObject`. The flow of data between the `ObservableObject` and the view is by `Binding` and the Combine framework. The ObservableObject is a StateObject in the view and by Bindings data is communicated between the view and StateObject.

- see [code snippet for ObservableReference](/post/codesnippetobserver/)
- see [code snippet for SSH settings View](/post/codesnippetviewssh/)

Combine is a complex framework to learn. It is though still easy and elegangt to use. More complex use of Combine take some time to learn. The following are parts where Combine also are used in RsyncUI:

- at startup [a check](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Newversion/NewversionJSON.swift) if there is a new version of RsyncUI available
  - there is a [JSON-file](https://github.com/rsyncOSX/RsyncUI/blob/main/versionRsyncUI/versionRsyncUI.json) with versions to update and url-link to the new version
- [reading and decoding JSON data](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/ReadConfigurationJSON.swift) from permanent storage into theire respective datastructures (configurations as Array<[Configurations](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/Configuration.swift)> and schedules as Array<[ConfigurationSchedule](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/Basic/ConfigurationSchedule.swift)>)
- encoding the above datastructures to [JSON data and writing data](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Storage/WriteConfigurationJSON.swift) to permanent storage
- subscribe, within the [process object](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Process/Main/RsyncProcess.swift), for notifications from the NotificationCenter
- parsing output from the above process object like [trimming and preparing output](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Output/TrimTwo.swift) from a rsync task, this trimming also looks for the string `error` in the output and reports if found

## Speed

SwiftUI refreshes the view every time there is a change on a `<Binding>`. And there are also several other happenings which causes a refresh of the view. If there are, within the view, properties which are computed it might become an issue. There can be several hundred log records each task. If sorting and filtering of logs are computed properties within a view it can become an speed issue aka *spinning beach ball*. Therefore are all sorting and filtering of logs computed within the [RsyncUIdata](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Data/RsyncUIdata.swift) object and the result is set to the `<Binding>` value after the sort or filtering is completed.

The above also apply to the restore function. Getting the remote filenames of synchcronized data might be huge, several hundred thousand or millions of lines. It is after the completion of getting filenames and filtering, the result is set to a `<Binding>` value which causes a refresh.
