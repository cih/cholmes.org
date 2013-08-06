---
layout: post
title: "Multiple ruby versions using proxy_pass with nginx, passenger and rvm"
date: 2013-08-03 18:49
comments: true
categories: [Nginx, Passenger, RVM]
---

I recently set up [gollum](https://github.com/gollum/gollum), a sinatra powered, git based wiki on a [DigitalOcean](https://www.digitalocean.com/) server that already had a number of other sites running on it. The server had passenger, nginx and rvm installed running ruby version 1.9.2 and gollum required >= 1.9.3 so it needed to be able to run multiple ruby versions. Here is a simplified example to show what the `nginx.conf` file was looking like, pretty standard stuff.

<!--more-->

```
http {
    passenger_root /usr/local/rvm/gems/ruby-1.9.2-p320/gems/passenger-3.0.19;
    passenger_ruby /usr/local/rvm/wrappers/ruby-1.9.2-p320/ruby;

    server {
       listen 80;
       server_name mysite.com;
       root /var/www/mysite.com/current/public;
       passenger_enabled on;
    }
}

```

To run a different ruby version without interfering with any of the existing sites on the server I decided to run a standalone instance of passenger and use nginx's proxy_pass to pass on the requests. Adding the site to the `nginx.conf` looked like this.

```
server {
      listen 80;
      server_name myproxysite.com;
      root /var/www/myproxysite.com/current/public;
      location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_set_header Host $host;
      }
   }
```

Then just a case of starting the passenger instance and restarting nginx.

```
cd /var/www/myproxysite.com/current/
rvm use 1.9.3 # You will need passenger gem installed
passenger start -a 127.0.0.1 -p 3001 -d # -d runs the process in the background
/opt/nginx/sbin/nginx -s reload
```