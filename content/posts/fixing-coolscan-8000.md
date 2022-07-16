---
title: "Fixing My Nikon CoolScan 8000"
date: 2022-07-11T15:58:39-07:00
draft: true
categories:
  hobbies:
    - photography
tags:
  - coolscan8000
  - film-scanner
  - photography

---
[Go directly to the broken piece and repair]()

### Bought a CoolScan 8000
I recently bought a used Nikon Coolscan 8000 film scanner on eBay. These scanners are old, so much so that Nikon 
does not even manufacture them anymore. They were deprecated in early 2000s in favour of Coolscan 9000, and even 
9000s are not manufactured anymore! However, 8000 is much cheaper than 9000; while used 9000 go for around 
US$3000-5000, whereas used 8000 go for around US$1000-1500.

Given that these scanners are more than 2 decades old, they still have a cult following (check the [Facebook group](https://www.facebook.com/groups/1514948298527146)). 
The reason has to do with the excellent lens, true 4000dpi scanning resolution, 14 bit A/D (analog-to-digital) 
converter and, its autofocus mechanism.  

#### Why a film scanner? Why film photography at all?
The digital cameras have taken over everything. As a hobbyist though, I dislike the idea of taking 100 photos of a 
scene with the intention of choosing the good photos later. The "later" part never comes, and I am stuck with 
hundreds of photos where I can't decide which ones to keep and which ones to delete. 

Since photography is a hobby for me, I like to a take leisurely approach and deliberate about each photo before 
pressing the button. That, however, does not work when I am shooting digital; I feel compelled to keep taking 
pictures lest I may miss a great shot. Film cameras, force me to slow down. There is no 4 frames/second of shoot 
mode, no auto-bracketing, and not even a built-in light meter. 

On top of it, the quality of photos is hard to beat. I use medium-format film camera and the potential resolution of 
these 120mm films is no match for run-of-the-mill digital cameras. You have to shell out a minimum of US$10,000 to 
get similar digital camera; and they are bulky to carry around.

### The Trouble



### The fix and specification
I had to 3-D print one part, and ordered other parts from McMaster-Carr. I have provided the links for what I 
purchased from McMaster-Carr (non-affiliate links i.e I do not get any money from the links). I have provided the 
STL file for the missing part which I had to 3-D print.

#### Screws and washers
* Most of the missing screws are [M3x0.5mm of 8mm length](https://www.mcmaster.com/90258A178/) (i.e. 3mm diameter, 0.5mm screw pitch, 8mm length)
* Screws for motor are M3x0.5mm with 5mm length; however, I was able to use 8mm long screws
* The external cover and front face also uses [3mm washer](https://www.mcmaster.com/98689A112/) and [3mm split-lock washer](https://www.mcmaster.com/92148A150/)

#### Motor coupling 
I went through a few links given on the Facebook group, and many people had used a single-form coupling. However, 
that required that the shafts to be ground in order to fit one straight-edge of the coupling. I did not like the 
idea because I was worried that I may grind down too much, and also, I may have to return the scanner. So I used 
clamp-style jaw, zero-backlash, vibration-damping motor coupling made of aluminium by 
[Ruland](https://www.ruland.com/). These coupling come in three pieces, one hub for the motor shaft, one hub for worm 
drive shaft, and a coupling spider and are made in the USA.

These are, however, expensive (around $50) compared to a coupling like uxCell 5mm to 6mm rigid coupling on 
[Amazon](https://www.amazon.com/a13052700ux0251-Stepper-Coupling-Coupler-Encoder/dp/B00DCAIRIC) which is 
available for around $10. 

* The [motor shaft](https://www.mcmaster.com/9845T51-9845T416/) is 6mm diameter, 21.8mm long, 15mm outer diameter 
  (Ruland part MJC15-6-A)
* The [worm drive shaft](https://www.mcmaster.com/9845T51-9845T415/) is 5mm in diameter, 21.8mm long, 15mm outer 
  diameter (Ruland part MJC15-5-A)
* The [coupling spider](https://www.mcmaster.com/9845T485/) fits in the hubs of these coupling (Ruland part JD10/15-98R) 

I am a big fan of McMaster-Carr because of the quality components; Amazon is full of third-party sellers who are 
either a hit or miss. While you can return the order for full refund, it's a hassle to order from another seller if 
you didn't receive what you ordered, or if the product fails. 

#### Slide rails and shaft


