+++
author = "Thomas Evensen"
date = "2020-04-16"
title =  "Signing and notarization"
tags = ["notarize","signed"]
categories = ["sequrity"]
description = "Some info about signing and notarizing."
lastmod = "2020-08-06"
+++
RsyncUI is signed with my Apple ID developer certificate and [notarized](https://support.apple.com/en-us/HT202491) by Apple. This means both apps are verified and checked for not containing malicious code. It ensures the users that the apps are clean and that they are working together with Apples Gatekeeper technology. A message from Apple is issued when opening either a new or updated application the first time.

From macOS 10.15 Catalina, [notarizing is required for all software](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution).
