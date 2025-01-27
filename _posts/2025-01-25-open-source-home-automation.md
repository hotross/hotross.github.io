---
layout: post
title: "Open source home Automation"
date: 2025-01-26 07:00:00 +1000
tags: [automation, home, firmware]
categories: [home]
author: Ross
image: 
  path: /assets/img/posts/catwaterfountain1.webp
---
# Me and Tasmota

I have a love hate relationship with home automation, in many ways is a microcosm of the way we interact with technology today. It can be truly useful and allow us to interact with our home in novel ways that aid people with disabilities and help us monitor for accidents, disasters and in many cases prevent them....

However that isnt what most home automation is, almost everything on the market requires IoT devices to be hooked up to the internet and before tou turn your porch light on send a message to a server half way around the world. I am not a fan of this. Of course there are ways around this you can VLAN you IoT devices to make it impossible for them to call home, but usually this makes them inoperable. I sought a betterway

Back in 2018 when i started looking into home automation there were almost no names in Local home automation. Home assistant exsited but it was a large scale project for managing complex routines. I wanted to turn a few lights on and off and see what the temperature was in my house. Then i found tasmota

Most IoT devices back in 2018 used a fairly ubiquitous microcontroller called the ESP8266. WHy was it used in all devices? It was cheap, had a decent amount of I/O and the documentation was great. So smart people figured that they could pull these devices out of cheap chinese IoT devices and reprogram them, thus tasmota was born. 

Reprogramming required a bit of technical knowhow at the beginning. I had struggled and documented what had worked for me on a few different devices. I passed on that knowledge to the forums and eventually we had a little community of people showing how to upload firmware to these devices and pull info from the sensors. 

Linked are a few of the devices i reprogrammed and pulled sensor data from as well as some of the fun use cases i found for IoT devices. 

Tasmota has become a little defunct in the last year or so, many other microntrollers have hit the market targetting IoT devices and those devices have the ability to lock firmware uploads. There are still other




## Articles I Wrote
- [Kogan Aircondtioner](https://templates.blakadder.com/kogan-KAPRA14WFGA.html) 
- [Light and Fan Switch](https://templates.blakadder.com/deta_6914HA.html)
- [Outdoor Light](https://templates.blakadder.com/arlec_ABL015HA.html)
- [Power Strip](https://templates.blakadder.com/useelink_SM-SO301AU.html)
## Photos

![Cat Water Fountain](/assets/img/posts/Catwaterfountain.webp)