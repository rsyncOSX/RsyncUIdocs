+++
author = "Thomas Evensen"
title = "Changelog"
date = "2024-07-27"
tags = ["changelog"]
categories = ["general information"]
lastmod = "2024-07-27"
+++
RsyncUI is [signed and notarized](/post/notarized/) and built as [Universal macOS Binary](https://developer.apple.com/documentation/xcode/building_a_universal_macos_binary).  If you miss some functions please drop me an email: thomeven@gmail.com or create an Issue on GitHub. All suggestions about enhancements are welcome.

## Version 2.1.x (work in progress)

Date: 9 August 2024

#### Xcode 16, Swift Testing and Swift Package Manager

For RsyncUI only. To be released as part of RsyncUI later in 2024, the work on RsyncUI (version 2.1.x) commenced in August 2024.

By Using Swift Package Manager (SPM), parts of the source code in RsyncUI is extraced and created as packages. One such package is [RsyncArguments](https://github.com/rsyncOSX/RsyncArguments), which create parameters to `rsync` from configurations. The old code, the base for packages, is deleted and RsyncUI imports the new packages. 

In Xcode 16 there is also a new module, Swift Testing, for testing packages. By creating packages and Swift Testing, important code is isolated and tested to verify it is working as expected. By SPM and Swift Testing, the code for RsyncUI is modularized, isolated, and tested before committing changes.

This is *work in progress*. I am learning every day and developing new code.

### Possible issue in function for restore

The issue only affects what I assume are advanced users, who synchronize data to remote servers by [passwordless logins](/post/ssh/).

There is an issue for some users in function *Restore*. I discovered the issue when working on the package [RsyncArguments](https://github.com/rsyncOSX/RsyncArguments). The issue is when *collecting* list of filenames from a remote server for select and restore. The issue does not affect the actual restore, only the list of filenames to select before a restore. 

If using only user selected ssh-key, not the default values for ssh-key, the user selected ssh-key and identityfile is *not* included in rsync command for listing files.

An example of the rsync command which causes the issue is: `rsync -e ssh -r --list-only thomas@raspberrypi:/backups/Documents/`. 

If not the default values for ssh-key is enabled, `rsync` will not grant access to remote server by the above command. When default values for ssh-key and ssh-port number are used, it is not requiered to include it in command. SSH will automatically pick up default values if exist.

The correct rsync command for listing of filenames on a remote server when only user defined ssh-key and identityfile are enabled is: `rsync --verbose --compress -e ssh -i ~/.ssh_rsyncosx/rsyncosx -p 22 -r --list-only thomas@raspberrypi:/backups/Documents/`. 

The user defined ssh-key and identityfile are included in the above command. 

Workaround: create and enable default ssh-key and identifyfile. This is fixed in version 2.1.x (not in version 2.0.0)

In the next version of RsyncUI, restore data from within RsyncUI is **only** valid for remote serves. The macOS Finder is a much better tool for restoring files from a local attached backup discs.

## Version 2.0.0 (build 101) -  27 July 2024

This is a release candidate. There will be a version 2.0.1 when macOS Sequoia is public sometime after the summer.

The work on adapting RsyncUI to the new concurrency model of Swift 6 is complete. There was one external source file, [John Sundell's Files](https://github.com/JohnSundell/Files). It caused some issues with adapting to the concurrency model. The source file is now deleted. The folder and file operations now use FileManager from Apple's Foundation.

RsyncUI is not a multi-threaded application. There is only one real asynchronous task in RsyncUI. The macOS system executes the task using the `rsync` command-line tool, not RsyncUI. RsyncUI only listens for termination and real-time output from `rsync`. During the async execution, RsyncUI updates a progress bar. All UI updates are on the main app thread. Most classes and structs are now annotated for execution on the main thread. This is to prevent data races and application crashes. A data race is when one thread accesses memory while the same memory is being mutated by another thread.

Summary changes:

- RsyncUI is now fully adapted to Swifts new concurrency model and Swift version 6
	- in Xcode `SWIFT_STRICT_CONCURRENCY = complete` and `SWIFT_VERSION = 6;` is set 
	- about [120+](https://github.com/rsyncOSX/RsyncUI/compare/v1.9.2...v2.0.0) files are changed and cleaned up
- by using the tool [periphery](https://github.com/peripheryapp/periphery), the code is cleaned and all not used classes, structs, functions and attributes are deleted
- there has been refactor of internal code and a few GUI cleanups
- thx to [Cavaliere100](https://github.com/Cavaliere100) for testing RsyncUI on MacOS Sequoia and experienced an application crash for new users
	- the issue is solved in the 2.0.0 rc
- RsyncUI is tested on MacOS Sequoia, built by Xcode16 beta4 and it is verified working as expected
- there is a new export and import function, tasks can now be exported and imported between profiles and to new Macs
	- import and export is by file
	- some more info [about export and import](/post/ver200rc/)

## Version 1.9.2 (build 100) - 11 June 2024

This is most likely the last release before macOS 15, macOS Sequoia is released sometime after the summer. Bugs will be fixed, though, if found. The work with Swift 6 and Xcode 16 beta commenced today. The major work in next release 2.0.0 (build 101) is compliance with the new concurrency model of Swift 6. And there are some new things there for me to learn and understand.

- view of the log file is back
- the logging of synchronization task is simplified
  - by default `on`, a summary only of each synchronization is added to the log records, view `Log Listings` from Sidebar (not changed)
  - by default `off`, there is also possible to add a short summary to the log file
    - timestamp
    - last twenty lines of output from rsync which includes a summary of the task
- the Settingsview is updated

## Version 1.9.1 (build 99) - 27 May 2024

This is a maintenance release of RsyncUI. There are some minor, non critical fixes and minor UI updates.

- adjusted width of RsyncUI to `.frame(minWidth: 1100, idealWidth: 1300, minHeight: 510)`
	- width might be reduced to 1100 points (`CGFloat`), default 1300 points as now
- if `Monitor Network` is on in settings, there is a check for connectivity to remote server every time a task is executed
	- if no connection during timeout an error messages is thrown
- in Add tasks, selected tasks might be tested as in parameters for rsync
	- only a `—dry-run` to verify what the task does
- in Add tasks, update tasks
	- fix a minor glitch refresh view when update tasks
- the Profiles view is moved to sidebar from the Add tasks
- a minor GUI update in view for details, each task, after an estimation run

## Version 1.9.0 (build 98) - 12 April 2024

This is a maintenance release of RsyncUI. There are some minor, non critical fixes and minor UI updates.

- changing colour of icon toolbar reset estimates in the main Tasks view, the colour is white if no estimates, red if there are estimates
	- this also applies to reset selections in Logs view
- the progress bar in the main Tasks view is only presented during synchronization, hidden else
- moved selection of profile from the Toolbar to the Sidebar, makes the Toolbar cleaner
- rsync version is displayed in bottom of the Sidebar
- fixed missing refresh of view when deleting log records
	- workaround, if not refreshed now, change view and return will refresh view
- updated the view for `ssh-copy-id` of public ssh-keys, in Settings (shortcut `⌘,`), Ssh menu and Show copy keys
- and some minor refactor of internal code

## Version 1.8.9 (build 97) - 26 March 2024

Changes in this release:

- fixed bug in ProgressView, if more than one task, max value (bound) for each progress is set correct
- demo profile is removed, some issues when refactor of object executing external task `rsync` in v1.8.8
	- fixing the issue would be to much spaghetti code in demodata for snapshots
- and some minor updates and cleaning of code as usual

May you all have a happy Easter and safe computing. Doing frequent backups keeps you most likely safer  :-)


## Version 1.8.8 (build 96) - 14 March 2024

Update 18 March: there is one minor issue in progressbar. When executing more than one task, the bounds of progressbar is not reset properly. This causes the progress not to work as expected. A fix will be released. *Issue is fixed in code.*

Changes in this release:

- there is some cleanup in the code and *one possible breaking change*, support for pre- and post tasks is removed
	- I believe only a few, if any, use pre- and posttasks, and the cleanup in code causes some issues to pre and post task
- in Add tasks, select the Home button (Home catalogs); if an external drive is attached selecting a catalog and mounted volume add (suggest) values for local catalog, remote catalog and Synchronize ID
- this version is compiled with Xcode version 15.3, released 5 March 2024, Swift 5.10 and it fixes one minor bug in RsyncUI, after execution of tasks RsyncUI returns to the root view as expected
	- the main new feature with Swift 5.10 is full dataisolation in the concurrency model
	- in this release several of previous refactored functions to use Swifts `async` and  `await` keywords for asynchronus execution are converted back to use what is called *completion handlers*, which are triggered post when the rsync task is completed 
	- I would prefer using Swifts `async` and  `await` keywords in what is called *structured concurrency*, but it does not work as expected by using the `Process` object which is responsible for execute all commands to rsync
- due to the above a few `async` functions are refactored back to use *completion handlers*, and some cleanup as part of this
- some changes of icons toolbar
- and this is also a maintenance release, cleanup and minor fixes in code
- deleted one external library, there were to many complains in library due to Swifts check for full dataisolation
	- using default SwiftUI functions, no benefit using external library
- I am now very reluctant to use other external libraries, another which was removed in version 1.8.5 sometimes caused a crash in RsyncUI

I am using RsyncUI myself several times a day, both on a local FreeBSD server and on two external local SSD disks. Every time I am making changes to code, documents, or photos, I am using RsyncUI to synchronize my backups. And to my own experience, RsyncUI is very stable, and rsync is, in my opinion, a fantastic and reliable tool for synchronize data. Some numbers about my own use of RsyncUI, using the logs and filter by year, and only to my FreeBSD server: in 2022, 451 synchronizations, in 2023: 1031 synchronizations, in 2024 until today: 247 synchronizations.

## Version 1.8.7 (build 95) - 20 February 2024

By doing the SwiftData version of RsyncUI, I got idea and motivation for several internal changes in version 1.8.7 (build 95). Regarding SwiftData and RsyncUI, it works but there seems not to be any real advantages compared to the JSON file version. Anyway, by doing the SwiftData project, I have done quite a few internal enhancements in this version. 

- several internal enhancements, see GitHub [to compare versions](https://github.com/rsyncOSX/RsyncUI/compare/v1.8.6...v1.8.7)
-  the Quick Task is moved to a toolbar button in the main tasks view
- there are some updates in demo data is updated as well, demo data now also includes some snapshot data to show how tagging works.
	- by tagging snapshots means tagging for delete old snapshots
	- DemoData profile might be deleted using the Tasks menu, choose Profiles from the toolbar
	- DemoData is downloaded from [GitHub](https://github.com/rsyncOSX/RsyncUI/tree/main/samplejsondata)
- and some localization updates, German and Norwegian

## Version 1.8.6 (build 94) - 30 January 2024

**Important**: the release  fixes the issues in version 1.8.5. Due to refactory of log records it is important you have installed and used version 1.8.5 before installing this release . Version 1.8.6 does **not** include check and copy of old file log records as version 1.8.5 does.

## Version 1.8.5 (build 93) - 23 January 2024

**One minor issue**: there is a minor non critical issue when adding new tasks, the logrecord after a run is not loaded when viewing logs. *Workaround is add task and restart RsyncUI.* The bug is fixed and a new release will come in a week or two. **The issue is only when new tasks are added.**

**And a second hickup as well**: To save changes in user settings, do not close the settings view right away, if changes in rsync settings, ssh settings or environment choose the **Info view** before closing the settings view. The issue is fixed in code.  And included in the updated release in a week or two.

Changes, summarized:
- internal naming of logrecords and physical file for saving are changed
	- this is a somewhat big internal change
	- data from old file logrecords are automatically saved by new filename, including for profiles if profiles is used
	- a kind of *breaking* change; you have to choose either to use RsyncUI or RsyncOSX, my advice is of course use RsyncUI
- the internal flow of and loading of data is also changed, the internal datastructure is now an `@Observable` class and data is now made avaliable to other views by a `@Bindable` property
	- when data is changed the internal data is updated by the `@Bindable` property, views are automatically refreshed and changes are also saved to permanen storage at the same time
- user settings now discover if parameters and data is changed and autosaves if changed, no need for explicit save changes
- there is now a possibility to load demo data, loading demodata creates a *DemoData* profile and copy demodata from the RsyncUI GitHub repository
	- load demo data from the Tasks menu or by shortcut `⌘L`
- Confetti in FirsTime view is removed due to a bug in external code for Confetti

Some details:

The internal naming of logrecords in the model in RsyncUI, including the physical file for saving logrecords, is changed to support understanding of what it is. Much of the model part was imported from RsyncOSX, and due to the history of RsyncOSX, the naming in RsyncUI was inconvenient. RsyncUI takes care of automatically copying and creating new files for log records. The change is a kind of *breaking* change; you have to choose either to use RsyncUI or RsyncOSX. Not both. My advice is, of course, to use RsyncUI.

There is a bug in the Confetti view and the FirstTime view for new users of RsyncUI. The bug is not resolved, and the Confetti is removed from RsyncUI. Confetti was an external package imported into RsyncUI.

## Version 1.8.2 (build 92) - 8 January 2024

This is maintenance release including a few minor enhancements:

- cleanup and remove duplicates in code
- fixed some toolbar actions and updated some of the icons on the toolbar
- new filtersearch in snapshots
- converted the last `ObservableObject` with the new `Observation` macro
	- property wrapper to create binding to mutable properties in SwiftUI
- the new `ContentUnavailableView` is used to inform when there are no match for filter search
	- there are filter search in tasks, logrecords and snapshots
- and fixed a couple of minor bugs as well

If you hoover the mouse over a toolbar icon, it will display a short message about which function is behind the icon. Just give it a second to display the message.

## Version 1.8.1 (build 91) - 29 December 2023

There are a few more minor GUI enhancements and tweaks. And cleaning of code, remove unused code and updates where needed.

- the adding tasks includes a list of all catalogs from your `$Home` catalog, if there is attached a drive the volume name is automatically copied to destination
- a new confirm dialog if number of files to synchronize is like a new task
	- sometimes a remote server or local disk is unavailable, if you commence a synchronize task unaware of destination resource is not available, rsync might believe this is a new full synchronize and a dialog confirms synchronize or abort
	- the feature to be switch on off in usersettings
	- if a remote server is unavailable rsync will *most likely* complain and throw an error, if `check for error in output` in user settings is enabled, the rsync error messages written to log and an Alert informing about it will occur
	- if a local disk is not attached rsync will try to synchronize data to `/Volumes/` catalog on your mac, this catalog is normally where macOS mounts local attached disks
```bash
/dev/disk5s2 on /Volumes/Import bilder (apfs, local, nodev, nosuid, journaled, noowners)
/dev/disk6s1 on /Volumes/Backups (apfs, local, nodev, nosuid, journaled, noowners)
```
## Version 1.8.0 (build 90) - 18 December 2023

Important: **all** functions within every view are now icons on the toolbar, upper right. Major functions are colored blue.

The following changes in release are:

- fixed some issues regarding adding ssh keypath, file and ssh port number
	- there is a check on the format which kicks in right away, the check is now debounced a few seconds to allow entering data
- even more cleanup in code after removing support for previous versions of macOS
	- there is always some code in a large codebase which should be revised and cleaned up
- and even more views are converted to `NavigationStack` and most functions moved to the toolbar
	- this makes the views cleaner and more space for important info
	- **all** sheet and pop-up views are removed, only Alert as pop-up if some odd situation occurs like missing either source or destination when adding tasks
	- within every view the main icon (function) is colored blue and a short help text is displayed when hoover mouse over icon

Update of user documentation is commenced, it might take some more time because most screen dumps are changed and text need updates.

## Version 1.7.9 (build 89) - 7 December 2023

Updated 8 December 2023, the timer and automatic execution of tasks are disabled and this version is uploaded to Homebrew as well.

From this release, RsyncUI is **only supported on macOS Sonoma**, the latest release of macOS. This also includes the RsyncUI version on Homebrew. With every new release of SwiftUI and macOS, there are several new features that are also beneficial for RsyncUI. The result is that the macOS Sonoma version of RsyncUI includes enhancements not found in the other version. And it is difficult to maintain two releases of RsyncUI; there are too many `#avaliable` statements in the code, which makes the code more vulnerable to bugs.

New features:

- RsyncUI is now supported on macOS Sonoma only
- RsyncUI now starts as a single window app, closing the window also closes the app
- the toolbar functions are now adjusted for which navigation is enabled, either sheet views or `NavigationStack`
- after abanding support for previous versions of macOS there are several cleanups in code
- navigation by `NavigationStack` is default on, switch off in usersettings for sheet views and pop-ups
- automatic execute tasks after estimate and the timer function are disabled
	- any automatic function introduces some risks for failure, better *safe than sorry*

**A minor issue**: *sometimes* when RsyncUI estimates tasks and there is data to synchronize, choosing to synchronize data after estimate only returns to the previous view without synchronizing. You will discover when this happens, just do another estimate and synchronize data after estimating. Sometimes there is a mismatch by the UUID (uniq identifier) selected for synchronizing data and UUID on task. I dont know why this sometimes happens, it might be a bug.  The guard statement just bails out if it happens, just do another estimate and synchronize.

###  Last version  supporting previous versions of macOS - 1.7.5 build (88)

The relase 23 November 2023 were the last releases of RsyncUI supporting macOS Montery and macOS Ventura, macOS 12 and 13. Next release will be for macOS Sonoma only. This also applies for the Homebrew version as well.

## Version 1.7.8 build (88)  and 1.7.5 build (88) - 23 November 2023

Both versions will run on macOS Sonoma, but one is built for macOS Sonoma only. And by the release of version *1.7.8 b(88)* and *1.7.5 b(88)* the macOS includes a few more enhancements than the other version. There are two versions because of the new `@Observable` macro introduced in Swift 5.9, Xcode 15 and macOS Sonoma.

Enable  `NavigationStack` by switch on in user settings, save and restart RsyncUI. Disable it by switch off, save and restart.

- *Version 1.7.5 b(88)* supports all macOS versions from macOS Monterey and is available from Homebrew as well
- *Version 1.7.8 b(88)* for **macOS Sonoma** only

There are some GUI changes in both apps.  And a couple of minor fixes. There are several methods for navigation within SwiftUI, and one method is utilizing `NavigationStack`. Enable `NavigationStack` is by settings and it is default off. All sheets, like pop up views, are for *the macOS Sonoma only* version converted to new Navigation if enabled. For *the Homebrew* version only for macOS 14 users and only the Tasks view including estimating details.

See more info about it [here](/post/navstack/).

## Version 1.7.7 build (87)  and 1.7.4 build (87) - 31 October 2023

*Version 1.7.4 build(87)* supports all macOS versions from macOS Monterey and is available from Homebrew as well.

*Version 1.7.7 build(87)* for **macOS Sonoma** only and only by direct [download](https://github.com/rsyncOSX/RsyncUI/releases/download/v1.7.7/RsyncUI.1.7.7.dmg) from GitHub. This version is for macOS Sonoma only because of migrating objects and bindings to the new `@Observable` macro introduced in Swift 5.9, Xcode 15 and macOS Sonoma.

There is, by the search field, in some of the views possible to filter the output. Within the logs and restore view filter by any string. In the previous releases, the filter might be observed as a kind of not working properly if there are many rows of data. This is due to the list of data is refreshed on every keypress in search field. And by every refresh, the list of data is computed. In the this version there is a one *second debounce* or delay in refresh. By the delay, typing in the search field is smoother.  The 1 second delay in *filter search* is notified by a rotating progressview.

And there are some other minor updates as well.

## Version 1.7.3 build (86) - 19 October 2023

Changes as for the macOS Sonoma build, but built for macOS Monterey to macOS Sonoma. Major difference for this version compared to the macOS Sonoma only, is the bindings introduced in Swift 5.9, the `@Observable` macro.

*Version 1.7.3 build(86)* supports all macOS versions from macOS Monterey and is available from Homebrew as well.

## Version 1.7.6 build (86) - 19 October 2023

For **macOS Sonoma** only and only by direct [download](https://github.com/rsyncOSX/RsyncUI/releases/download/v1.7.6/RsyncUI.1.7.6.dmg) from GitHub. This is a maintenance release.

There are some minor fixes and the major work is replacing the ShellOut package with an updated and maintained package. The ShellOut in the released version of RsyncUI is not working. The ShellOut let the user execute shellscript ahead and after execution of a synchronization task. A shell script might be like moving files, mounting a filesystem from a remote server and so on. The ShellOut must be used with care and most likely only the advanced macOS users with experience in writing shellscripts might find this feature usefull.

## Version 1.7.5 build (84) - 28 September 2023

For **macOS Sonoma** only and only by direct [download](https://github.com/rsyncOSX/RsyncUI/releases/download/v1.7.5(b84)/RsyncUI.1.7.5.dmg) from GitHub.

The major work in this release is migrating objects and bindings to the new `@Observable` macro introduced in Swift 5.9, Xcode 15 and macOS Sonoma. Migrating code to the new macro is a *breaking change* and that is why there are two builds.  This version only supports macOS Sonoma.

*Version 1.7.2* supports all macOS versions from macOS Monterey and is available from Homebrew as well.

## Version 1.7.2 build (85) - 23 September 2023

This is a maintenance release. Build by Xcode 15 for macOS Monterey to macOS Sonoma. There are no bugfixes (none reported), some enhancements only and a few cleanups in code.

- there is a change in restore for snapshot task, either select to restore from a previous snapshot or default the latest
- on macOS Sonoma, to delete a task, log or snapshot select and use the ⌫ (backspace)
	- the delete from the Edit menu does not work on *macOS Sonoma*
	- the delete works as expected on macOS Ventura and Monterey

## Version 1.7.1 build(83) - 1 September 2023

The following are enhancements of RsyncUI, minor updates which makes the app easier to use.  Some of the changes are utilizing SwiftUI modifiers for table operations like *copy*, *paste* and *delete*. By utilizing modifiers for table, default menu functions are automatically enabled for all three table operations.

 For macOS 12 and later:

 - profile is moved to the toolbar, it makes the navigation stack more clean
 - delete tasks from main- and add view is updated to use function from Edit menu (deleted from Tasks menu)
 - delete logrecords from within Log listings view from Edit menu
 - fixed error message about missing files for new users, if missing file default files are created
 - added automatic execution when all tasks are estimated
 	- user set seconds before execution and function can be disabled, *disabled* by default
 	- select the button counting down to *temporary* disable

For macOS 13 and later:

- from the Edit menu the shortcuts `⌘C` and  `⌘V` will copy and paste copies of the selected tasks.

The copy and paste will append task(s) to make it more easy to create new task based upon existing data. Data as source, destination, server, username and parameters to rsync are copied from the selected task(s).

## Version 1.7.0 build(82) - 16 August 2023

There is tooltip for each function on the toolbar. MacOS Monterey does not support double click on row, see [how to execute](/post/macos12/)  a `--dry-run` on macOS Monterey. The RsyncUI documentation is updated and more updates will be done after this release.

- there is a cleanup in main taskview, if a task is executed after any estimation a progressbar will be presented
- some adjustments in logs- and restore view
- some of the functions are moved the toolbar
- color of the buttons are adjusted

## Version 1.6.6 build(81) - 1 August 2023

This is a maintenance release. Minor cleanups, bug fixes and enhancements in parts of the code.

- task are marked when estimated
- new button for display rsync output on estimated task
	-	remeber first double click estimate a task, next double click will execute the estimated task
- huge output (more than 20000 lines) from rsync is truncated and notified
	- summary of rsync output is appended to truncated output
- enable and disable checking for error in output from rsync
	- errors in output from rsync is notified
- and some cleanup and minor fixes.

## Version 1.6.5 build(80) - 16 July 2023

This is a maintenance release.  No enhancments but a few cleanups and bugfixes. RsyncUI will become the primary application this year (compared to RsyncOSX). RsyncOSX will still be maintained, but bugfixes only. According to Apple, SwiftUI is the future and RsyncUI is developed by utilizing SwiftUI. And on macOS 13 RsyncUI is already more feature rich than RsyncOSX.

## macOS Sonoma and RsyncUI

I have commenced porting RsyncUI to macOS Sonoma and Swift 5.9. By Swift 5.9 the new `Observable` macro replace the  `@StateObject` propertywrapper. This is a *breaking* change and there will be two releases for RsyncUI when macOS Sonoma is public. Combine is still used in parts of the macOS Sonoma version of RsyncUI. The port of RsyncUI to macOS Sonoma is almost completed.

## Version 1.6.3 build(79) -  29 June 2023

The release includes some important fixes for *administration* of snapshots. There are also some enhancements for macOS 13 and later:

- for **macOS 13 and later** a double click on row executes a `--dry-run`
	- the next doubleclick will **execute** the task, RsyncUI verify if previous doubleclick was a `--dry-run`, if not a new `--dry-run` is executed
	- only **avaliable for macOS 13** and later due to SwiftUI requirements, the DryRun button is removed if macOS 13 and later
- after a  `--dry-run` it is now possible to execute task direct or by a new doubleclick
- when executing a `--dry-run` and initate execute after shows a view of progess
	- version 1.6.1 will only execute the task and show a rotating progress until the task is completed
- some of the rotating progress and position on screen is slightly changed
- fixes of critical issues in administration of snapshots

## Version 1.6.1 build(77) -  20 June 2023

*Non critical issues* in version 1.6.0 are fixed.

## Version 1.6.0 build(76) -  16 June 2023

Update **19 June 2023**: there are a couple of *non critical issues* which cause some functions like `--dry-run` within the main view not working **after** a synchronize all execution of tasks. Fixes are done in code and an update will be released in a  day or two.

There are several minor GUI changes like all `list` and `foreach` listing are replaced with `table`.  There are also a new log of major synchronize actions. Select  the shortcut `⌘O` for view logfile and select actions. The restore part is changed a little bit.

And as always there are some cleanup in code.

## Version 1.5.0 build(73) - 4 May 2023

There is a change within the internals for navigation. RsyncUI supports macOS from version 12.0. From macOS 13.0 Apple has deprecated the [NavigationView](https://developer.apple.com/documentation/swiftui/navigationview) and released [NavigationSplitView](https://developer.apple.com/documentation/swiftui/navigationsplitview). Within this release there is now a check if macOS 13 and [code](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Sidebar/SidebarVentura.swift) for navigation is refactored. The deprecated [code](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Views/Sidebar/Sidebar.swift) for navigation still works for macOS 12, but new code is simpler when there is complex navigation.

This version also includes a very simpel timer function to postspone synchronization of data **while you are working**.  The timer is **not** like a schedule function.  The timer is working if RsyncUI is minimized and your Mac is not going to sleep. The visual count down of minutes might not be correct if RsyncUI is minimized, but the internal count down is correct. This is due to the *timer library*  require the app to be active.

RsyncUI writes a record to the log every time it executes a profile by the timer. The timer has to be reactivated after each time.

There are also a few minor cleanups as well.

## Version 1.4.8 build(70) - 24 March 2023

There are cleanup and refactor of the main tasks view, internal code only. There are also two GUI updates:

- after an estimate it is now possible to execute task direct
- there is a list of all tasks for all profiles sorted by last run date from the main tasks view

## Version 1.4.7 build(69)  -  14 March 2023

Update 17 March 2023:

- RsyncUI is now avaliable to install by Homebrew: `brew install --cask rsyncui`

The following are new:

- the restore part for `snapshot` tasks is modified, restore is from last snapshot only, **no** changes for normal `synchronize` tasks
- the actual restore command is presented in Restore view (might be copied and pasted within a terminal)
- there is a update of GUI for `DryRun` in main Tasks view

No bugfixes, only a few minor enhancements

## Version 1.4.5 build(67) -  7 March 2023

The following are new:

- the estimated view, changed to a table view
- the position navigation items within the navigation bar  is now fixed, e.g. does not change vertical position when a new sidebar action is selected
- create and delete profile is a by a button (from Add task view)
- the restore part is refactored, mostly internal code

## Version 1.4.3 build (65) - 8 February 2023

This is a maintenance release.

- fixed one non critical bug
- some cleanup in code and a few minor GUI updates
- this is a maintenance release

## Version 1.4.2 build (64) - 6 January 2023

Compiled on Apple Silicon (M1 Pro) by Xcode 14.2 as a Universal macOS Binary on macOS Ventura

There are some minor updates and some internal cleanups in this release, nothing big at all. There is added an simple assist function in add task. The parameters to rsync view is enhanced, if the `verify` switch is on the Verify button executes a verify command.  And likewise for `synchronize` and `restore` switch. All verify commands are `--dry-run` commands.

**Caution**: regarding the Verify button and the `verify` switch is on. If there are many files a verify will take some time due to rsync computes the checksum and compares each files by checksum.

{{< figure src="/images/rsyncparameters/verify.png" alt="" position="center" style="border-radius: 8px;" >}}

## Version 1.4.0 build (62) - 6 December 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.1 as a Universal macOS Binary

Some enhancements and a bugfix in this release.

Parameters to rsync:

- any changes to parameters are presented "on the fly", add or delete a parameter and the updated rsync command is presented
- the changed rsync command might be verified (by a `--dry-run`) ahead of saving

Estimate and details:

- in main view select `Estimate` button without selecting a task
    - after closing the summarized estimated view, select a task and the details (`--dry-run`) is presented
    - select another task and the details is presented
    - the `Reset` will reset all estimates, likewise if tasks er executed after estimate will reset all estimates.

And there is a bugfix in [Quick Synchronize](https://rsyncui.netlify.app/post/quicktask/).

## Version 1.3.9 build (57) - 18 November 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.1 as a Universal macOS Binary

There are a few changes and fixes to the snapshots and the parameters to rsync parts of RsyncUI. Changes are:

- snaphots: fixed a few bugs, the first and last snapshot are not possible to delete even if they are marked for delete, during delete process they are removed from list of delete if tagged
- snapshots: tagging and select for delete are moved to shortcut actions and menu actions
- parameters to rsync: if default parameters are marked for delete the actual parameterlist presented is updated, changes has to be saved to take effect

## Version 1.3.8 build (56) release candidate - 10 November 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.1 as a Universal macOS Binary

There are a few changes and fixes to the snapshot part of RsyncUI. The changes are as applied to the snapshot part of RsyncOSX. This is a release candidate and will be released as an new version in a couple of weeks.

## Version 1.3.7 build (56) - 5 November 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.0 as a Universal macOS Binary

There is fixed a minor bug when selecting a task and hitting the shortcut `⌘R` for excute task now. The task is executed but the spinning progresswheel did not disappear when task was completed. It is now fixed.

## Version 1.3.6 build (55) - 31 October 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.0 as a Universal macOS Binary

The major work in this release is rewriting some of the code to utilize Swifts async and await for asynchronous execution of code. The new code utilizing async and await is much simpler to read and write. The need for callback functions are reduced and it makes code lesser.  Lesser code is better code. Asynchronous execution is a key part of RsyncUI. The completion of a task is not known ahead of execution and whenever a task is completed next action is executed. Next action is e.g. execute next synchronization task, present output from rsync or present a list of files.

The main view is also changed a little bit, see [the changed main view](/post/tasks/).

## Version 1.3.0 build (53) - 30 September 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.0 as a Universal macOS Binary.

- removed "Select and slide to left for delete" a task, to delete a task select it and delete either by shortcut `⌘D`(in Synchronize view) or by menu
- new shortcut `⌘I`(in Synchronize view) for getting status about local and remote data


## Version 1.2.9 build (52) - 8 September 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 14.0 as a Universal macOS Binary.

This release is built on macOS  Ventura. There are some minor GUI enhancements.

## Version 1.2.8 build (51) - 20 March 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 13.3 as a Universal macOS Binary.

- the Execute buttons within main view is one button now, in user config enable always estimate first
  - if not set RsyncUI will execute tasks with no estimation
  - shortcuts for estimation and execution works as expected

## Version 1.2.7 build (50) - 17 March 2022

Compiled on Apple Silicon (M1 Pro) by Xcode 13.3 as a Universal macOS Binary.

This is a primarily a maintenance release.

- there are a few changes within log records
  - search and filter
  - removed a button
- within the restore view there is a new search facility
- the userconfig is now saved as JSON file, automatically transferred from the previous PLIST config file
  - userconfig are values like which version of rsync is utilized, restore path and so on

## Version 1.2.6 build (48) - 31 December 2021

Compiled on Apple Silicon (M1 Pro) by Xcode 13.2.1 as a Universal macOS Binary.

RsyncUI is slowly, but steady becoming better and more user friendly. RsyncUI is stabel, most of the core functions are based on code from RsyncOSX. There are no plans for major changes, but more like minor enhancements when I discover parts which should be improved.

- delete a task by shortcut `⌘D` (in Synchronize view)
- updated a few labels
- some minor updates as well

## Version 1.2.5 build (48) - 6 December 2021

The following are [changes](/post/newversion/) within this version:

- multiple tasks and single task view is merged into one view
- the new task view includes some reorganization of functions
  - estimate and execute all tasks or selected tasks
  - execute all tasks (no estimation) or selected tasks
  - estimate one task, execute task after estimation or cancel, view detailed output from rsync
- a few buttons are removed, functions in buttons are moved to shortcuts
- there is a new first time start view

## Version 1.2.3 build (46) - 11 November 2021

Compiled on Apple Silicon (M1 Pro) by Xcode 13.1 as a Universal macOS Binary.

Localization for German and Norwegian added. Added GUI panels for selecting catalogs to synchronize.

## Version 1.2.2 build (45) - 28 October 2021

The issues **below** is solved in this version.

I have just got my new Apple Silicon based MacBook Pro 14" with the new M1 Pro processor. The path for the installation of Homebrew on Apple Silicon Mac´s is changed. And there is an issue in changing path for rsync in RsyncUI. Homebrew on Apple Silicon based Mac´s installed in `/opt/homebrew/bin/`.

RsyncUI should also detect if on a Apple Silicon or Intel based Mac.

And  there is also an annoying error messages if a not valid path for `rsync` and restore is set.

## Version 1.2.1 build (42) - 21 October 2021

Build by Xcode 13.1 RC

The major work is internal. There might be several hundred or thousands of logrecords. Reading and loading logrecords into memory is moved to when they are needed. And not when the app is started or a new profile is selected. The change will improve memory footprint and speed up the application.

The default profile is automatically selected at start of application.

Localization to German, Italian and Norwegian is **not** yet added. There was some issues in localization and it is removed for the moment. Most of strings are already translated into German and Norwegian.

## Version 1.2.0 build (41) - 28 September 2021

The issue in Update configurations is fixed. There was also a issue with labels (prompts) in textfields which is fixed.

## Version 1.1.2 build (40) - 9 September 2021

This build includes some minor UI tweaks in toggle buttons (see [settings](/post/normalsettings/)). The docs are updated with screenshots. This is most likely the last update before macOS Monterey is relesed. A new build, version 1.2.0build (41) will be released as soon as Apple release macOS Monterey and Xcode 13.

## Version 1.1.2 build (39) - 1 September 2021

The schedule part of app is removed. The majority of users dont use scheduling. This is the experience from RsyncOSX and the download statistics. In about 2000 downloads of RsyncOSX only 80 is the scheduling app.

## Version 1.1.2 build (38) - 28 August 2021

- a few minor UI enhancements
- no bugfixes

And the QA and work on the UI continues.

## Version 1.1.2 build (37) - 21 August 2021

- redesign of rsync parameters UI, [split into parameters and default parameters](/post/rsyncparameters/)
- fixed a couple of bugs in rsync parameters as well

The QA and work on the UI continues, still not happy with some of the views.

## Version 1.1.2 build (36) - 16 August 2021

- finally decided about button style, see screenshots in this doc
- some minor changes

## Version 1.1.2 build (35) - 11 August 2021

- added "select and slide to left" for delete a configuration
- removed the delete button within multiple tasks view
- utilized a few new features included in last Xcode 13 beta 5, released 10 August 2021

Thats it for now.

## Version 1.1.2 build (34) - 30 July 2021

New [build](https://github.com/rsyncOSX/RsyncUI/releases) for public beta of MacOS Monterey, build by **Xcode 13 beta 4**, builds are English only.

The QA and cleanup of UI continues on the road to release on macOS Monterey. RsyncUI is **stable** and there are not any known issues. The following is changed compared to previous builds.

- the buttons and toggle buttons are changed
- the multiple tasks and single tasks view buttons for estimate and execute are "cleaned up"
  - in both views select the execute button executes the task(s) in one go
  - or estimate, view estimate and then execute
- the schedules view is changed as well
  - it is required some more QA on the schedules
- the log views and filter logs are updated, both all logs and by configuration
- and some internal stuff is refactored
- one minor bugfix

## Version 1.1.2 build (28)

There is 29 June 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.1.2 of RsyncUI. There are two builds, one for macOS Big Sur and one for macOS Monterey.

At start of the macOS Big Sur version select, from the drop down, either the "Default profile" or other profile if used. This is **not** required on RsyncUI on macOS Monterey. RsyncUI on macOS Monterey picks the default profile when selecting a task.

- RsyncUI conforms [the App protocol](https://developer.apple.com/documentation/swiftui/app)
- the UI is cleaned up a bit
- several internal changes
- RsyncUI adapts to some changes in macOS settings

The localization of RsyncUI is somewhat refactored. For the moment RsyncUI is localized to German and Norwegian, and there are a few strings missing in the release candidate.

## Version 1.1.1 build (27)

**Update 17 June 2021**. The builds are removed for the moment.

There is 4 June 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.1.1 of RsyncUI. The following is fixed in this release:

- refactored parts of decode and encode JSON, Combine is a super framework
- refactored a few other parts as well
- SwiftUI require some computed properties, like UUID, on data
  - these properties are added during reading data, by mistake these properties was also written to file
  - this is now fixed and the filesize, specially the logs file, is reduced
- existing users of RsyncOSX using defalt format for storing data (PLIST) now can use RsyncUI to [transform default PLIST data](/post/plist/) to JSON which is required in RsyncUI

## Version 1.1.0 build (26)

There is 21 May 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.1.0 of RsyncUI. The following is fixed in this release:

- after a delete of a profile, reload of existing profile names
- a minor update in UI for post and pretask (clearing the input fields)
- more internals using the Combine framework, check about [Combine in development details](/post/developmentdetails/#combine)
- some cleaning up and minor refactor
- a minor bug in executing shell scripts
- updates to [the UI for adding and updating Configuration](https://rsyncui.netlify.app/post/addconfigurations/)
- updates to [the UI for adding shell scripts](https://rsyncui.netlify.app/post/shellout/)

## Version 1.0.1 build (24)

There is 12 May 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.0.1 of RsyncUI and RsyncSchedule.

The following are changes compared to previous releases:

- delete a Profile
- administration of Snapshots
  - the issue with snapshots and remote catalogs is solved
  - save plan and day on a snapshot task
  - delete old snapshots
- a few minor cleanups and enhancements in the UI part

## Version 1.0.0 build (23)

There is 06 May 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) version 1.0.0 of RsyncUI and RsyncSchedule, the menu app for executing scheduled tasks. The **snapshot administration**, like delete old snapshots, is still not yet completed. The work on snapshot administration is going forward and it will be released as an update of RsyncUI. But there are a few issues which has to be resolved before release.

The following are changes compared to previous releases:

- German and Norwegian localizations are updated
- even more use of the Combine framework
- a few internal updates and UI updates

Issue: there is an issue, in Snapshots, selecting a snapshot task and collecting remote data for snapshotcatalogs. The UI will notify if it seems to be such an issue.

About **JSON**: see note on the release 0.99.

## Prerelease version 0.99 build (22)

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

## Prerelease v0.60 build (20) - breaking changes

There is 21 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version of RsyncUI and RsyncSchedule, the menu app for executing scheduled tasks. There are two **breaking changes** in this release:

The following are changes compared to previous release:

- there was an bug in creating configurations if never used RsyncUI and RsyncOSX before
- the menu app RsyncSchedule is released
  - the menu app can be activated from the `File` menu or by `⌘S` shortcut
- and some minor tweaks and updates in the UI
- execution of **shellout tasks**, configurations with pre and post shell scripts

## Prerelease v0.55 build (19)

There is 14 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- **restore** data is in the prerelease
- this prerelase is also a test of informing about updates
- and as always some minor updates

The pace of new prereleases will slow down, it will probably be a copule of new pre releases and after that a few version 1.0.0 release candidates (in May 2021) before release of version 1.0.0.

## Prerelease v0.49 build (18)

There is 12 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- some improvmentes in speed view synchronized filelist within the restore part
  - still the actual restore is not yet implemented
- some other minor improvmentes as well
- RsyncUI now **inform** when there is a new update for download

## Prerelease v0.48 build (17)

There is 9 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- there is fixed an issue with speed in administrating logs, previous versions *spinning beach ball* where many log records

## Prerelease v0.47 build (16)

There is 8 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- commenced developing the restore view
- updated the progress indicators, size and how they are presented
- and some ohter minor updates as well

It seems to be a release version 1.0.0 of RsyncUI sometime in May 2021.

## Prerelease v0.45 build (15)

There is 5 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- some cleanup and tweaks in the UI
- the base language is English, German and Norwegian localization is up to date, Italian is still work to do

## Prerelease v0.42 build (14)

There is 2 April 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- added Quick task, add a source and a destination and go for it

## Prerelease v0.41 build (12)

There is 31 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- shortcuts for estimating and executing in both multiple and single task (see the File menu)
- German and Norwegian localization is updated
- there is still work to do abouth the Italian localization
- and some other parts are also enhanced

## Prerelease v0.39 build (11)

There is 25 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- adding parameters to rsync
- som UI updates

The plan for release of version 1.0 is sometime in June or July 2021.

## Prerelease v0.36 build (10)

There is 18 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- a kind of "race" situation related to Alert and the word error in output is fixed
- logs view, either all or by config, search and delete in logs
- and a few other enhancments as well, commenced using Combine

## Prerelease v0.36 build (8)

There is 15 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- the issues with usersettings should be solved
- a few other enhancments
- focus the next few weeks are QA of what is implemented and planning what to be developed next
- I am also using time to learn more about SwiftUI, focus now is Combine and how can I use Combine in RsyncUI

## Prerelease v0.35 build (7)

There is still some minor issues with settings - a new prerelease will be uploaded in next week (16 - 20 March). Use RsyncOSX if you will change some settings.

There is 14 March 2021 [released](https://github.com/rsyncOSX/RsyncUI/releases) a new version for test. The following is changed compared to previous version:

- the user settings is updated, there were a few bugs in previous version
- the documentation for [user settings is also updated](/post/userconfiguration/)
- with this release there is about three months since I commenced the preparation and work on RsyncUI
- RsyncUI will probably be released in version 1.0 in about two or three months, either late in May or beginning of June 2021
- as the development progresses new testreleases will be available

## Prerelease v0.3 build (6)

There is 12 March 2021 [released a test version](https://github.com/rsyncOSX/RsyncUI/releases). The testversion can be used in parallel with RsyncOSX.
