+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Code snippet for the AddConfigurationView"
tags = ["SwiftUI","code snippets"]
categories = ["SwiftUI"]
description = "Why is the development of RsyncUI based on SwiftUI?"
lastmod = "2021-04-06"
+++
The [AddConfigurationView.swift](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Add/AddConfigurationView.swift) view are put together of two columns and two buttons in right corner. The properties, like `localandremotecatalog` are computed and details about it are hidden within the property itself.

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
