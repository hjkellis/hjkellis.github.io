+++
title = "Smart Mirror"
description = "Repurposed hardware and custom software to create a home automation interface."
weight = 1

[extra]
local_image = "/images/mirror_fin.png"
# link_to = "https://github.com/hunterwellis/Manipulator-Environment"
+++

I modified a Lululemon workout mirror so that I could use a Raspberry Pi to display a custom dashboard through the mirrors display.

# Hardware
Lululemon stopped producing these mirrors and they require users to pay for a subscription to use the mirror for its inteded purpose. As a result I was able to snag one of these second had for \\$150 (they originally sold for \\$1500!). The hardware on these mirrors is great, especially compared to many of the DIY smart mirrors floating around the internet.

<center>
    <img src="/images/mirror.jpg" height="350" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        Internals of the Mirror<br>(it is just a LCD and a two way mirror)
    </i>
</center>

I only made slight modifcations to the internals of the mirror to get it to work how I wanted, this included replacing the display driver and SBC that came with the mirror with a matching display driver I found on ebay and a Raspberry Pi 3 - Model B that I had sitting around since highschool. After that it was just a matter of some cable management to route power to the RPI and the hardware was all finished.

<center>
    <img src="/images/mirror_kb.jpg" height="350" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        RPI Desktop Displayed on Mirror
    </i>
</center>

From there I accesssed the Pi via SSH and had my way with this machine.

# Software
[Github Repo](https://github.com/hunterwellis/Iris)
<!-- I wrote the UI for the mirror in Qt and it integrates some basic widgets for time, weather, spotify, habit tracking, etc. I plan to eventually make this the frontend for a minimalist home automation system I have been working on called _Iris_ that integrates natural language processing with some basic home automation tasks. -->

<center>
    <img src="/images/mirror_fin.png" height="350" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        Mirror displaying weather and time.
    </i>
</center>

