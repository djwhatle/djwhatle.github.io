---
layout: post
title:  "Building an ATX power supply enclosure"
categories: general
---
![atx_image_1](/assets/atx_power_supply/image_1.jpg)

I've been working on a lot of digital electronics based projects recently. When I'm working maker-grade devices (such as the recently popular ESP8266 WiFi capable microcontroller), I need to source a good amount of current at a standard digital voltage.

An ATX computer power supply can provide many useful DC voltages for digital applications (3.3V, 5V, 12V). I bought a $20 Corsair power supply from Newegg and started my research. It proved trivial to break out the voltages in the style of a lab power supply. I wanted to make something that would look cooler than an ATX power supply sitting on my desk, so begun designing an enclosure.

This was my first laser-cutting project. I was able to use the resources available at the NCSU Entrepreneurship Initiative Garage to cut everything out. I am lucky to have access to a Universal Laser Systems 60W CO2 laser through the EI. The whole project cost $27. The power supply is actively cooled and capable of supplying up to 430 watts of power.

![atx_image_2](/assets/atx_power_supply/image_2.jpg)

Having no experience with vector graphics creation, my first design was created with [MakerCase](http://www.makercase.com/), a really cool Javascript-based enclosure generator. Unfortunately, the auto-generated plans weren't structurally sound, and they were pretty ugly. It took cutting the plans out and putting the box together to realize it wouldn't work. I was forced to embrace "fail early and fail often".

![atx_image_3](/assets/atx_power_supply/image_3.png)

![atx_image_4](/assets/atx_power_supply/image_4.jpg)

After cutting the first revision and being unsatisfied, I decided to create my own design. I am taking a Solidworks class at NCSU, so I took the path of least resistance and used the tool I knew. [An Adafruit guide](https://learn.adafruit.com/laser-cut-enclosure-design/overview) provided some great guidelines for getting started with laser cut enclosure design.

{:class="center-p"}
![atx_image_5](/assets/atx_power_supply/image_5.png)

I based my drawing files on equations which can be modified all in one place. This allows for quick revisions.

{:class="center-p"}
![atx_image_6](/assets/atx_power_supply/image_6.png)

From Solidworks I exported an SVG. Adobe Illustrator was then used for front-panel re-arrangement and graphics/vent placement. I used Google's image search tools to find a cool looking vector graphic representing an "ideal voltage source". Tying together the technical and artistic aspects of the design made me happy.

![atx_image_7](/assets/atx_power_supply/image_7.png)

![atx_image_8](/assets/atx_power_supply/image_8.png)

![atx_image_9](/assets/atx_power_supply/image_9.jpg)

After cutting everything out, I made sure everything would fit together and then proceeded to cut all of the connectors off the ATX power supply, leaving only shortened wires. I put both banana jacks and screwterms on the front panel. I figured this type of configuration would maximize versatility. I would like to add some USB ports if I build another one of these in the future.

![atx_image_10](/assets/atx_power_supply/image_10.jpg)

I always have a few Arduino Pro Mini's lying around to embed in projects (Arduino is an easy to program microcontroller in case you aren't familiar). I also had some WS2812B RGB LED's from China that tend to break every time I put any strain on them (great for putting in a box and never touching!). I programmed a boot-up and shut-down animation that also serves as a power indicator. White masking tape works great as a cheap light diffuser, especially when LED's are mounted at close range.

![atx_video_1](/assets/atx_power_supply/video_1.gif){:class="width-100"}

![atx_image_11](/assets/atx_power_supply/image_11.jpg)

![atx_image_12](/assets/atx_power_supply/image_12.jpg)

![atx_image_13](/assets/atx_power_supply/image_13.jpg)
