+++
author = "Thomas Evensen"
title = "The RsyncUI changelog"
date = "2021-03-11"
description = "Changelog"
tags = ["RsyncUI"]
# categories = ["changelog"]
lastmod = "2021-04-21"
+++
The prerelease is a version **for test and preview of what is coming**. It is work in progress and bugs might occur. RsyncUI is [signed and notarized](/post/notarized/).

---

The latest prereleases are close, by functions, to the current release of RsyncOSX. But it is still in development and bugs might occur. There are still a few major functions missing, but the gap is closing. Also check the [todo list](/post/todo/) for an up to date status.

---
## Version 0.99 - release candidate version 1.0.0

The work on RsyncUI commenced in December 2020 and version 1.0.0 is close to release. The rc version 1.0.0 will be released in first week of May 2021, after about four months of work. The four last months also includes learning the basics about SwiftUI and Combine frameworks. And there is still a lot to learn. RsyncUI is reusing a lot of the model classes form RsyncOSX. There has been some minor refactor av the model classes due to utilizing Combine and adaption to RsyncUI.

I believe RsyncUI is ready to be released. There is still work to do, but that will be included in future relases.


## Prerelease v0.60(build 20) - breaking changes

There is 21 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version of RsyncUI and RsyncSchedule, the menu app for executing scheduled tasks. There are two **breaking changes** in this release:

- RsyncUI from this release **only** supports JSON files
- settings in RsyncUI is separated from RsyncOSX settings

You **must** set new user settings in RsyncUI if other than default values, like change version of `rsync`. If you are using RsyncOSX and want to test RsyncUI, [please enable JSON support in RsyncOSX](https://rsyncosx.netlify.app/post/json/) ahead of using RsyncUI.

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

It seems to be a release version 1.0.0 of RsyncUI sometime in May 2021. There are only a few missing parts, see [todo list](/post/todo/).

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
