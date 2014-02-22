---
layout: post
title: "Making life easier with chrome extensions"
date: 2013-08-24 11:00
comments: true
categories: [Chrome, Javascript, Extensions]
---

Often as a developer I find myself looking for tools and techniques that will speed up or simplify any mundane or repetitive tasks I have to carry out. In some cases all it will take is a few lines of code here, or a little script there and I can save precious seconds to use elsewhere. It's important to share this time saving across the team if it is something everyone can benefit from, especially if they are non-technical and perhaps could not implement something similar themselves. Obviously distributing scripts to non-technical colleagues is not the way to go, here is an example of how a simple chrome extension helped out my team.

<!--more-->

At [Specle](http://specle.net) we deliver print and tablet ads to publishers across the UK and Europe, each of these ads is called a "job". The support teams will regularly be looking up jobs mostly for customer queries and the dev team have the odd technical query so it can be a pretty common task. This involves navigating to an admin page in the browser, then entering a job number, searching and finally selecting the job from the results. The way I see it there are at least a few clicks that can be avoided there!

Now pretty soon after I started I set up a javscript bookmarklet that allowed me to enter a job id and would take me to the page, sweet! Super simple, here it is.

```javascript
javascript:(function(){var job=prompt("Specle Job Number","ID");window.open('http://specle.net/specle_send_jobs/' + job, '_blank');})();
```

So adding this as a bookmark url, when you visit the bookmark a prompt appears, enter the job number and away you go. Now this is pretty handy for me, its also easy to set up, but distribution would be a bit tricky. I would be creating bookmarks on other machines or providing instructions for some copy and paste so I decided to go for a more complete solution. All of us at Specle use chrome as our main browser (we have conditioned them well) so I figured a simple chrome extension would be a nicer way to distribute to the team. It also has the advantage of being easier to update and adding a keyboard shortcut to the extension removed one more click for me! I don't plan to go into the details of writing the extension as there are loads of great [resources](http://developer.chrome.com/extensions/getstarted.html) already but here is a link to the code on [github](https://github.com/specle/specle-chrome) if you want to take a look.

->![](http://cih-static.s3.amazonaws.com/blog/specle-chrome-screenshot.png)<-

If you want to publish your extension through the Chrome Developer Dashboard then you don't need to worry about [packaging](http://developer.chrome.com/extensions/packaging.html) it but to distribute a non-public version you can create the package and it can be hosted and installed with the click of a link, or so I thought! Google no longer allows extensions to be installed directly from a url for good reasons that are explained [here](https://support.google.com/chrome_webstore/answer/2664769?p=crx_warning&rd=1). This did mean that it is not quite as simple as I was hoping for in terms of installation, the process is to download the packaged ```.crx``` file and drag it onto the extensions page in chrome. Not ideal but certainly preferable to the bookmarklet method, plus it looks nicer too!

As a final little tip, in chrome if you go to ```Window > Extensions``` and scroll all the way to the bottom and hit the ```Keyboard Shortcuts``` link you can set shortcuts for all of your extensions.

