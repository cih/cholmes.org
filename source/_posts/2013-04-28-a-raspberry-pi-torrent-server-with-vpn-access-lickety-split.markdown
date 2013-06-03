---
layout: post
title: "A Raspberry Pi torrent server with VPN access, lickety-split!"
date: 2013-04-28 15:28
comments: true
categories: [Raspberry Pi, VPN, Torrent]
---


This is a quick guide so setting up a torrent server on your RaspberryPi. So next time you think of something you want to download you can get it going so that it will be waiting for you when you get home.

This assumes that you have alreay got your OS installed, if not there is an easy to follow [guide](http://elinux.org/RPi_Easy_SD_Card_Setup), I went for the [Soft-float Debian](http://www.raspberrypi.org/downloads) "wheezy" distro. You will need to have a monitor and keyoard connected the first time you boot your Pi, at this point you will be given a few config options only one to worry about for this guide is enabling ssh.

Just a bit of setup on the machine you will be using to acess the Pi remotely. I dont have a public facing IP address on my home network so in order to be able to access the Pi while I am away from home I need some way to connect to it over the web. Enter [Hamachi](https://secure.logmein.com/products/hamachi/)! LogMeIn Hamachi is a hosted VPN service, you can download the [unmanaged client](https://secure.logmein.com/products/hamachi/download.aspx) here and have up to 5 machines on a network for free (at time of writing).

Just follow the installer for the client and once done all you need to do is create a newtwork that you will be able to connect to from the Pi. Navigate to Network > Create Network and you will see the dialog below.

![Create Hamachi Network](http://cih-static.s3.amazonaws.com/create-hamachi-network.png)

So now we can get the Pi setup and connected to our Hamachi network. Now we ssh into the Pi, there is no reason that you can't set this up in a terminal on the Pi but for the pupropse of testing the VPN later it makes sense to do it this way.

```
  ssh pi@< your-ip-address-here >
```

Enter your password when promted, if its the first time you have ssh'ed in from your machine you will be asked to confirm that you want to connect. This will add the RSA to your know_hosts file.

Now we download the Hamachi installer.

```
  sudo wget https://secure.logmein.com/labs/logmein-hamachi_2.1.0.86-1_armel.deb
```

Then install it.

```
  sudo dpkg -i logmein-hamachi_2.1.0.86-1_armel.deb
```

Join the network that you created using the client earlier.

```
sudo hamachi join <network-name> <password>
```

That's it we can now test it out by ssh'ing into the Pi from the public IP, open the hamachi client on your machine and right click on the Pi machine within the network you just created and select 'Copy Ipv4 address'.


Now we have the Pi set up with VPN access, just get the torrent server set up and we are ready to go.

```
  sudo apt-get install transmission-daemon
```

```
  sudo service transmission-daemon start
```

By default this will download files to /var/lib/transmission-daemon/downloads directory. You may need to edit the settings file to whitelist your IP or change your password etc. You can see full details of the settings on the [transmission docs](https://trac.transmissionbt.com/wiki/EditConfigFiles).

And thats it! You can get the public facing IP for the transmission web interface from your Hamachi client. The web interface runs on port 9091 so navigate in your browser and away you go. Enjoy!

