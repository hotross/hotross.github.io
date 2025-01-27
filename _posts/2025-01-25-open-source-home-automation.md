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

I have a love-hate relationship with home automation. In many ways, it's a microcosm of how we interact with technology today. It can be truly useful, offering novel ways to interact with our homes, aid people with disabilities, and help us monitor for accidents or disasters—sometimes even preventing them altogether.

However, that's not the reality for most home automation systems. Almost every device on the market requires IoT devices to be connected to the internet, meaning that before you can even turn on your porch light, a message is sent to a server halfway around the world. This doesn’t sit well with me. Sure, you can configure your IoT devices on a separate VLAN to prevent them from calling home, but this usually renders them inoperable. I wanted a better way.

### The Search for a Local Solution

Back in 2018, when I first started exploring home automation, there were very few options for truly local home automation. Home Assistant existed, but it was a large-scale project designed for managing complex routines. All I wanted was a simple solution to control a few lights and check the temperature in my house. That's when I discovered **Tasmota**.

### Why Tasmota?

In 2018, most IoT devices used a popular microcontroller called the **ESP8266**. Why was it so widely used? It was cheap, had a decent amount of I/O capabilities, and the documentation was excellent. Smart developers realized they could remove these chips from inexpensive Chinese IoT devices, reprogram them, and run their own firmware. And thus, **Tasmota** was born.

### The Early Struggles

At first, reprogramming these devices required a bit of technical know-how. I struggled in the beginning but documented what worked for me across several different devices. I shared this knowledge on forums, and over time, a small community formed around the project. People began helping each other with firmware uploads, and we shared ways to extract sensor data and integrate devices into our systems.

### A Shift in the Market

Tasmota was revolutionary for a while, but over the past year or so, things have changed. New microcontrollers targeting IoT devices have hit the market, and many now come with locked firmware, making reprogramming more difficult. Despite this, there are still plenty of opportunities to experiment with IoT devices, and Tasmota remains a valuable tool for those willing to dive in.

### Some of My Tasmota Projects

Here are a few of the devices I’ve reprogrammed and the use cases I’ve explored with IoT technology:

- **[Kogan Air Conditioner](https://templates.blakadder.com/kogan-KAPRA14WFGA.html)** 
- **[Light and Fan Switch](https://templates.blakadder.com/deta_6914HA.html)** 
- **[Outdoor Light](https://templates.blakadder.com/arlec_ABL015HA.html)**
- **[Power Strip](https://templates.blakadder.com/useelink_SM-SO301AU.html)** 

### Photos

![Cat Water Fountain](/assets/img/posts/Catwaterfountain.webp)


