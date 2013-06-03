---
layout: post
title: "A two minuite solution to backup a remote server"
date: 2013-05-29 09:36
comments: true
categories: [rsync backups]
---

Until recently I had a pretty unorganised approch when it comes to backing up my data. That's not to say I didn't undertand the importance of it or that I didn't do it at all, but it was certainly not an automated or even regular process.

I have a couple of servers on the cloud hosting service [DigitalOcean](https://www.digitalocean.com/), which is worth checking out if you haven't already. DigitalOcean does offer to take backups in the form of a snapshot of you server, which is great, but it is nice to know that the important code or whatever is in more than one place. Anyway enough talk here are the commands to set this up.

```
rsync -r -t -v --progress --delete -c -l -z user@remote_ip:/ ~/Downloads/Backups/DigitalOcean/ServerOne
```

Thats it, just one line! You just pass the user, remote IP and path (in this case I sync the root directory) for the source folder, then the location of the destination folder. There are a bunch of options too, if you want to find out what the options I am passing in this command are doing just type the following.

```
rsync
```

I actually made a shell script (consisting of this line repeated once for each server) that I chucked into the init.d directory and ran via a cron job. Admittidly this is not the most complete solution but not bad for 2 minuites work and will certainly do the job for what I need at the moment.