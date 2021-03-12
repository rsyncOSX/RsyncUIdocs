+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "JSON support"
tags = ["json","config file"]
categories = ["general information"]
description = "Some info about signing and notarizing."
lastmod = "2020-12-13"
+++
RsyncUI supports read and write configurations and logs as [JSON](https://en.wikipedia.org/wiki/JSON) files. The user will have the option to convert existing configurations and logs from [PLIST](https://en.wikipedia.org/wiki/Property_list) to JSON and the other way.

Before converting to either, [in user configuration](/post/userconfiguration/), make a backup of the current configuration files. The current configurations is backed up in the catalog `$Home/Documents/RsyncOSXcopy-$date-suffix`.

## Enabling JSON

To enable JSON support is a **two step** process. Go to User settings and select the JSON tab. There is two actions:

- Verfiy - verify after Convert either converted JSON or PLIST files
- Convert -  will transform the current format to either JSON or PLIST, after Convert choose Verify

After transforming, the second task is to enable JSON support by selecting the `JSON` option [in user configuration](/post/userconfiguration/)

## JSON enablet

RsyncUI will automatically quit and after a restart JSON support is enablet. For new users only select the `JSON` option to enable JSON support.

A yellow label indicates JSON support is enablet. The JSON files are stored in, add profilename if profile is used:

- `./rsyncosx/macserial/configurations.json` for configurations
- `./rsyncosx/macserial/schedules.json` for schedules
