+++
title = "One Year using Linux"
date = "2025-06-06"

[taxonomies]
# tags=["linux"]

[extra]
# repo_view = true
# comment = true
+++

It's hard to believe that one year ago I was a Windows' user. Especially, considering the hard time I give my friends for using Windows nowadays.

# Making the Switch
Initially, I switched to Linux to work on my Master's thesis in robotics, which required ROS2 (which is most compatible with Ubuntu). Now, I could have easily used Docker or some other platform to virtualize my problems away, but I had taken an [Intro to Unix](https://ece.vt.edu/undergrad/courses/2524.html) course at my university with some friends and was pretty fed-up with the headaches of using Windows. As such I gave up any chance of having a healthy relationship with technology and I entered the rabbit-hole.

<center>
    <img src="/images/ubuntu_noble_numbat.png" height="350" width=auto >
</center>

Luckily for me I made the decision to switch during the summer and the Company I was an intern for lent me a Windows laptop, so I had a decently large margin of time to deal wth the learning curves that come with installing Linux on bare-metal.

# Things Just Work!?
Upon switching I immediately noticed that _things just work_ on Linux. If I needed to install an application, a framework, or a tool the package manager was there to save the day. (No more dealing with MinGW, GCC comes preinstalled.) Maybe it sounds strange to say that "_things just work_"--I mean that is how it is supposed to bej after all, but coming from Windows where it feels like youre OS is constantly battling you this was huge. 

I remember just trying to install Qt5 on Windows was a headache, navigating convoluted GUIs, setting Window's environment PATH, restarting my computer, and constanly validating Windows that: "yes, I am absolutely sure I want to do this". On the other hand on Linux this was as easy as: ```apt install qt5-default```.

<center>
    <img src="/images/limitless.gif" height="350" width=auto >
</center>
<center>
    <i>
        How it feels writing a <code>Hello World!</code> program in Vim.
    </i>
</center>

Of course this power comes with responsibilty. Within the first week while trying to ```rm``` a directory I ran ```sudo rm -r ./*``` from the wrong directory and ended up deleting all of my unbacked-up configuration files.

# Configuration and Workflow

Since, switching to Linux I have adopted a number of different technologies and configurations that have been amazing for my productivity and streamlining my workflow. However, maybe more important than increasing productivity, these optimizations just made the process of working from my computer more enjoyable. 

<center>
    <img src="/images/linux_rice.png" height="350" width=auto >
</center>
<center>
    <i>
        My current Linux desktop environment and neovim.
    </i>
</center>


I set up a custom configurations for polybar, i3, jgmenu, etc. that make my desktop environment feel super smooth, and allow me to not even have a mouse on my desk. Additionally, I recently jumped off the deepend and started using Vim as my main text-editor which has made my workflow feel even more clean. Now, when I ```ssh``` into a server I work pretty much the same as if I were on my own setup.

<br>
<br>
<br>
<br>
