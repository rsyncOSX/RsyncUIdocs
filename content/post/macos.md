+++
author = "Thomas Evensen"
date = "2023-01-01"
title =  "MacOS versions and RsyncUI"
tags = ["macOS"]
categories = ["general information"]
+++

On every new release of macOS, Swift, SwiftUI and Xcode there are new features only supporting the latest release. RsyncUI is not an advanced application, but there are some features only available on each version of macOS.  With Swift 5.9, Xcode 15 and macOS 14 Apple introduced the `@Observable` macro. On previous macOS versions, the property wrapper `@StateObject` in combination with `ObservableObject` and Combine, are used to create binding to mutable properties. The new macro simplifies how to create bindings and there is also quite a boost in performance. The performance part is not that important for RsyncUI, but lesser code is better code.  There is also a new `@Bindable` property wrapper which create bindings to mutable properties of `@Observable` objects. 

## MacOS 14 Sonoma

There are two versions of RsyncUI supporting macOS Sonoma. The default version is available from Homebrew and supports macOS Monterey and later. And there is a build for macOS Sonoma only which includes migrating  objects and bindings to the new `@Observable` macro. Migrating code to the new macro is a *breaking change* and that is why there are two builds. 

On macOS 14 is the `ContentUnavailableView`, an interface, which display when the content is unavailable. If the user enters a filter search with no result the new interface displays a default view.

{{< figure src="/images/macos/ContentUnavailable.png" alt="" position="center" style="border-radius: 8px;" >}}

## MacOS 13 Ventura and later

Features only available on macOS Ventura and later:

- within the main view, double click on row for estimate and execute
- within the Tasks view ( Add tasks),  copy and paste tasks by shortcuts `⌘C` and  `⌘V` and Edit menu

## MacOS 12 Monterey

On macOS Monterey, *double-click* on a task is *not available*. The only way to check the output from an estimation run within the main view on macOS 12 is to estimate all tasks, dismiss the estimated view, and check the output from rsync the i from the toolbar main view.


Select the *wand and stars* on the toolbar for estimate all tasks.
 
{{< figure src="/images/macos/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

After the estimate run, *Dismiss*  the view.

{{< figure src="/images/macos/resultestimate.png" alt="" position="center" style="border-radius: 8px;" >}}

From the main view select a task and the *i* from the toolbar.

{{< figure src="/images/macos/estimatemain.png" alt="" position="center" style="border-radius: 8px;" >}}

And the result of the estimation run is displayed.

{{< figure src="/images/macos/dryrun.png" alt="" position="center" style="border-radius: 8px;" >}}
