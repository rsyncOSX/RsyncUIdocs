+++
author = "Thomas Evensen"
date = "2023-11-10"
title =  "What is NavigationStack?"
tags = ["navigationstack"]
categories = ["general information"]
lastmod = "2023-11-12"
+++
There are several methods for navigation within SwiftUI, and one method is utilizing `NavigationStack`: "*A view that displays a root view and enables you to present additional views over the root view*". The root view is the tasks view, and the all other views like estimating details, execution of tasks and so on will be presented ontop of the root view. No more pop up views and I think the presentation of the other views connected to execution of tasks will be smoother and better.  

There will be a version to try out what `NavigationStack` is before release in a week or two. Personally I believe `NavigationStack` is more convenient, but most likely next release will enable the user to choose what to use by settings.

The code in the changed views are also cleaned up and easier to read. I have been working on this for a couple of days only, and it need some more testing before a *try out version* is published. 

### Views 

The main or *root view* when RsyncUI starts. For new users the *First Time* view is presented.  

{{< figure src="/images/navstack/start.png" alt="" position="center" style="border-radius: 8px;" >}}

Selecting the *Wand and stars* commence an estimating run and display the result ontop of the *root view*. The left arrow on the toolbar, upper left, indicates this is a view ontop of *root view*. Selecting the arrow returns the main view.

And of course double click on a row works as expected. First double click executes a dryrun, the details from dry run is presented on top of *root view*. Next double click executes the real run.

{{< figure src="/images/navstack/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

If a row is selected the details about estimation is presented ontop of the *estimated view*. 

{{< figure src="/images/navstack/details.png" alt="" position="center" style="border-radius: 8px;" >}}

Within the *estimated view* there is a *left arrow* on the toolbar upper right. Selecting it will execute the real synchronize run displaying the progressbar each task.

{{< figure src="/images/navstack/execute.png" alt="" position="center" style="border-radius: 8px;" >}}

First time info for new users of RsyncUI, with confetti.

{{< figure src="/images/navstack/confetti.png" alt="" position="center" style="border-radius: 8px;" >}}

