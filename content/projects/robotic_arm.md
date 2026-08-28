+++
title = "Robotic Arm"
description = "Hardware and software for a 6-DOF desktop robotic arm."
weight = 0

[extra]
local_image = "/images/arm.jpg"
# link_to = "https://github.com/hjkellis/Manipulator-Environment"
+++

# Intro
This project article documents building of a 6-DOF robotic arm (modified version of an [open-source hardware design by tw2ka](https://www.dropbox.com/scl/fi/mgowac0a7bwx7u2pcz12b/Arduino-robot-arm-files-step.zip?rlkey=3cpy6x4wcpfr1s548s7qxxex5&e=2&dl=0) with custom electronics and firmware). Additionally, the hardware files, software packages, and firmware for this project can be found [here](https://github.com/hjkellis/arm-trajectory-controller).

<center>
    <img src="/images/jsp_demo.gif" height="350" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        Arm and Joint State Publisher
    </i>
</center>

# Hardware 
The goal for the hardware side of this project was to reduce price while maintaining as much of the performance of the original design as possible. In order to accomplish this goal, hardware was constrained to consumer/hobbiest level electronics and 3D printed rigid bodies. Most of the control hardware was taken from an old 3D-printer I built in high school, for which I wrote custom firmware to integrate motor controls, serial communication, and position feedback.

## Mechanical
The robotic arm consists of stepper motors, belts, pulleys, and 3D-printed rigid bodies. The first 5 joints (J1 to J5) use bipolar NEMA 17 stepper motors, while the last joint (J6), responsible for rotating the end effector, uses a bipolar NEMA 8 stepper motor. All belts are off-the-shelf GT2 timing belts. Ball and shunt bearings were also used in various sizes to reduce friction between joints.

<center>
<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
    <img src="/images/stepper_feedback_1.png" height="200" style="width: auto;">
    <img src="/images/stepper_feedback_2.png" height="200" style="width: auto;">
</div>
<div style="text-align: center; margin-top: 10px;">
    <i>
        Stepper motors with feedback sensors
    </i>
</div>
</center>

## Electrical


A recycled RAMPS stepper motor board was used to control the stepper motors, with micro-stepping applied for higher resolution. A neodymium magnet was attached to the back of each stepper motor shaft with a AS5600 magnetic encoder to read joint positions. Finally, communication with the ROS2 control package was established via UART over USB.

<center>
<img src="/images/RAMPS.jpeg" height="200" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        RAMPS control board.
    </i>
</center>

Encoder feedback was mostly used to for backdriving the robotic arm. But a simple closed loop control scheme was also added to ensure accurate postion tracking.

{% mermaid() %}
graph LR 
    A(ROS2) --> B(uC)
    B --> C(Motor Drivers)
    C --> D(Stepper Motors)
    D --> E(Encoders)
    E --> B
{% end %}
<center>
    <i>
        Postion feedback system
    </i>
</center>

Closed-loop control of the stepper motors was managed by the custom RAMPS firmware and a simple proportional feedback controller. Luckily, the mechanical design led the steppers to rarely lose steps.


# Software
The ROS2 packages for this project can be found [here](https://github.com/hjkellis/Manipulator-Environment).


<center>
    <img src="/images/robot_arm.png" height="350" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        Kinematic chain visualization (RViz)
    </i>
</center>
