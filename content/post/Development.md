+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "The development of RsyncUI"
tags = ["SwiftUI"]
# categories = ["SwiftUI"]
description = "Why is the development of RsyncUI based on SwiftUI?"
lastmod = "2021-03-12"
+++
The development of RsyncUI commenced in December 2020 and [version 1.0.0 was released](https://github.com/rsyncOSX/RsyncUI/releases) in May 2021. The name is **RsyncUI** and it is built for **macOS Big Sur** and later. That is why it is released as a new appliction and not as an upgrade the current version of RsyncOSX. There are also some SwiftUI features in code which require macOS Big Sur.

[SwiftUI](https://developer.apple.com/documentation/swiftui/) was released in 2019 and is a new **declarative framework** for UI development across the various Apple operating systems. It is still young and in development. Developing the UI based on SwiftUI compared to developing utilizing the [Cocoa](https://en.wikipedia.org/wiki/Cocoa_(API)) framework is a huge step forward. The code for the UI utilizing SwiftUI is minimal and easily separated from the Model (MVC). By hiding application logic in properties, functions and closures will simplify the code. The declarative paradigm also makes the code for the UI cleaner and more easy to follow.

The future of development on the Apple plattform is SwiftUI. Not only by SwiftUI, but in companion with the other Swift and Objective-C frameworks.

Less code is better code.

[Combine](https://developer.apple.com/documentation/combine) is also a new **declarative framework** from Apple. In RsyncUI it is used for asynchronous tasks like validate user input, listening for notifications from the NotificationCenter, decode and encode JSON data and checking, trimming and verify the output from rsync.

There are some more details about the use of Combine in [the details about development](/post/developmentdetails/).

## The source code

The source is available on my [GitHub account](https://github.com/rsyncOSX/RsyncUI). If you have any comments or ideas please use [the discussion part for RsyncUI](https://github.com/rsyncOSX/RsyncUI/discussions).

## Resources to learn SwiftUI and Combine

There are a lot of resources to learn SwiftUI. Google, Stack Overflow, YouTube and GitHub are amongst the most used resources. I am also following a few blogs like:

- [Paul Hudson´s Hacking With Swift](https://www.hackingwithswift.com/)
- [John Sundell´s Swift by Sundell](https://swiftbysundell.com/)
- [Dave Werver´s iOS Dev Weekly](https://iosdevweekly.com/)
- [Apple tutorials about developing in SwiftUI](https://developer.apple.com/tutorials/app-dev-training)

There are also several resources available for the Combine framework. I will like to point the following resources:

- [Matt Neuburg´s Understanding Combine,](https://www.apeth.com/UnderstandingCombine/)
- [Joseph Heck´s Using Combine](https://heckj.github.io/swiftui-notes/)
- [PhysicsNerd´s  YouTube SwiftUI channel](https://www.youtube.com/c/PhysicsNerdDev/featured)
