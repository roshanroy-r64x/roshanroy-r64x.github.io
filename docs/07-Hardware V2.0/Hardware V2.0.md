---
title: Hardware 2.0
---

# Hardware V2.0

## Distance/Signal Conditioning Subsystem Version 2.0 Discussion

If I were to create a Version 2.0 of my Distance/Signal Conditioning subsystem, there are several improvements I would make now that I have built the first version, tested it, and integrated it with the rest of the project. The current design performs all of its required functions: it accepts a 9 V input through the barrel jack and fuse, regulates it down to 5 V using the LM7805, powers the GP2Y0A21YK0F distance sensor, conditions the analog output through the MCP6002 op-amp, and sends the processed signal into the PIC18F57Q43. The board also includes a PWM-driven status LED, debouncing components, and labeled connectors for communication. Functionally the system works, but now that the schematic has been translated into a physical PCB, it is much easier to see which areas could be refined for Version 2.0.

The first improvement I would target is the power stage. Right now the subsystem uses a linear LM7805 regulator to drop 9 V down to 5 V. With multiple components powered from that rail — the sensor, the op-amp, and the microcontroller subsystem — the regulator must dissipate the voltage difference as heat. In the schematic, this entire path flows through the barrel jack, fuse, input capacitor network, and finally into the LM7805 before the 5 V rail branches out to the rest of the design. While this works, a switching regulator would be a far better option in Version 2.0. It would introduce significantly less power loss, keep the board cooler, and improve overall efficiency, especially during long operation where the sensor and amplifier are continuously active.

Another improvement relates to the signal conditioning stage. The MCP6002 op-amp performs well for buffering and scaling the distance sensor output, but the current design is very simple — a single non-inverting gain stage with fixed resistors. After building and testing the system, I realized that having adjustability would be extremely useful. In Version 2.0, I would add either a small multi-turn potentiometer or a jumper-selectable gain configuration. That would allow calibration of the sensor range, compensation for part-to-part variance, and finer control over what analog voltage range maps into the PIC’s ADC. This makes the subsystem more flexible and robust.

I would also revise the way the board handles noise and filtering. The GP2Y0A21YK0F is known for producing noisy analog outputs, and while the current design includes decoupling capacitors and a simple RC network, testing revealed that the output still fluctuates more than ideal. In a second version, I would introduce a more deliberate low-pass filter ahead of the op-amp or apply a two-stage amplifier design with dedicated filtering. This would produce a cleaner ADC signal, reduce jitter, and improve measurement stability.

Another category of improvement is testability and debugging, which became very noticeable once the board was physically assembled. The Version 1 design has only a few test points, and many nets such as the sensor output, op-amp output, and 5 V rail can only be accessed by probing component pins directly. In Version 2.0, I would add clearly labeled test pads for:

* the raw sensor output

* the amplified signal going into RA0

* the 5 V regulated rail

* the 9 V input

* op-amp supply pins

ground reference
These additions would make troubleshooting significantly easier and reduce the risk of accidental shorts when using oscilloscope probes.

Another meaningful change would be improving the robustness of the sensor interface. The GP2Y0A21YK0F is sensitive to electrical noise and supply fluctuations. In Version 2.0, I would include additional supply filtering near the sensor connector and possibly ESD protection on the output pin. This would make the system more resistant to transient spikes and improve long-term reliability.

Finally, I would reconsider how much of the design depends on the external Curiosity Nano microcontroller board. While the Nano makes development simple, integrating the PIC18F57Q43 directly onto the PCB in Version 2.0 would have several advantages: reduced wiring complexity, cleaner routing, lower cost, and a more professional design overall. The schematic already shows the necessary connections for power, ADC, and debugging; extending this to include the PIC and minimal support components would be a natural progression.

Overall, the Version 1 subsystem works well and has been a great learning experience, but Version 2.0 would focus on increasing efficiency, signal quality, debugging capability, and design maturity. Replacing the linear regulator with a switching regulator, adding adjustable gain or additional filtering in the amplifier stage, improving test point access, strengthening sensor protection, and eventually integrating the PIC directly onto the board would all produce a more polished, reliable, and scalable subsystem. These enhancements would make the design far more capable in real-world environments and elevate it from a functional prototype to a refined hardware module.



Attached is the code used to verify functionality of the individual subsystem in .zip format, [*here*](https://github.com/roshanroy-r64x/roshanroy-r64x.github.io/blob/main/docs/07-Microcontroller-Code/Distance%20Sensor%20Front%20End.zip).