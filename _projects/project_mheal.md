---
layout: page
title: MHEAL Clear Lung Project
description: a low-cost vest to diagnose pneumonia in children
img: assets/img/mheal/clearlunglogo.png
importance: 2
category:
---
December 2019
<br>
### A New Diagnostic Tool for Childhood Pneumonia
Joey Costello and John Obeid

<div class="row">
    <div class="col-5 col-sm-3 mt-3 mt-md-0  mx-auto d-block">
        {% include figure.html path="assets/img/mheal/clearlunglogo.png" title="logo" class="img-fluid" %}
    </div>
</div>

#### Diagnosing Pneumonia in Children
Pneumonia is the largest source of mortality in children in developing countries, accounting for nearly two million 
deaths each year. Since pneumonia is treatable, the problem lies in diagnosis; unrefined diagnostic techniques result 
in the infection going undiagnosed or frequently misdiagnosed as malaria. Our group, the Clear Lung Project, has been 
developing a low-cost, intelligent diagnostic tool to help solve the challenges of diagnosing pneumonia in 
resource-limited areas. 

When fully completed, our diagnostic tool will incorporate a wearable vest to record lung sounds from the patient 
and a viewing screen where the physician can see the result. Upon seeing a patient with a breathing problem, a 
physician or health professional would have the patient wear the system, which would record lung sounds as they 
breathe. After analyzing the recorded sounds, the system would predict if pneumonia is a likely diagnosis and 
suggest seeking more advanced medical expertise for treatment or further diagnostic scans.

When listening to the lungs with a stethoscope, trained physicians typically listen to several locations on the 
patient’s back. Similarly, our system uses multiple microphones positioned across the back to detect localized lung 
sounds including coughs, wheezing, and crackles. This year we completed a prototype recording system and are in the 
process of developing machine learning algorithms to analyze the audio recordings and make a diagnostic prediction.

#### Based on a Raspberry Pi Computer
The full system has two main parts: a vest worn by the patient that records lung sounds, and a main control unit that 
controls recording and displays results. At the core of the system we used a Raspberry Pi computer, which is small, 
inexpensive ($35), and capable of performing all the required processing. After the user starts the system, the Pi 
records audio from four piezo contact microphones, analyzes the audio through a machine-learning algorithm, and 
outputs its diagnosis to the display.

One issue with the Pi is its lack of analog inputs and real-time computing ability; this means an external board is needed 
for recording audio. We first tried using the Arduino-based Teensy board which is inexpensive and can record four 
channels at 48 KHz. However, we ran into consistency issues streaming the data through the I2S interface back to the 
Pi for processing. Luckily, we found a 
[multi-channel audio board built for the Pi](http://www.audioinjector.net/rpi-octo-hat), which can record up to 
six channels. The Pi sees the board as a standard audio interface so any recording software can be used.  

<div class="row align-items-center">
    <div class="col-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/system internals.png" title="system internals" class="img-fluid" %}
    </div>
    <div class="col-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/piezo.png" title="piezo" class="img-fluid" %}
    </div>
</div>


#### Improving Recording Quality
Initially, we connected the piezo microphones directly to the audio board but the recordings were very high-pitched, 
“tinny” sounding. After some research we discovered the problem was an impedance mismatch between the piezo and the 
audio line-in input. As shown in the plot below
(from [this useful blog post](http://www.richardmudhar.com/using-piezo-contact-mics-right/)), the mismatch 
creates a high-pass filter that attenuates low frequencies. Lung sounds like crackles and wheezes have frequencies of 
100-200 Hz making it critical to accurately capture these lower frequencies.

<div class="row">
    <div class="col-5 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/mheal/impedance.png" title="impedance" class="img-fluid" %}
    </div>
</div>


To solve the problem, we designed an amplifier circuit to act as a higher load impedance and reduce the filtering effect
(and amplify the signal slightly). The circuit (below) is based on 
[Richard Mudhar’s piezo amplifier](http://www.richardmudhar.com/piezo-contact-microphone-hi-z-amplifier-low-noise-version/).  

<div class="row">
    <div class="col-7 mt-3 mt-md-0 mx-auto">
        {% include figure.html path="assets/img/mheal/schematic.png" title="schematic" class="img-fluid" %}
    </div>
</div>


We designed a custom PCB with four of these circuits to take in four microphone inputs, and output to the Pi through two
ethernet cables. The board has two additional pins for eventually adding other sensors 
(like breathing rate and pulse-oximetry). Everything was laid out in Eagle and we had the boards printed through 
OSHPark for a few dollars. We then 3D printed a simple case with snap-on lid to protect the board, and the case mounts 
on the back of the patient’s vest.

PCB Front, PCB Back, and assembled PCB with case:
<div class="row d-flex align-items-center">
    <div class="col-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/pcb 1.png" title="pcb" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/pcb 2.png" title="pcb" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/open unit.jpeg" title="schematic" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


#### Vest-Based Recording System
The full system consists of the wearable-vest and control unit. We modified a weight-lifting vest since it already had 
numerous straps and attachment points to hold the microphones and the pre-amplifier board. We designed 3D printed mounts
to hold the microphones and connect to the vest through velcro for adjustability. Two ethernet cables carry the 
analog microphone signals to the main control unit for analysis.


Wearable-vest and control unit:

<div class="row">
    <div class="col-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/vestworn.jpeg" title="vest on person" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mheal/vest and unit.jpeg" title="vest microphones" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


#### Future Work
This year we completed a working prototype with adjustability to allow for testing different microphone positions and 
user sizes. Next, we plan on adding buttons for a user interface as well as other sensors to aid in diagnosis 
(heart rate, breathing rate, pulse oximetry). Our largest challenge going forward will be recording enough example 
lung sounds from patients with and without pneumonia to then train accurate machine-learning algorithms. We hope to 
soon take our system abroad to get doctor and patient feedback to guide further developments.
