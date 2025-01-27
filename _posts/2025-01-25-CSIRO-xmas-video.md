---
layout: post
title: "See Spot Write"
date: 2025-01-26 07:00:00 +1000
tags: [cad, robotics, spot]
categories: [work]
author: Ross
image: 
  path: /assets/img/posts/chalk-header.webp
---
# CSIRO Christmas Video 2023

## Project Overview
I was asked to use the Robotics platforms we had at CSIRO Pullenvale to put together a unique Christmas Video, encorporating the technology in a unique way that would play well on social Media. The robotics division had recently bought a Boston Dynamics Spot with a Robotic arm mounted on it and i thought it would be technically impressive and a fun challenge to use the Arm to create a christmas message.


## Challenges & Solutions
Upon doing some background research i saw that Boston dynamics had implemented a rudimentary G-code intepreter, similair to how a 3d printer works. This had the unique benefit of interacting in the global frame of reference which mean that instead of being restricted to where the arm could move while the robot was static, it would be able to move itself and the arm together to form shapes.

However reading through the documentation i noted, to make it move in the global reference frame the force sensor on the arm had to be turned off, meaning if we were pushing a object on a uneven surface the object would likely have to be spring loaded to ensure constant force on the ground.

To solve this we could approach it by using a marking system that doesnt need to make contact directly and use a relatively flat surface but spray paints and robots seemed a bad idea. 

What i ended up on was designing a spring loaded chalk holder in Solidworks. Chalk being the obvious choice as it was easy to use and clean and it marks surfaces easily. 

After designing the chalk holder, I got to work in the code, the Boston Dynamics guys are actually pretty great with their example code and loading stuff in, is not that tricky, it requires to remotely login to the robot with ssh and you can basuically transfer files and ask it to run. They do however have a very scary "estop feature" which slams the robot down onto its belly when you press it. 

I had to scale my gcode because after testing i realised they had a scaling factor in their interpreter.


## Lessons Learned
After all of that i only had a day to try and get my footage for the video, and it was a day. In the end i must of done about 35 runs and ran into several issues. The gripper on the arm hand didnt have enough power to hold onto my chalk holder, The surfaces i were working on were VERY uneven causing me to change the Z height alot and wasting alot of chalk. I got a few decent runs and in the end the 37C  weather and the limited number of batteries caused this to not quite work as intended. I did manage to make a video that did quite well on the groups linkdin but it wasnt exactly what i had in mind. Still overall a very fun project combining so many different tools.

## Links & Pictures
- [Video Demo](https://www.linkedin.com/posts/navinda_well-done-csiro-robotics-csiros-data61-activity-7143799961690812417-YVQD) 

