---
title: Resources
---

# Resources

## Microcontroller Code

## Overall Team System

This firmware runs on the PIC18F57Q43 Curiosity Nano and coordinates all three subsystems to control the ClapSense Hub. It reads Aaron's clap detector on RA0 to toggle the hub on and off, checks Quinn's light sensor on RA1 so the motor only runs when the sensor is covered, and processes Roshan's distance sensor signal from RA3 to generate a smooth LED brightness response.

A three state motor controller manages OFF, START, and RUN behavior based on clap events, while a distance based brightness table maps ADC readings into six intensity levels that transition gradually using a simple weighted average filter. The main loop and timer interrupts work together to update the motor, LED, and UART logging every 50 ms, creating a responsive and stable embedded system that combines all three sensor inputs into one integrated behavior.

### Downloads

- [Team Subsystem Hardware Functionality project ZIP](https://github.com/roshanroy-r64x/roshanroy-r64x.github.io/blob/main/docs/08-Resources/Team.zip)

## Individual Subsystem

This program implements the individual Distance and Signal Conditioning subsystem that Roshan designed. The PIC18F57Q43 reads the analog output of the GP2Y0A21YK0F distance sensor through the MCP6002 op amp on RA0, converts the value with the ADC, and maps the result to a PWM duty cycle that drives a status LED. As an object moves closer or farther from the sensor, the LED brightness changes smoothly, giving a clear visual indication of measured distance.

To make the readings reliable, the code averages multiple ADC samples and applies simple filtering to reduce noise from the sensor. Calibration constants and scaling factors convert raw counts into usable brightness levels, and the firmware continuously updates the LED inside the main loop using a timer based refresh so that the output does not flicker. This demonstrates a complete embedded signal chain from analog sensing through conditioning, conversion, and real time visual feedback.

### Downloads

- [Individual Distance Subsystem Hardware Functionality project ZIP](https://github.com/roshanroy-r64x/roshanroy-r64x.github.io/blob/main/docs/08-Resources/Distance%20Sensor%20Front%20End.zip)
