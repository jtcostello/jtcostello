---
layout: page
title: Resin+LED Bedside Table
description: a wood/metal bedside table with resin and interactive lighting
img: assets/img/ledtable/ledtable_overview.jpg
importance: 2.5
category:
---
January 2019

<div class="row align-items-center">
    <div class="col-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/50 final 1.jpg" title="table" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/52 final 3.jpg" title="table" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

One night lying in bed I realized I didn’t have a bedside table or a nearby light; that needed to be fixed. I had been 
wanting to do something with woodworking for a while, so a light-up wooden bedside table was the perfect project. 
The final table includes a cherry top with light-up resin inlay, hidden touch-sensor, and a custom steel frame.

#### Wood Top

I started by picking up a large piece of Cherry from 
[Urbanwood](https://www.recycleannarbor.org/divisions/reuse-center/urbanwood) in Ann Arbor for the tabletop. 
I straightened the sides with the jointer, cut shorter planks the length of the table, and glued the planks 
together for a 30x30x2” top.

<div class="row">
    <div class="col-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/5 slab.jpg" title="wood" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Next I made a template and routed out a diamond shape for the lights and resin inlay. For the lights I used a 
waterproof WS2812 LED strip placed on the inner and outer sides of the inlay. These are RGB LEDs that are 
individually addressable allowing for animations to be displayed. They were hot glued down with the power/data wires 
going through a small hole to the back of the wood.


<div class="row align-items-center">
    <div class="col-7 col-sm-4 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/11 slot jig.jpg" title="jig for slot cutting" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-7 col-sm-4 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/12 slot.jpg" title="slot" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-7 col-sm-4 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/24 light slot.jpg" title="light slot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### Resin Inlay

The biggest challenge of the project was the resin inlay. Resin requires 75-85˚ temperatures to properly harden and I 
didn’t have a good place inside the house for letting it set while keeping fumes away. So that meant the garage was the 
only option, but December in Michigan does not come close to reaching the necessary temperature.

To keep the resin warm while hardening for 24 hours, I used a tarp to enclose a small section of the workbench and put 
a space heater inside. I poured the first ~1cm with clear resin to let more light through, then poured the top with a 
translucent blue. After hardening overnight, I sanded down the top and applied several coats of polyuerathane to 
finish the surface.

<div class="row align-items-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ledtable/25 resin 1.jpg" title="resin pour" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ledtable/26 resin 2.jpg" title="resin pour" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row align-items-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ledtable/27 sanding.jpg" title="sanding" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ledtable/28 finished top.jpg" title="finished top" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### Capacitive Sensor + Light Controller

Next I designed a capacitive touch sensor to make the lights interactive while keeping the surface simple and polished. 
I placed several small foil strips on the table underside, about 1cm below the surface. The Teensy microcontroller 
(an Arduino board) used to control the lights also has several pins capable of capacitive sensing; I wired the foil 
strips to these pins to detect when a user’s hand is present. By looking at which strips are activated, the 
microcontroller can determine which direction the hand is sliding, and dim the lights accordingly.

<div class="row align-items-center">
    <div class="col-8 col-sm-4 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/40 cap sensor.jpg" title="capacitive sensor" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-8 col-sm-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/41 cap slot.jpg" title="capacitive sensor slot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


#### Metal Base

For the table frame, I cut and welded square steel tubing into a unique diagonal base. I sanded the frame, 
spray-painted it black, cut holes for running a power cable through the sides, and screwed it to the table-top.


<div class="row align-items-center">
    <div class="col-6 col-sm-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/30 metal.jpg" title="metal" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6 col-sm-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/32 welding 2.jpg" title="welding" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row align-items-center">
    <div class="col-6 col-sm-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/35 metal stand 1.jpg" title="metal stand" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6 col-sm-6 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/36 metal stand 2.jpg" title="metal stand" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### Final Table
I’m very happy with how the final table turned out. Along the way I learned many more skills in woodworking, 
resin pours, and welding. Now the table sits next to my bed and I have fun playing with the lights every night.

<div class="row align-items-center">
    <div class="col-5 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/light anim 1.gif" title="light animation" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-5 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/light anim 2.gif" title="light animation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-7 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/51 final 2.jpg" title="table" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row align-items-center">
    <div class="col-5 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/50 final 1.jpg" title="table" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-5 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/ledtable/52 final 3.jpg" title="table" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


