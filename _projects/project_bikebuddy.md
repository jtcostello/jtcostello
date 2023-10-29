---
layout: page
title: Bike Buddy
description: an app to alert for help during bike adventures
img: assets/img/bikebuddy/BikeBuddyLogo.png
importance: 3
category:
---
June 2020

<div class="row">
    <div class="col-5 col-sm-5 mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/bikebuddy/bikebuddy_screenshot.png" title="example image" class="img-fluid rounded" %}
    </div>
</div>


In 2020 I was doing a lot of biking in the Santa Monica Mountains, where I was often out of cell service and away from
people. I made BikeBuddy as a way to alert my family if I didn't return home by a certain time. The app lets the user
set an "emergency" time, and if the user doesn't return home by that time, the app sends an SMS to the an emergency contact.
A backend server sends the SMS, so the user doesn't need to be in cell service for the alert to be sent. Once the user
returns home the alert is automatically cancelled.

I used Google Firebase as a backend server since it has easy integration into Android apps, is free, and can schedule
tasks with simple javascript functions. Whenever a user adds a ride on the app, Firebase schedules an SMS alert at the 
"emergency" time. Once a minute, the server check if an SMS needs to be sent. If the user 
safely returns home, the app cancels the alert in the database. Also, the app updates the "last known position" location in the database
which also gets sent in the emergency SMS.

Luckily I've never had a real emergency, but it's nice to have the safety net in place.

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/bikebuddy/DSC_0358.JPG" title="example image" class="img-fluid rounded" %}
    </div>

    <div class="col-sm-6 mt-3 mt-md-0 mx-auto d-block">
        {% include figure.html path="assets/img/bikebuddy/BikeBuddyLogo.png" title="example image" class="img-fluid rounded" %}
    </div>
</div>






