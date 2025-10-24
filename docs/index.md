---
title: EGR 304 Embedded Systems Design
tags:
- tag1
- tag2
---
<center>
<font size= "6">Roshan Roy Geoffrey Joe Datasheet</font><br>
as part of<br>
<font size= "8"> ClapSense</font><br>
for<br>
<font size= "5"> Team 204 </font><br>

**Submission: December 01, 2025**
</center>

## Introduction

This page documents the Sensor Front-End Driver Subsystem developed by Roshan as part of Team 204’s EGR 304 project. The purpose of this subsystem is to receive control signals from the master hub, process light level information, and drive an external lamp output. This GitHub page provides a clear overview of the subsystem architecture, chosen components, power and signal interfaces, and the role this hardware plays in the larger team system.

### Project Summary

ClapSense is a light that is activated on and off by clapping. This idea was developed to provide an easier way to control your lights, especially for older people, while maintaining the comfort of your house. The clap light is also equipped with manual switches for power and a setting to dim the lights to your preference.

The Sensor Front-End Board is responsible for translating digital control signals from the Master Controller into physical lamp actuation, while also integrating a light sensor to monitor ambient light conditions. This subsystem receives a lamp toggle command from the hub through an 8-pin connector, uses an LM358 non-inverting op amp to amplify the signal from a TEMT6000 light sensor, and provides real-time feedback via an LED output.

Attached here is the link to our [team report.](https://asu-egr304-2025-f-204.github.io/)


### My Contribution

My contribution focuses on designing and implementing the Sensor Front-End subsystem, which includes:

    * Selecting and integrating a TEMT6000 light sensor and an LM358 non-inverting op amp circuit to provide an amplified analog signal to the microcontroller’s ADC.

    * Configuring PWM and DAC outputs on the PIC18F57Q43 to control a red LED for visual feedback and a MOSFET or relay driver to actuate the lamp.

    * Implementing signal mapping between the hub and my board, including UART RX and a digital input line for lamp toggle control.

    * Ensuring clean and labeled power distribution (+5 V regulated) and proper grounding shared with the team boards.

This subsystem plays a key role in turning control signals into real-world actuation, ensuring reliable lamp operation under different environmental conditions.

To review the details listed of the material used to construct the subsection, you can review it in the ["BOM"](https://roshanroy-r64x.github.io/03-BOM/BOM/) section of the datasheet.
