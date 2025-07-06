+++
title = "Demo"
date = "2025-05-28"

[taxonomies]
# tags=["documentation"]

[extra]
# repo_view = true
# comment = true
+++

# What is this?
This project includes:
- ROS2 digital twin for visualization of the UR3e arm.
- Qt dashboard for monitoring robot telemetry data.
- Instrumentation integration example.

# Digital Twin

Here I built a quick software-based digital twin of a Universal Robots UR3e robotic arm for detecting errors, collecting hardware data, and remote monitoring. This twin visualizes the robot's real-time joint positions, servo torques, tool center point (TCP), and any other sensor feedback--providing a live, interactive model of what the robot is doing at any moment in the lab. I wrote this in Python and C++.

<img src="/images/ur3e.png" height="400" width=auto style="float: left; margin-left: 175; margin-right: auto; display: block;">
<img src="/images/ur3e_robotiq.png" height="400" width=auto style="float: right; margin-left: auto; margin-right: 150; display: block;">
<div style="clear: both;"></div>
<center>
    <i>Digital Twin</i>
</center>

This digital twin system can integrate into a larger laboratory twin providing fault detection, data collection, and remote monitoring for the whole laboratory. 

A headless Gazebo Harmonic sim was set up to simulate the motor joint torques.

<center>
    <img src="/images/gazebo.png" height="400" width=auto alt="ur3e rviz">
    <br>
    <i>Gazebo Sim</i>
</center>


## Visualization
Visualization of the digital twin is handled in RViz, this integrates nicely with ROS2. Through the Qt GUI users can toggle between the real position given via real telemetry data from the lab and the simulated/projected trajectory.

<center>
    <img src="/images/ur3e_rviz.png" height="400" width=auto alt="ur3e rviz">
    <br>
    <i>UR3e + Robotiq Gripper (RViz)</i>
</center>

## Qt Dashboard
The planned trajectory and telemetry data is displayed in real-time for monitoring. Error values are also computed and error margins can easily be defined and detected. The Qt Dashboard also allows the user to toggle between visualization of the planned and actual trajectory along with a dropdown menu to select the parameter they would like to monitor. Data is timestamped and stored in a CSV file for post-processing and logging.

Of course, I can only simulate the telemetry data here.
<center>
    <img src="/images/dashboard.png" alt="ur3e dashboard">
    <br>
    <i>UR3e Qt dashboard (left) with RViz (right)</i>
</center>


# Sensor Integration
It is necessary for an autonomous laboratory to incorporate many sensors to ensure accurate estimation of the lab's state.

{% mermaid() %}
graph LR 
    %% Analog Subgraph
    subgraph Analog
        A(Sensor) --> B(Signal<br>Conditioning)
        B --> C(Low-pass filter)
    end
    %% Digital Subgraph
    subgraph Digital
        C --> D(ADC)
        D --> E(Digital Filter)
        E --> F(Processed Data)
        C --> G(Raw Data)
    end
    style Digital fill:#ddd,stroke:#333
    style Analog fill:#ddd,stroke:#333
    style F fill:#6f6,stroke:#333
    style G fill:#6f6,stroke:#333
{% end %}

<center>
    <i>Typical signal processing pipeline</i>
</center>

Here I designed the analog and digital circuitry necessary to read from a photodiode. While photodiodes are probably not relevant to the work being done now I imagine they will be when measuring electromagnetic waves is necessary, additionally they require a more complex analog filtering stage compared many other sensors which would be good to demonstrate my skills in both analog and digital electronics.

## Analog Stage

Here is the analog stage I designed to amplify the current signal and attenuate signal aliasing. These schematics were captured in KiCAD and validated in SPICE simulations.

### Signal Conditioning
<img src="/images/TIA_param.png" alt="TIA" height="400" width=auto style="float: right; margin-left: 5">

Using a transimpedence amplifier to amplify the signal and turn it into a voltage signal. This can be defined with the following transfer function.

$$\frac{V_{out}(s)}{I_{ph}(s)} = \frac{-R_f}{1+sR_fC_f}$$
$$\Rightarrow H(s) = 1 + \frac{300k}{4.7k (1 + s * 300k * 27p)}$$
<div style="clear: both;"></div>
<i style="float: right">Direct Form II Block Diagram (Second Order)</i>

### Anti-Aliasing
Here is Sallen-Key low-pass filter at a cutoff of ~15kHz that functions as the last stage before discretizing the signal via the ADC.
<center>
    <img src="/images/AA_filter.png" alt="TIA" height="400" width=auto>
</center>
$$f_c = \frac{1}{2\pi R_5C_5R_6C_6} \approx 14.5k$$

Both of these circuits were validated in a SPICE simulation.

## Digital Stage
### IIR Filter
After sampling from the ADC, the digital stage consists of a direct form II implementation of a lowpass IIR Butterworth filter designed in MATLAB and implemented in C.

<center>
    <img src="/images/dfII.png" alt="Direct Form II Block Diagram" style="background-color:white">
    <br>
    <i>Direct Form II Block Diagram (Second Order)</i>
</center>

This development from DF I reduces memory usage and can be written as,

$$\omega(n) = x(n)-a_1\omega(n-1)-a_2\omega(n-2)-...$$
$$y(n) = b_0\omega(n)-b_1\omega(n-1)-b_2\omega(n-2)-...$$

where $\omega$ is the intermediate states.

Here is the implementation of a generalized IIR filter in C:

```C
float iir_filter(float x, float *a, float *b, float *w, int *index) {
    float w_new = x;

    // state
    for (int i = 1; i < FILTER_ORDER; ++i) {
        int idx = (*index - i + FILTER_ORDER) % FILTER_ORDER;
        w_new -= a[i] * w[idx];
    }

    // output
    float y = b[0] * w_new;
    for (int i = 1; i < FILTER_ORDER; ++i) {
        int idx = (*index - i + FILTER_ORDER) % FILTER_ORDER;
        y += b[i] * w[idx];
    }

    // update state
    w[*index] = w_new;

    // update ring buffer
    *index++
    if (*index >= FILTER_ORDER){
        *index = 0;
    }

    return y;
}
```

<!-- # Custom Desgined End-Effector -->

# Stepper Motors

I should also note that stepper motors can be easily integrated to the digital twin. For stepper position tracking a neodymium magnet can be attached to the motor shaft and the position value measured via a magnetic encoder.

<img src="/images/encoder_mount.png" height="400" width=auto style="float: left; margin-left: auto; margin-right: auto; display: block;">
<img src="/images/magnet_stepper.png" height="400" width=auto style="float: right; margin-left: auto; margin-right: auto; display: block;">
<div style="clear: both;"></div>

<center>
    <i>3D printed encoder mount and neodymium magnet attachment.</i>
</center>
