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

This page documents the Distance Front-End Subsystem developed by Roshan as part of Team 204’s EGR 304 project. The purpose of this subsystem is to measure the proximity of a movable slider using a distance sensor and use that data to control the brightness of an LED. This GitHub page provides an overview of the subsystem’s hardware architecture, selected components, signal and power interfacing, and how this board integrates into the overall ClapSense system.

### Project Summary

ClapSense is an interactive lighting system that allows users to turn lights on and off with a clap. The system is designed to provide simple and intuitive control—especially useful for users seeking convenient lighting adjustments without physical switches. Additionally, it allows manual dimming and brightness adjustment.

The Distance Front-End Board is responsible for detecting the position of a slider relative to a distance sensor and translating that input into a variable brightness output. The subsystem uses a Sharp GP2Y0A21YK0F analog distance sensor to measure distance, feeding its signal through an MCP6002 op amp before reaching the PIC18F57Q43 Curiosity Nano’s ADC. The microcontroller then uses this analog value to adjust the LED brightness via PWM output.

When the slider moves closer to the distance sensor, the LED dims through the corresponding potentiometer adjustment. Conversely, when the slider moves away from the distance sensor, the LED brightens, demonstrating a dynamic feedback system controlled by physical distance.

Attached here is the link to our [team report.](https://asu-egr304-2025-f-204.github.io/)


### My Contribution

My contribution focuses on designing and implementing the Distance Front-End subsystem, which includes:

* Integrating the Sharp GP2Y0A21YK0F analog IR distance sensor and buffering its output with an MCP6002 op amp for stable ADC readings.
* Configuring the PIC18F57Q43 peripherals—using ADC for sensor input and PWM for LED brightness control based on distance.
* Implementing a dynamic brightness system where moving a slider closer to the distance sensor dims the LED, and moving it away brightens the LED through the potentiometer interface.
* Ensuring proper power management using a LM7805 regulator to provide a stable 5 V supply shared across the sensor, op amp, and microcontroller.
* Establishing clean signal mapping across boards through an 8-pin connector, maintaining consistent labeling and power distribution between subsystems.

This subsystem provides the real-time analog interface between physical user interaction and visible system output, playing a key role in connecting sensory input to light control.

To review the details listed of the material used to construct the subsection, you can review it in the [BOM](https://roshanroy-r64x.github.io/03-BOM/BOM/) section of the datasheet.
