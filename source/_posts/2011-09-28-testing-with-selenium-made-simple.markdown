---
layout: post
author: Chris Holmes
title: "Testing With Selenium Made Simple"
date: 2011-09-28 14:32
comments: true
categories: [Testing, Selenium, Ruby, Rails]
---

Using Selenium RC in your Rails project was never easier...
-----------------------------------------------------------

Testing is one of those things that can get overlooked when developing web applications! I started off as a tester and when doing my own development projects I like to make it as simple and easy to maintain as possible.

<!--more-->

I found Selenium RC really simple to use, I started off using Selenium IDE to record my tests and exporting them to Ruby code to edit and improve them. Having a suite of tests is great but I found that as a tester I was the only one using them. I have put together a [gem](https://rubygems.org/gems/selenium-rake "selenium-rake") that packages the selenium server, a few rake tasks and an example test generator. This means that as a developer you can install one gem and from there you can run your tests with one command! This will also allow testing teams to work on scripts and the files can then be used by the developers before the testers see the site.

Doesn't matter if you prefer RSpec or Test::Unit both are fine! Below is a short guide on getting set up and using it.

Installing
----------
At the command line...
``` ruby
gem install selenium-rake
```
or in your gemfile
``` ruby
gem 'selenium-rake'
```
(not forgetting to run _bundle install_)

You will need to check that you have Java runtime environment installed. To do this just type...
``` ruby
java -v
```
If not you can get it [here](http://java.com/en "Get Java")

This will give you the Selenium server and it will make 4 rake tasks available for you. You can also generate an example script to get you started. This can be found in the test/functional directory.
``` ruby Generating an example script
rails generate example
```
You can start using these rake tasks
``` ruby Generating an example script
rake rc # This excecutes all of the rake tasks below
rake rc:start # This starts the Selenium server
rake rc:tests # This runs all tests in test/functional directory with _selenium in the filename
rake rc:stop # This stops the Selenium server
```
Now you can start to play, put your test files into the test/functional directory and use _rake rc_ and your good to go!!

Want to help improve this gem [pull requests](http://www.github.com/cih) are very welcome!