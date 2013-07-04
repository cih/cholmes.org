---
layout: post
title: "Scripting Automater to upload files to S3"
date: 2013-07-03 18:43
comments: true
categories:
---

For me sharing a screenshot used to involve opening up [Transmit](http://panic.com/transmit/), dragging the file in from finder, setting the premissions and copying the URL. Now Automater and a simple shell script enables me to right-click on an image and select "Upload to S3", this uses curl to upload the file to S3, puts the URL of the file on my clipboard and triggers a notification when the file is uploaded. This example uses [Growl](http://growl.info/) for the notification but its easy enough to use a different method if you want. Nice and simple, so here is how to got it set up..

<!--more-->

Firstly open up Automater and create a new service.

->![](http://cih-static.s3.amazonaws.com/blog/automater_service.png)<-

From the dropdown for "Service receives selected" select "files or folders" in "Finder", this sets the context for where your new service will be available. From the library on the left choose "Utilities" and drag "Run Shell Script" into the main window. Change the "Pass input:" dropdown to "as arguments" which will pass the file into the script as an argument.


->![](http://cih-static.s3.amazonaws.com/blog/automater_script.png)<-

The screenshot above shows an example script. The first part copies the url to your clipboard and removes whitespace from the filename, the curl command does the uploading and the final part is for the notification once complete.

Uploading to S3 using using HTTP POST requires a few prerequesits, one of which is a policy document which S3 uses for authorisation and imposes limits on the files that can be uploaded and the other is a signed version of this document known as a signature. If you want to generate the signature and policy document yourself you will find all the infomation in this [article](http://aws.amazon.com/articles/1434).

I have put together a ruby script that will abstract all of this and give you the script to paste into Automater based on your S3 credentials, bucket name and upload directory. Just replace the four variables at the top with your S3 access key, secret key, bucket name and directory name. The script just takes the S3 policy document and Base64 encodes it and creates a signature value using your secret key and outputs the shell code that will copy the url to your clipboard, upload the file using curl and then using growl notify you when the upload is complete.

{% gist 5920884 %}

Save a copy, update the variables and make sure it is executable.

```
  vim automater_to_s3.rb # Paste in the code above and edit the variables, save and quit
  chmod 777 automater_to_s3.rb
  ruby automater_to_s3.rb
```

Paste the output from the script and hit save and give your service a name, I chose "Upload to S3". When you right click on a file you will see the option. You will notice that the policy document in this example restricts content type and file size, feel free to change this if you want to upload different file types.