---
layout: post
title: "Adding Twitter functionality to Refinery CMS with refinerycms-tweets"
date: 2013-06-12 21:43
comments: true
categories: [Ruby, Rails, Refinery CMS]
---

[Refinery CMS](http://refinerycms.com/) is an open source Rails based CMS that I have used a couple of times, it's so simple to get up and running and highly customisable. It allows for functionality to be assed easily through [Rails engines](http://edgeapi.rubyonrails.org/classes/Rails/Engine.html). There are already a number of good engines out there that allow for adding pretty complex features in just a few commands.

I wanted to add a Twitter account to a site I was making for a client, they wanted to be able to change the account, number of tweets that kind of stuff. I couldn't find an engine out there so I put one together and was happy to be able to give something back for people like myself to use.

![Admin view of the Twitter account](http://cih-static.s3.amazonaws.com/refinerycms-tweets-screenshot.png)

I wont go into the technical implementation here as its probably better just to browse through the code and documentation on [github](http://github.com/cih/refinerycms-tweets). You can use a Twitter widget or a simple jQuery implementation with the option of a callback to render the results of the api call yourself.


