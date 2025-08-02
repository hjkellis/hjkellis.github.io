+++
title = "Keyboard Build"
date = "2025-07-31"

[taxonomies]
# tags=["documentation"]

[extra]
# repo_view = true
# comment = true
+++

3D-Printed and handwired a Bastard Keyboards [Scylla](https://github.com/Bastardkb/Scylla).

Here is a list of materials I used:

- 58 $\times$ 1N4148 Flyback Diodes
- 58 $\times$ Gateron Brown Switches
- 2 $\times$ Pro Micro Dev Boards
- 2 $\times$ Female Aux Connectors
- 2 $\times$ Female Aux Connectors
- 3D Printer Filament

# 3D Printed Case
The print took ~12 hours total (6 hours for each side) on a BambuLabs A1 mini.

<center>
    <img src="/images/kb_print.jpg" height="350" width=auto style="margin-left: auto; margin-right: auto; display: block;">
    <i>
        3D printed case, still on the print-plate.
    </i>
</center>

# Wiring
I hand soldered each board, this ended being the most labourious part of this project as each side of the keyboard has 29 keys. Additionally, with 3 solder joints (2 wires and a diode) per key, 30 connections to the microcontroller, and 3 connections to the AUX jack, this worked out to $2 \times 29 + 2 \times 5 \times 6 + 2 \times 6 = 124$ solder joints in total. I also had to cut and strip each wire to fit properly into the case.

<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
    <img src="/images/kb_keycaps.jpg" height="350" style="width: auto;">
    <img src="/images/kb_wiring.jpg" height="350" style="width: auto;">
</div>
<div style="text-align: center; margin-top: 10px;">
    <i>Keyboard wiring (minus the &mu;C)</i>
</div>


# Firmware & Keymaps
For the firmware I used QMK, an "open-source keyboard firmware for Atmel AVR and Arm USB families". I had to write my own hardware configuration files to match with my microcontroller and wiring. The documentation for QMK and made things super easy.

For keymaps I have 4 layers, one for typing, the second and third for symbols, arrow keys, and function keys, and the last is a special layer that is triggered when both layer keys are pressed that accesses some system features.

All layers have a transparent thumb cluster.

## Base Layer
For my base layer I am just using a standard QWERTY.

<small>
<small>
<pre>
<code>
.-----------------------------------------.                                  .-----------------------------------------.
| Esc  |   1  |   2  |   3  |   4  |   5  |                                  |   6  |   7  |   8  |   9  |   0  |  Bsp |
|------+------+------+------+------+------|                                  |------+------+------+------+------+------|
| Tab  |   Q  |   W  |   E  |   R  |   T  |                                  |   Y  |   U  |   I  |   O  |   P  |  \   |
|------+------+------+------+------+------|                                  |------+------+------+------+------+------|
| Del  |   A  |   S  |   D  |   F  |   G  |                                  |   H  |   J  |   K  |   L  |   ;  |  '   |
|------+------+------+------+------+------|                                  |------+------+------+------+------+------|
| Shft |   Z  |   X  |   C  |   V  |   B  |                                  |   N  |   M  |   ,  |   .  |   /  | Shft |
'-----------------------------------------/                                  \-----------------------------------------'
                                  / LOWER /---------------.    .---------------\ RAISE \
                                 /       / Enter /  Del  /      \  Bsp  \ Space \       \
                                '-------/       /       /        \       \       \-------'
                                       /---------------/          \---------------\
                                      /  Alt  / Ctrl  /            \  Ctrl \  Alt  \
                                     /       /       /              \       \       \
                                    '---------------'                '---------------'
</code>
</pre>
</small>
</small>

## Upper Layer
The upper layer contains symbols and function keys

<small>
<small>
<pre>
<code>
 .-----------------------------------------.                                  .-----------------------------------------.
 |      |  F1  |  F2  |  F3  |  F4  |  F5  |                                  |  F6  |  F7  |  F8  |  F9  |  F10 |  F11 |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |   [  |   ]  |      |                                  |   $  |   /  |  *   |  #   |   ~  |  F12 |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |  Ins |  !   |  @   |   (  |   )  |      |                                  |   %  |   -  |  +   |  =   |  ?   |      |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |   {  |   }  |      |                                  |   ^  |   &  |  |   |      |      |      |
 '-----------------------------------------/                                  \-----------------------------------------'
                                  /       /---------------.    .---------------\       \
                                 /       /       /       /      \       \       \       \
                                '-------/       /       /        \       \       \-------'
                                       /---------------/          \---------------\
                                      /       /       /            \       \       \
                                     /       /       /              \       \       \
                                    '---------------'                '---------------'
</code>
</pre>
</small>
</small>



## Lower Layer
The lower layer just contains arrow keys.

<small>
<small>
<pre>
<code>
 .-----------------------------------------.                                  .-----------------------------------------.
 |      |  F1  |  F2  |  F3  |  F4  |  F5  |                                  |  F6  |  F7  |  F8  |  F9  |  F10 |  F11 |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |   [  |   ]  |  +   |                                  |      |      |      |      |      |  F12 |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |  Ins |  !   |  @   |   (  |   )  |  -   |                                  |      | left | down |  up  | rght |      |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |   {  |   }  |  =   |                                  |      |      |      |      |      |      |
 '-----------------------------------------/                                  \-----------------------------------------'
                                  /       /---------------.    .---------------\       \
                                 /       /       /       /      \       \       \       \
                                '-------/       /       /        \       \       \-------'
                                       /---------------/          \---------------\
                                      /       /       /            \       \       \
                                     /       /       /              \       \       \
                                    '---------------'                '---------------'
</code>
</pre>
</small>
</small>

## System Layer
Finally, there is a final layer that is triggered when both layer keys are pressed simultaniously that allows me to control the mouse and other system features.

<small>
<small>
<pre>
<code>
 .-----------------------------------------.                                  .-----------------------------------------.
 | BASE |      |      |      |      | BASE |                                  | BASE |      |      |      |      | BASE |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |      |      |  V+  |                                  |  B + |      |      |      |      |      |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |      |      |  V-  |                                  |  B - | ms_l | ms_d | ms_u | ms_r |      |
 |------+------+------+------+------+------|                                  |------+------+------+------+------+------|
 |      |      |      |      |      | Mute |                                  |      |      |      |      |      |      |
 '-----------------------------------------/                                  \-----------------------------------------'
                                  /       /---------------.    .---------------\       \
                                 /       /       /       /      \       \       \       \
                                '-------/       /       /        \       \       \-------'
                                       /---------------/          \---------------\
                                      /       /       /            \       \       \
                                     /       /       /              \       \       \
                                    '---------------'                '---------------'
</code>
</pre>
</small>
</small>

# Finished Product
This is the final product, with keycaps installed!

