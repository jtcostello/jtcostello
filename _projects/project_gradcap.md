---
layout: page
title: Grad Cap Light Display
description: a custom circuit board with 100 rgb leds
img: assets/img/gradcap/gradcapoverview.png
importance: 1
category:
---

<video width="640" height="360" controls>
    <source src="/assets/40 board video.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>


<img src="/assets/img/gradcap/gradcapoverview.png" width="50%" height="50%" class="rounded mx-auto d-block" alt="grad cap overview">


May 2020

Back in February, I started designing a light-up graduation cap for my undergrad graduation ceremony 
scheduled for May (ultimately cancelled because of the pandemic). As an electrical engineer and 
soon-to-be neuroengineering grad student, I took inspiration from circuit-brain designs 
<a href="https://www.shutterstock.com/video/clip-1020844972-creative-circuit-brain-semispheres-4k-uhd-animation">like this </a>.
Others <a href="https://hackaday.io/project/11725-wireless-led-matrix-grad-cap-display">have put LED matrix displays</a> on their grad cap and programmed cool animations across the screen. 
But this seemed too easy and all designs disappeared as soon as it turned off. I wanted something that 
could light up with animations, but also have a permanent design for display. I settled on creating 
a custom circuit board with small LEDs animating a printed design. 

After drawing a few sketches including a full-size drawing, I created the design in Photoshop. 
The mortarboard has an inconvenient 0.75in hole for the tassel so I made sure it was centered 
nicely within the M. I exported the design as an SVG and imported into Eagle.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/00 stick note sketch.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/01 big sketch.jpg" title="sketch 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/03 black letters with M.png" title="psd design" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

I chose to use WS2812b RGB leds, which are commonly used in LED light strips. I went with the 3.5mm SMD LEDs which were 
the smallest I could reliably hand-solder (for future board iterations I may try the 1.5mm LEDs for a higher resolution 
display). The LEDs are chained together and only need a single data line for control, making it very easy to created 
individually-addressable displays with a few lines of code. I ended up using 96 LEDs evenly spaced around the board to 
animate the “neural activity”.

For the microcontroller I chose the Atmel328p, the same as on the Arduino Uno, allowing for compatibility with the 
standard Arduino IDE. A small lipo battery would power the board and fit on the underside of the grad cap, hidden from view.

I created the schematic and laid out the full board in Eagle. I added a pin header to program the microcontroller and 
breakout connections to manually control the LEDs (which were very useful when the microcontroller wasn’t working). 


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/08 micro schematic.png" title="sketch 1" class="img-fluid rounded z-depth-1" %}
    </div>
<div class="row">
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/09 leds schematic.png" title="sketch 1" class="img-fluid rounded z-depth-1" %}
    </div>
<div class="row">


After finalizing the PCB design, the next challenge was finding a manufacturer to make it for a reasonable price. 
OSHPark and a couple others would charge almost $500 for the 100in2 board. I went with JLCPCB who produced the 5 copies 
of the full board with faster shipping for $52. Even in mid-March with Coronavirus in full-swing in China, 
the boards arrived in only a couple weeks.


<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/20 gradcap_schematic_top.png" title="schematic" class="img-fluid rounded mx-auto d-block" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/21 gradcap_schematic_bottom.png" title="schematic" class="img-fluid rounded mx-auto d-block" %}
    </div>
<div class="row">


Once the boards and all components arrived, I got started on the 450+ solder connections. I connected an external 
Arduino to the LED input pins and verified the connections each time I added another LED. The main problem with using 
only a single data-line for all the LEDs is if a single connection is bad, then the whole string of lights fails 
(but it’s obvious where the bad connection lies). 

<div class="row">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/30 assembly 1.jpg" title="assembly" class="img-fluid rounded mx-auto d-block" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/33 3 assembly lapse x4 cropped gif.gif" title="assembly" class="img-fluid rounded mx-auto d-block" %}
    </div>
<div class="row">


Now the fun part: programming the light animations. Adafruit’s Neopixel library made it easy to set each LED’s color 
and brightness. I recorded each LED’s XY coordinates and it’s “neural tree” location (tree number and depth, see figure 
below), and stored these in an array. For simple animations like the exploding wave, an LED’s color is calculated based 
on its location and the current timestep. For the neural activity animation, each “tree” is activated at a random time, 
with maximal activation starting at depth 1 and flowing up to depth 5 smoothly. 

But what’s a Michigan cap without a Go Blue? I converted the G O B L U E text into a 20x85 bitmap that scrolls across 
the display. At a single timestep, a 20x20 slice is taken out of the full bitmap. Each LED’s color is determined by 
rounding it’s XY position to the nearest 20x20 grid location, then extracting the 1/0 at the location in the current 
20x20 slice. Iterating slices across the full 85 width shows the full GOBLUE.



<div class="row">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/37 tree depths.png" title="LED tree and depths" class="img-fluid rounded mx-auto d-block" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/gradcap/38 goblue matrix.png" title="data matrix" class="img-fluid rounded mx-auto d-block" %}
    </div>
<div class="row">


I hot-glued the PCB onto the mortarboard with the battery on the underside. I have yet test the battery life, but I 
expect it to give at least an hour of display time. 


The display turned out exactly how I’d pictured it and I hope I can wear it to a ceremony in the future. There are many 
more possibilities for animations, especially since it’s a full-color display (not limited solely to maize and blue). 
I’m now working on making a wooden frame to display it on a wall when not being worn. An additional future project might 
involve placing EEG electrodes inside the cap to display real brain activity with the lights. 
Perhaps that’s a project for my PhD graduation cap. 



