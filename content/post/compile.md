+++
author = "Thomas Evensen"
date = "2020-04-17"
title =  "How to compile RsyncUI"
tags = ["compile"]
categories = ["source code"]
description = "If you pull RsyncUI from GitHub you can easy compile your own version."
+++
RsyncUI is only depended upon Cocoa and  Foundation classes which are standard Swift libraries. There are two ways to compile, either in Xcode or utilize `make` from command line in RsyncUI catalog. To use make require Xcode command line utilities to be installed. Execute the following command and follow the instructions.

`xcode-select --install`

## Remove signing credentials or replace

To compile you have to either remove signing or replace signing credentials. To remove or replace select Target RsyncUI and tab "Signing and Capabilities". The first view is my signing credentials.

![](/images/RsyncUI/master/compile/signing.png)

To remove select "Team: none" and "Signing Certificates: Sign to Run Locally".

![](/images/RsyncUI/master/compile/nonsigning.png)

## Compile scripts

There are two utilities used, [SwiftLint](https://github.com/realm/SwiftLint) and [SwiftFormat](https://github.com/nicklockwood/SwiftFormat). Both can be removed, select tab "Build Phases" and delete the lines. Or you can use [Homebrew](https://brew.sh/index_nb) to install both utilities.

![](/images/RsyncUI/master/compile/scripts.png)

Remove the build scripts.

![](/images/RsyncUI/master/compile/nonscripts.png)

## Ready to Compile

Either execute RsyncUI directly in Xcode or utilize make. Go to the catalog top RsyncUI and execute the following command.

`make clean & make`

After the compiling is completed the RsyncUI.app is build and saved in:

`RsyncUI/Build/Products/Release/RsyncUI.app`

## Tools used

The following tools are used in development:

- Xcode (the main tool)
- make to compile new versions in terminal
- [create-dmg](https://github.com/sindresorhus/create-dmg) to create new releases
- [periphery](https://github.com/peripheryapp/periphery) to identify unused code
- [SwiftLint](https://github.com/realm/SwiftLint) to enforce Swift style and conventions
- [SwiftFormat](https://github.com/nicklockwood/SwiftFormat) for reformatting Swift code

All the above, except Xcode are installed by using [Homebrew](https://brew.sh/).
