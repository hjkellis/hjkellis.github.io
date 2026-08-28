+++
title = "Solving Cart Pole with a PID Controller"
date = "2025-07-10"

[taxonomies]
# tags=["documentation"]

[extra]
# repo_view = true
# comment = true
+++

This is my solution to the classic Cart-Pole problem, using a simple PID controller implemented in python and Gymnasium.

# Proportional-Derivative Control
For balancing the pole a simple PD controller was sufficient. In my implementation, I approximated the derivative error with a Tustin transform.

PD Controller:
$$u(t)=K_p\cdot e(t)+K_d\cdot\frac{de(t)}{dt}$$
discrete approximation,
$$\Rightarrow u[n]\approx K_p\cdot e[n]+2K_d\cdot\frac{e[n]-e[n-1]}{T_s}$$

# Integral Control
For integral control, I used a backwards euler approximation - where $K_i\int^{t}_{0}{e(\tau)d\tau}$ is the integral term:

$$K_i\int^{t}_{0}{e(\tau)d\tau}\approx K_i T_s\sum^{n}\_{k=1}{e[k]}$$

To deal with memory constraints, a ring buffer was used to capture the integral over a fixed range.

# Code
Here is the very simple code snippet of my controller logic. $T_s$ and other constants are aggregated into the controller gains and `prev_errs` is a ring buffer.
```python
err = -obs[2]  # pole angle
err_d = err - prev_errs[0]
err_i = Ts * sum(prev_errs)

ctrl_sig = Kp * err + Ki * err_i + Kd * err_d

action = 1 if ctrl_sig < 0 else 0  # discretize the output
```

# Result
This simple application of PID yields a decently stable output, but I still need to do some parameter tuning especially on the integral term.

<center>
    <img src="/images/cartpole.gif" height="350" width=auto >
</center>
