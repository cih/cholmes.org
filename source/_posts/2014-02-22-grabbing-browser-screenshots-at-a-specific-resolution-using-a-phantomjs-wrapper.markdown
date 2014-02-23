---
layout: post
title: "Grabbing browser screenshots at a specific resolution using a phantomjs wrapper"
date: 2014-02-22 22:36
comments: true
categories:
---

I found myself using [phantomjs](http://phantomjs.org/) a few times recently as an easy way of capturing browser screenshots at a specific resolution. It's a great tool and was nice and simple to get setup but I kept having to refer back to my notes to remind myself of the command so I wanted to make it a little easier for me to use.

<!--more-->

Before
------
```
	phantomjs /path/to/js/file.js http://google.com my_screenshot.png 1024 768
```

The method that I was using to take the screenshot was to pass a JavaScript file to phantomjs along with a url, output file path, width and height. So nothing difficult here, but there was an easy opportunity for fewer keystrokes and nice `help` option to remind me of the argument order.

After
-----
```
	screenshot help
	=> screenshot <url> <width> <height> # Creates a screenshot-timestamp.png in the current directory

	screenshot http://google.com 1024 768
```

So now I don't have to think about where the js file is located, plus I have another handy feature in that after the screenshot is taken the image is opened for me to take a look, also by adding this script to my `$PATH` I can use it from anywhere. Not the most complicated hack but a good example of how something simple can make a task such as this easier, that's what it's all about!

You can grab the script [here.](https://gist.github.com/cih/9165262)