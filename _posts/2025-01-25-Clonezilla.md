---
layout: post
title: "Clonezilla"
date: 2025-01-26 07:00:00 +1000
tags: [automation, windows, clonezilla]
categories: [work]
author: Ross
image: 
  path: /assets/img/posts/pikvm1.webp
---
# Operating Systems and Embedded Devices

Every single job i have had, required me in some way or another to put a operating system on a device. If you name a way to do this task , most likely I have done it thousands of times, everyone has their own special hacks or changes that they think makes their system a little better, I am here to tell you almost all of them suck. I should rephrase, if you are loading a single Operating system one time in a day a USB stick, a copy of Rufus and a can do attitude works great. If your needs are slightly more complex then it is a uphill battle fighting configuration changes, scale and sheer complexity. Most technicians aren't software engineers and most software engineers find no pleasure in figuring out infrastructure needs when time and a annoyed technician will do the work.

I ended up becoming very frustrated with this system. In my job were were using norton ghost to load windows XP images onto embedded machines and this took nearly 2 hours per machine and it was VERY prone to corrupting either the USB stick or the device. Browsing around for a better solution i found clonezilla, which seemed a touch more modern and had rave reviews. I switched over and it worked much better, the image writing system they used was much more stable and it worked alot faster.

Next issue, The user interface was terrible, many times customers would send back systems that they could reflash themselves... that is they could reflash themselves if the UI for clonezilla was very intimidating, i had a little experience with linux systems and i new how to make menus in Whiptail, sure enough clonezilla had a way to implement that. This really helped us let customers reload software with guardrails up. their USB stick was configured to only their system and if it didnt work well, thats okay send it back.

We also had another issue, We had 6 different embedded devices for the mining industry, each required a different cloned image and each software updates pushed by the developers often required new dependencies that our core program didnt have installed. Me and one of the QA team developed a very rudimentary CI/CD pipeline where he would install the dependencies on a system, clone it and i would load it onto a network share. Instead of loading the systems straight from the USB we would load them over a NFS share. A big bonus of this system was the speed increase and we no longer had 5 diferent versions of images for each system. We had one standard one that was approved to work with the newest system from QA

About halfway through the lifecycle of these embedded systems the manufacture urged us to do a firmware update on the microcontroller in the computer as it was causing some power issues. This would of been a massive recall. We had thousands of devices out in the field and the firmware update required many speciality software tools and knowledge to work. I was tasked to see if i could find a better way. The microcontrollers were Atmel chips and i knew linux had a tool for working with these called AVR-dude. I attempted to use this tool with clonezilla as it was simply a temp operating system but rightfully so the dev had made everything read only. Thankfully the documentation for clonezilla was wonderful and after looking at some examples i realized i could mount the filesystem on my PC, install the tools and software i need and then close the system back up.

This allowed the system to first do the firmware update, then do the reimaging. This meant any old minesite tech could jump onto the machine with his USB stick and then the update would be complete in a matter of minutes without ever having to remove the machine.

Another issue we were running into were remote deployments in Indonesia. Hardware available in indonesia was not allowed to be purchased in AUstralia due to import laws so our hardware could not be loaded before hand. Usually this wouldnt be that bad but the technicians spoke very little english and due to covid proper training could not be done. The solution i came up with was using a Raspberry pi and a HDMI to usb adapter to make a rudimenerary KVM that could load software and do configurations with a tech just plugging it in and unplugging it. 

I have also successfully used clonezilla to multi image devices using a torrent network, allowing for rapid deployment of up to 100 devices at once. It is a very cool technology but i only really scraped the surface.

## links
- [Clonezilla](https://clonezilla.org/)

## Photos

![PIKVM](/assets/img/posts/pikvm1.webp)
![Firmware and Imaging](/assets/img/posts/imagingandfirmwareupdate.webp)
![Firmware and Imaging](/assets/img/posts/imagingshelf.webp)