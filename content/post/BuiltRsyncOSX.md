+++
author = "Thomas Evensen"
date = "2021-01-01"
title =  "How are RsyncOSX built?"
tags = ["built"]
categories = ["general information"]
lastmod = "2021-01-01"
+++

This is only a very short overview of some details about RsyncOSX.

# RsyncOSX, Storyboard

*RsyncOSX* utilizes *Storyboard*, which is a tool for graphical design of views. UI components like buttons, tables and other UI components are added and placed within the view by the developer utilizing Xcode. After design all UI components are connected by creating bindings to Swift code. The developer manually adds a reference to the Swift source code for every view within the Storyboards and the UI components within the views. If the developer misses to bind a UI component, the app will crash with an nil pointer exception every time that view is exposed.

## Storyboard for the tab views

Xcode supports multiple storyboards. For RsyncOSX there is created two storyboards, *tab views* which are the main views and *sheetviews* which are pop-up views.

{{< figure src="/images/Xcode/storyboard1.png" alt="" position="center" style="border-radius: 8px;" >}}

## Storyboard for the sheetviews

And for every UI component within a storyboard it is requiered to manually bind it. And then there are constraints to control where UI components are placed and position when the UI is resized.

{{< figure src="/images/Xcode/storyboard2.png" alt="" position="center" style="border-radius: 8px;" >}}

To be honest, it is way easier to work with SwiftUI and not Storyboards. 

# Start of RsyncOSX

The start of RsyncOSX starts with the attribute `@NSApplicationMain` which kicks off everything. Within the Storyboard, the entry point is marked, and the view is binded with the Switf code to start the application. The Toolbar is programmatically constructed, which makes it easier to change vs. designing it on the Storyboard.



