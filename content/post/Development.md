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

[SwiftUI](https://developer.apple.com/documentation/swiftui/) is a framework for UI. Compared to a Swift, Storyboard and View Controllers application, the numbers of codelines to create the UI with SwiftUI is minimal. And SwiftUI is a **declarative framwork**.

[Combine](https://developer.apple.com/documentation/combine) is also a new **declarative framework** from Apple. I am using it primarly for asynchronous tasks like validate input and listening for (two) notifications from the NotificationCenter. Those two notifications are very important for RsyncUI to work. They must be reliable and whenever they are triggered RsyncUI must catch them.

The future of development on the Apple plattform is SwiftUI. The code for the UI utilizing SwiftUI is minimal and easily separated from the Model (MVC). By hiding application logic and actions in properties, functions and closures will simplify the code and make more easy to read. The declarative paradigm makes the code for the UI cleaner and more easy to follow.

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

Another important aspect of SwiftUI is the [single source of truth](https://developer.apple.com/documentation/swiftui/managing-user-interface-state). Single source of truth is also an important part of the MVC architecture.
