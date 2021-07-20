+++
author = "Thomas Evensen"
title = "The RsyncUI changelog"
date = "2021-03-11"
description = "Changelog"
tags = ["RsyncUI"]
# categories = ["changelog"]
lastmod = "2021-05-06"
+++
There are a few significant changes in the updated SwiftUI 3 and macOS 12, please see more info about [changes in RsyncUI on macOS 12](/post/macos12/).

The builds are considered as beta versions even if version number is greater than one. The builds are stable and they are working. But the UI needs some more polish and QA, and the next version is 1.2.0(build xx) when macOS Monterey is released. The betas, version 1.1.2(build xx), will be updated when there are new updates in code.

## Version 1.1.2(build 32) - updated 20 July 2021

New [build](https://github.com/rsyncOSX/RsyncUI/releases) for public beta of MacOS Monterey, build by Xcode 13 beta 3. There is still some issues with localization, builds are English only.

The build for macOS Big Sur is **removed**, there are many changes in Xcode 13, SwiftUI 3 and macOS Monterey compared to current official releases from Apple

The macOS Monterey version includes enhancements only available for macOS Monterey.
- the buttons and togge buttons are changed
- the multiple tasks and single tasks view buttons for estimate and execute are "cleaned up"
  - in both views select the execute button executes the task(s) in one go
  - or estimate, view estimate and then execute
- the schedules view is changed as well
  - it is required some more QA on the schedules
- the log views and filter logs are updated, both all logs and by configuration
- and some internal stuff refactored

The QA and cleanup of UI continues on the road to release on macOS Monterey.

## Version 1.1.2(build 28)

There is 29 June 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.1.2 of RsyncUI. There are two builds, one for macOS Big Sur and one for macOS Monterey.

At start of the macOS Big Sur version select, from the drop down, either the "Default profile" or other profile if used. This is **not** required on RsyncUI on macOS Monterey. RsyncUI on macOS Monterey picks the default profile when selecting a task.

- RsyncUI conforms [the App protocol](https://developer.apple.com/documentation/swiftui/app)
- the UI is cleaned up a bit
- several internal changes
- RsyncUI adapts to some changes in macOS settings, see link about [RsyncUI on macOS Monterey](/post/macos12/)

The localization of RsyncUI is somewhat refactored. For the moment RsyncUI is localized to German and Norwegian, and there are a few strings missing in the release candidate. See more info about localization in [RsyncUI on macOS Monterey](/post/macos12/).

## Version 1.1.1(build 27)

**Update 17 June 2021**. The builds are removed for the moment.

There is 4 June 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.1.1 of RsyncUI. The following is fixed in this release:

- refactored parts of decode and encode JSON, Combine is a super framework
- refactored a few other parts as well
- SwiftUI require some computed properties, like UUID, on data
  - these properties are added during reading data, by mistake these properties was also written to file
  - this is now fixed and the filesize, specially the logs file, is reduced
- existing users of RsyncOSX using defalt format for storing data (PLIST) now can use RsyncUI to [transform default PLIST data](/post/plist/) to JSON which is required in RsyncUI

## Version 1.1.0(build 26)

There is 21 May 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.1.0 of RsyncUI. The following is fixed in this release:

- after a delete of a profile, reload of existing profile names
- a minor update in UI for post and pretask (clearing the input fields)
- more internals using the Combine framework, check about [Combine in development details](/post/developmentdetails/#combine)
- some cleaning up and minor refactor
- a minor bug in executing shell scripts
- updates to [the UI for adding and updating Configuration](https://rsyncui.netlify.app/post/addconfigurations/)
- updates to [the UI for adding shell scripts](https://rsyncui.netlify.app/post/shellout/)

## Version 1.0.1(build 24)

There is 12 May 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.0.1 of RsyncUI and RsyncSchedule.

The following are changes compared to previous releases:

- delete a Profile
- administration of Snapshots
  - the issue with snapshots and remote catalogs is solved
  - save plan and day on a snapshot task
  - delete old snapshots
- a few minor cleanups and enhancements in the UI part

## Version 1.0.0(build 23)

There is 06 May 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.0.0 of RsyncUI and RsyncSchedule, the menu app for executing scheduled tasks. The **snapshot administration**, like delete old snapshots, is still not yet completed. The work on snapshot administration is going forward and it will be released as an update of RsyncUI. But there are a few issues which has to be resolved before release.

The following are changes compared to previous releases:

- German and Norwegian localizations are updated
- even more use of the Combine framework
- a few internal updates and UI updates

Issue: there is an issue, in Snapshots, selecting a snapshot task and collecting remote data for snapshotcatalogs. The UI will notify if it seems to be such an issue.

About **JSON**: see note on the release 0.99.

## Prerelease version 0.99(build 22)

There is 28 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a release candidate of RsyncUI and RsyncSchedule, the menu app for executing scheduled tasks.

The following are changes compared to previous release:

- German and Norwegian localization is completed
- more use of the Combine framework
- split two "busy" UIs into two views, schedules and rsync parameters
- some minor tweaks in preparation for release of version 1.0.0

**Caution**: RsyncUI can be used in **parallel with RsyncOSX**. But that requires **RsyncOSX** to be setup to use **JSON files** and that the files for permanent storage is in the same catalog as RsyncUI. RsyncUI and RsyncOSX does **not** share the user settings.

There is some more info about [how to setup RsyncOSX utilizing JSON](https://rsyncosx.netlify.app/post/json/). The `About` for both RsyncOSX and RsyncUI shows in bottom of view, where the data is saved. Default catalog for storing files for both apps is:

```bash
$HOME/.rsyncosx/macserialnumber/
```
## Prerelease v0.60(build 20) - breaking changes

There is 21 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version of RsyncUI and RsyncSchedule, the menu app for executing scheduled tasks. There are two **breaking changes** in this release:

The following are changes compared to previous release:

- there was an bug in creating configurations if never used RsyncUI and RsyncOSX before
- the menu app RsyncSchedule is released
  - the menu app can be activated from the `File` menu or by `⌘S` shortcut
- and some minor tweaks and updates in the UI
- execution of **shellout tasks**, configurations with pre and post shell scripts

## Prerelease v0.55(build 19)

There is 14 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- **restore** data is in the prerelease
- this prerelase is also a test of informing about updates
- and as always some minor updates

The pace of new prereleases will slow down, it will probably be a copule of new pre releases and after that a few version 1.0.0 release candidates (in May 2021) before release of version 1.0.0.

## Prerelease v0.49(build 18)

There is 12 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- some improvmentes in speed view synchronized filelist within the restore part
  - still the actual restore is not yet implemented
- some other minor improvmentes as well
- RsyncUI now **inform** when there is a new update for download

## Prerelease v0.48(build 17)

There is 9 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- there is fixed an issue with speed in administrating logs, previous versions *spinning beach ball* where many log records

## Prerelease v0.47(build 16)

There is 8 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- commenced developing the restore view
- updated the progress indicators, size and how they are presented
- and some ohter minor updates as well

It seems to be a release version 1.0.0 of RsyncUI sometime in May 2021.

## Prerelease v0.45(build 15)

There is 5 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- some cleanup and tweaks in the UI
- the docs about the [development](/post/development/) of RsyncUI is updated, and more updates will come
- the base language is English, German and Norwegian localization is up to date, Italian is still work to do


## Prerelease v0.42(build 14)

There is 2 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- added Quick task, add a source and a destination and go for it

## Prerelease v0.41(build 12)

There is 31 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- shortcuts for estimating and executing in both multiple and single task (see the File menu)
- German and Norwegian localization is updated
- there is still work to do abouth the Italian localization
- and some other parts are also enhanced

## Prerelease v0.39(build 11)

There is 25 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- adding parameters to rsync
- som UI updates

The plan for release of version 1.0 is sometime in June or July 2021.

## Prerelease v0.36(build 10)

There is 18 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- a kind of "race" situation related to Alert and the word error in output is fixed
- logs view, either all or by config, search and delete in logs
- and a few other enhancments as well, commenced using Combine

## Prerelease v0.36(build 8)

There is 15 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- the issues with usersettings should be solved
- a few other enhancments
- focus the next few weeks are QA of what is implemented and planning what to be developed next
- I am also using time to learn more about SwiftUI, focus now is Combine and how can I use Combine in RsyncUI

## Prerelease v0.35(build 7)

There is still some minor issues with settings - a new prerelease will be uploaded in next week (16 - 20 March). Use RsyncOSX if you will change some settings.

There is 14 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- the user settings is updated, there were a few bugs in previous version
- the documentation for [user settings is also updated](/post/userconfiguration/)
- with this release there is about three months since I commenced the preparation and work on RsyncUI
- RsyncUI will probably be released in version 1.0 in about two or three months, either late in May or beginning of June 2021
- as the development progresses new testreleases will be available

## Prerelease v0.3(build 6)  

There is 12 March 2021 [released a test version](https://github.com/rsyncOSX/RsyncUI/releases). The testversion can be used in parallel with RsyncOSX.
