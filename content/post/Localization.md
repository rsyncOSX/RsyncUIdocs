+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Localization"
tags = ["Localization"]
categories = ["general information"]
description = "RsyncUI speaks several languages."
+++
RsyncUI and the menu app RsyncOSXsched are prepared for localization. Default language for both is English.

RsyncUI is localized to:

- Norwegian - by me
- English - the base language of RsyncUI

Localization is done by utilizing [Crowdin](https://crowdin.com/project/RsyncUI) to translate the xliff files which are imported into Xcode after translating. Xcode then creates the required language strings. [Crowdin is free for open source projects](https://crowdin.com/page/open-source-project-setup-request).

Volunteers are wanted for translating to other languages. Please create an issue if you have possibility to translate. Translating to new languages is mostly a proofreading exercise. [Crowdin](https://crowdin.com/project/RsyncUI) does most of the work and proofreading is last step before importing into code.
