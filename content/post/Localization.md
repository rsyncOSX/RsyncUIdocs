+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Localization"
tags = ["Localization"]
# categories = ["general information"]
description = "RsyncUI speaks a few languages"
+++
RsyncUI and the menu app RsyncOSXsched are prepared for localization. Default language for both is English.

RsyncUI is localized to:

- English - the base language of RsyncOSX
- German - by [Andre Voigtmann](https://github.com/andre68723)
- Italian - by [Stefano Steve Cutelle'](https://github.com/stefanocutelle)
- Norwegian - by me

Localization is done by utilizing [Crowdin](https://rsyncosx.crowdin.com/u/projects/30) to translate the xliff files which are imported into Xcode after translating. Xcode then creates the required language strings. [Crowdin is free for open source projects](https://crowdin.com/page/open-source-project-setup-request).
