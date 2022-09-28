+++
author = "Thomas Evensen"
date = "2021-04-17"
title =  "How to compile RsyncUI"
tags = ["config files"]
categories = ["general information"]
+++
RsyncUI is only depended upon the Swift language and SwiftUI and Foundation frameworks. There are two ways to compile, either in Xcode or utilize `make` from command line in RsyncUI catalog. To use make require Xcode command line utilities to be installed. Execute the following command and follow the instructions.

`xcode-select --install`

## Remove signing credentials or replace

To compile you have to either remove signing or replace signing credentials. To remove or replace select Target RsyncUI and tab "Signing and Capabilities".

## Compile scripts

There are two utilities used, [SwiftLint](https://github.com/realm/SwiftLint) and [SwiftFormat](https://github.com/nicklockwood/SwiftFormat). Both can be removed, select tab "Build Phases" and delete the lines. Or you can use [Homebrew](https://brew.sh/index_nb) to install both utilities.

## Ready to Compile

Either execute RsyncUI directly in Xcode or utilize make. Go to the catalog top RsyncUI and execute the following command.

`make clean & make`

After the compiling is completed the RsyncOSX.app is build and saved in:

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
