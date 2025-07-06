+++
title = "Smooth Cartesian Path Planning"
date = "2025-07-06"

[taxonomies]
# tags=["linux"]

[extra]
# repo_view = true
# comment = true
+++

# Motivation
Originally, when writing the firmware for my robotic arm I avoided the difficulties of trying to achieve smooth cartesian movements all together, opting instead for succesive position commands to be sent over serial - leading to lots of jitter. This jitter was fine for my research at the time as most of my results were done in simulation anyway, and my trajectories were simple. However, now that I am using the robotic arm for purely personal use, I find that that the smooth real-time cartesian motion is extremely desireable.

# How to achieve smooth linear motions?
In order to achieve smooth motion I moved away from ```AccelStepper``` library - which only offers position control. Instead I wrote my own firmware to control the velocities of the motor joints over time. This is the solution I came up with to solve this problem:

{% mermaid() %}
graph LR 
    subgraph Host
        A(ROS2) --> B(MoveIt!)
    end
    B --> D(Joint Trajectories)
    D --> E(Ring Buffer)
    subgraph Robot
        E --> F(Joint Velocities)
        subgraph Joint Buffers
            F --> G(Step Buffer)
        end
        G --> M(Timer ISR)
        M --> N(Step Motors)
    end
    style Host fill:#ddd,stroke:#333
    style Robot fill:#ddd,stroke:#333
    %% style C fill:#6f6,stroke:#333
    %% style G fill:#6f6,stroke:#333
{% end %}

Time parameterized joint trajectory angles are calculated using the ```MoveIt!``` IK solver which are then sent over serial to a ring buffer which are then converted into steps, these steps are then executed by the ISR to achieve the smooth, continuous, cartesian path-planning.

# Code

// TODO: add code

# Results

// TODO: add video

The packages I wrote to control my arm can be found [here](https://github.com/hunterwellis/Arm-Trajectory-Controller).
