+++
author = "Thomas Evensen"
title = "The RsyncUI changelog"
date = "2021-03-11"
description = "Changelog"
tags = ["RsyncUI"]
categories = ["changelog"]
lastmod = "2021-03-11"
+++
If you are utilizing a local version of rsync, execute the rsync utility in a terminal window before using RsyncUI. There is a process of granting access for the rsync utility before using it by RsyncUI. MacOS will also ask permission for accessing your home catalog the first time you start RsyncUI. If you also utilize the menu-app (RsyncUIsched), be aware of you might have to force quit RsyncUI the first time you start the menu-app. This is because the macOS asks for permissions when starting the menu-app for the first time and RsyncUI is not closed automatically when starting the menu-app. This might happen only once first time start.

**THIS SITE IS WORK IN PROGRESS**

The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur. There is a [todo list](/post/todo/), please read it before commencing the use of the prerelease.

RsyncUI is [signed and notarized](/post/notarized/). Please see info about [the latest version of rsync in install](/post/rsync/).

Using RsyncUI requires some knowledge of `rsync`. The main objective for RsyncUI is to ease the use of `rsync`, not teach macOS users how to use `rsync`. That is beyond the scope of RsyncUI. Setting the wrong parameters to rsync can result in deleted data. And RsyncUI will not stop you for doing so. That is why it is very important to execute a simulated run (`--dry-run`) and inspect what happens before a real run.

## Prerelease v0.35(7)

There is 13 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- the user settings is updated, there were a few bugs in previous version
- the documentation for [user settings is also updated](/post/userconfiguration/)
- with this release there is about three months since I commenced the preparation and work on RsyncUI
- RsyncUI will probably be released in version 1.0 in about two or three months, either late in May or beginning of June 2021
- as the development progresses new testreleases will be available

## Prerelease v0.3(6)  

There is 12 March 2021 [released a test version](https://github.com/rsyncOSX/RsyncUI/releases). The testversion can be used in parallel with RsyncOSX.
