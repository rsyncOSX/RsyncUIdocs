+++
author = "Thomas Evensen"
date = "2024-07-26"
title =  "Version 2.0.0 release candidate"
tags = ["quick task"]
categories = ["release candidate"]
lastmod = "2024-07-26"
+++
Some info about the version 2.0.0 release candidate.

RsyncUI is now fully adapted to Swifts new concurrency model and Swift version 6. The code was not to hard to adapt to the new concurrency model. Xcode16 beta throws warnings and compiler errors when there are issues about the new concurrency model. And by handling the warnings and errors one by one it is a matter of time before all code is OK. Another task was cleaning up the code. There is a really fantastic tool [periphery](https://github.com/peripheryapp/periphery) to assist finding not used parts of the code. About [120+](https://github.com/rsyncOSX/RsyncUI/compare/v1.9.2...v2.0.0) files are changed as part of adapting code and cleaning up.

In Xcode16 the following build settings are set:

- `SWIFT_STRICT_CONCURRENCY = complete`
- `SWIFT_VERSION = 6;` 

RsyncUI is testet on MacOS Sequoia, built by Xcode16 beta4 and it is verified working as expected

There is a new export and import function, tasks can now be exported and imported between profiles and to new Macs.

{{< figure src="/images/ver200rc/export.png" alt="" position="center" style="border-radius: 8px;" >}}

Export: select catalog and set name for export file. The export file is a JSON data file. Either selected tasks or all tasks might be exported to file.

{{< figure src="/images/ver200rc/startimport.png" alt="" position="center" style="border-radius: 8px;" >}}

Import: as an example a new profile is created for importing tasks. Before import there are no tasks created.

{{< figure src="/images/ver200rc/selectfileimport.png" alt="" position="center" style="border-radius: 8px;" >}}

Import: select the exported JSON file for import.

{{< figure src="/images/ver200rc/importtasks.png" alt="" position="center" style="border-radius: 8px;" >}}

Import: the file for import is selected, data is presented for import. Either select some tasks or all tasks are imported.

{{< figure src="/images/ver200rc/tasksimported.png" alt="" position="center" style="border-radius: 8px;" >}}

Import: all tasks are imported in to the empty new profile. If tasks are imported into an existing profile with tasks, the imported tasks are appended to existing tasks.
