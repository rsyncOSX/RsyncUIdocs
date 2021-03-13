+++
author = "Thomas Evensen"
date = "2021-03-12"
title =  "Next version"
tags = ["swiftui, nextversion"]
categories = ["swiftui"]
description = "Some info about SwiftUI version of RsyncOSX"
lastmod = "2021-03-12"
+++
The development of next version commenced in December 2020 and the release of RsyncUI will be sometime before summer 2021. The name of the next version is **RsyncUI**. It is built for **macOS Big Sur** and later, that is why it will be released as a new appliction and not replace the current version of RsyncOSX.

SwiftUI is **a framework for UI**. Compared to a Swift, Storyboard and View Controllers application, the numbers of codelines to create the UI with SwiftUI is minimal. Programming the UI in SwiftUI is **declarative** and not imperativ. The code for the model part is traditional Swift code.

And to be honest, **the future of RsyncOSX is SwiftUI**. And it is **really fun to code in SwiftUI**. The code for UI is minimal and separated from the Model (MVC). By hiding application logic and actions in properties, functions and closures will simplify the code and make more easy to read. The declarative paradigm makes the code for the UI cleaner and more easy to follow.

## About the development and progress

There are some more info about the progress in [the todo list](/post/todo/). Also check out the [changelog for changes and updates](/post/changelog/)

The final version will be released sometime closer to summer 2021. Most of the core basic functions like executing tasks, compute the parameters to rsync are reused code from the current version. And most of the executing part is stable and working.

## The source code

The source is available on my [GitHub account](https://github.com/rsyncOSX/RsyncUI). If you have any comments or ideas please use [the discussion part for RsyncUI](https://github.com/rsyncOSX/RsyncUI/discussions).

## Resources to learn SwiftUI

There are a lot of resources to learn SwiftUI. Google, Stack Overflow, YouTube and GitHub are amongst the most used resources. I am also following a few blogs like:

- Paul Hudson´s, [Hacking With Swift](https://www.hackingwithswift.com/)
- John Sundell´s, [Swift by Sundell](https://swiftbysundell.com/)
- Sean Allen´s [swift news](https://github.com/SAllen0400/swift-news)
- Dave Werver´s [iOS Dev Weekly](https://iosdevweekly.com/)
- [Apple tutorials about developing in SwiftUI](https://developer.apple.com/tutorials/app-dev-training)

Another important aspect of SwiftUI is the [single source of truth](https://developer.apple.com/documentation/swiftui/managing-user-interface-state). Single source of truth is also an important part of the MVC architecture.
