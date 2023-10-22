---
layout: page
title: Myo Arm
description: a low-cost, 3D printed prosthetic arm controlled by EMG
img: assets/img/myoarm/armoverview.jpg
importance: 3
category:
---
December 2021

<div class="row">
    <div class="col-sm mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/myoarm/armoverview_wide.jpg" title="3d printed arm" class="img-fluid rounded" %}
    </div>
</div>

For my embedded systems class, my team developed a low-cost, 3D-printed prosthetic hand controlled by EMG. Traditional 
prosthetics can cost upwards of $20k, and we aimed to develop a open-source alternative for <$100. Unlike other prosthetics,
our final prosthetic can also be used as a mouse/keyboard for a computer.

We used a Myo armband to record 8-channels of EMG data and transmit the data over bluetooth to an ESP32 
microcontroller. The microcontroller processes the signals, and controls the hand using 2 servos or can act as 
a mouse/keybaord for a computer. The user can switch between "hand" and "computer" modes with a button.

I specifically developed the machine learning training and real-time control software for the project
([code here](https://github.com/jtcostello/arm_controller)).
I made a python app that guides the user through collecting training data with 5 different hand gestures, and then trains an LDA
classifier. The classifier weights are exported to C code that runs on the ESP32 in real time. I also implemented the
training code on the microcontroller so that the user can train the classifier without needing a computer. To let the user
type characters, I created a tertiary morse code where the user uses flex/extend/fist gestures to select letters.



<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/myoarm/systemdiagram.jpg" title="system overview" class="img-fluid rounded" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/myoarm/diagram2.jpg" title="system overview" class="img-fluid rounded" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/myoarm/diagram1.jpg" title="system overview" class="img-fluid rounded" %}
    </div>
</div>
