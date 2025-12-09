---
title: Component Selection
---

## Voltage Regulator Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](LM7805.png)<br> TI LM7805CT/NOPB<br>$0.75/each<br>[Link to product](https://www.digikey.at/en/products/detail/texas-instruments/LM7805CT-NOPB/3901929?srsltid=AfmBOopTMflYUGFDdDmnUsD8TNz4yrmp66EBxTwRtfcOCVvsSaKWJ1qR)                 | \* Easy to heatsink<br>\* Compatible with PSoC<br>\* Up to 1–1.5 A                                               | \* Higher dropout (~2 V); can run hot → bigger thermal budget<br>|
| ![](MCP1825S.png)<br> Microchip MCP1825S-5002E/DB <br> $0.70/each <br> [Link to product](https://www.digikey.com/en/products/detail/microchip-technology/MCP1825S-5002E-DB/1636099?) | \* 500 mA LDO <br>\* lower dropout than 7805 <br> \* compact SOT-223 package | * SMD reflow/soldering skill needed <br>\* less tolerant of big thermal loads                                                         |
| ![](AMS1117.png)<br> AMS1117-5.0<br>$0.13/each<br>[Link to product](https://www.digikey.com/en/products/detail/evvo/AMS1117-5-0/24370130?)                 | \* 1 A rating<br>\* Compact<br>                                               | \* Moderate dropout (~1.1–1.3 V) <br>\* Current higher than some LDOs <br>\* Dip in quality|

**Choice:** LM7805CT/NOPB

**Rationale:** Meets the project’s 500 mA requirement and compatible with the PSoC. Same voltage regulator as the rest of the group so consistency maintained as well.

## Op-Amp Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](LM358.png)<br> TI LM358<br>$0.50/each<br>[Link to product](https://www.digikey.com/en/product-highlight/t/texas-instruments/lm358-dual-operational-amplifiers?)                 | \* Dual amp; single-supply 5 V operation<br>\* Tolerant of inputs near ground| \* Not rail-to-rail in/out<br>\* Input bias & offset higher than modern CMOS parts|
| ![](MCP6002.png)<br> MCP6002-E/P <br> $0.60/each <br> [Link to product](https://www.digikey.com/en/products/detail/microchip-technology/MCP6002-E-P/683196?) | \* Rail-to-rail I/O <br>\* Great at 5 V or 3.3 V <br> \* Good for sensor buffering | * Lower GBW (1 MHz) may limit high-speed filtering                                                         |
| ![](TLV2372IDR.png)<br> TLV2372IDR<br>$1.45/each<br>[Link to product](https://www.digikey.com/en/products/detail/texas-instruments/TLV2372IDR/381216?)                 | \* Rail-to-rail<br>\* 3 MHz GBW; more headroom<br>\* low power per channel                                               | \* Higher cost <br>\* SOIC/T&R variants may require SMD rework skills|

**Choice:** MCP6002

**Rationale:** For an ambient-light signal into the PIC’s ADC, rail-to-rail I/O, low power, and clean operation at 5 V are more valuable than bandwidth. MCP6002 gives simpler headroom management than LM358 with minimal cost increase.

## Distance Sensor Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](GP2Y0A21YK0F.png)<br>GP2Y0A21YK0F<br>$12.41/each<br>[Link to product](https://www.mouser.com/ProductDetail/Sharp-Microelectronics/GP2Y0A21YK0F?qs=5S%2F4hkdqNNcI0gpWLEuQ8w%3D%3D&srsltid=AfmBOor6tRQwArriCsBX9USd7xWGLUOvLn5iKQPQR_6T8RsckpvSWZ2-)                 | \* 10–80 cm analog IR distance sensing <br>\* 5 V supply compatible with system rail<br>\* Simple 3-wire hookup (Vcc, Out, GND)| \* Non-linear analog output curve<br>\* Accuracy ±10% typical<br>\* Sensitive to color/surface reflectivity|
| ![](HC-SR04.png)<br> HC-SR04 Ultrasonic Module<br> $5.25/each <br> [Link to product](https://www.sparkfun.com/ultrasonic-distance-sensor-hc-sr04.html) | \* 2 – 400 cm range<br>\* Low  cost and 5 volts<br>\* Easy firmware via trigger/echo timing | * Requires two I/O pins<br>\* Unreliable on soft/angled targets<br>\* Bulkier than IR sensor                                                         |
| ![](VL53L1X.png)<br> Adafruit VL53L1X Time of Flight Distance Sensor - ~30 to 4000mm - STEMMA QT / Qwiic<br>$14.95/each<br>[Link to product](https://www.adafruit.com/product/3967)                 | \* 4 m max range<br>\* High precision and narrow field of view<br>\* I²C digital output with built-in filtering                                               | \* Needs 3.3 V rail + level shifting<br>\* More complex firmware (I²C driver)|

**Choice:** Sharp GP2Y0A21YK0F

**Rationale:** Operates directly from the 5 V rail and outputs an analog voltage enough for the PIC ADC, eliminating extra signal-conditioning hardware. It covers the intended 10–80 cm detection zone with low power draw and minimal code overhead, ideal for quick integration into the Distance Front End.

## Final Component Summary

| **Component Category**           | **Component Name**         | **Part Number**    | **Description / Purpose**                                                                 |
| -------------------------------- | -------------------------- | ------------------ | ----------------------------------------------------------------------------------------- |
| **Microcontroller**              | PIC18F57Q43 Curiosity Nano | DM182029           | Reads amplified distance sensor signal (RA0), drives PWM LED, provides subsystem control. |
| **Distance Sensor**              | Sharp IR Distance Sensor   | GP2Y0A21YK0F       | Outputs analog voltage proportional to distance (10–80 cm range).                         |
| **Op-Amp (Signal Conditioning)** | Dual Op-Amp                | MCP6002            | Conditions and amplifies the sensor output before feeding the PIC ADC.                    |
| **Voltage Regulator**            | 5 V Linear Regulator       | LM7805             | Converts 9 V barrel jack input to regulated 5 V for the subsystem.                        |
| **Indicator Output**             | Red Status LED (PWM)       | Broadcom HLMP-4700 | Visual distance indicator driven by PWM from PIC.                                         |

## Pinout

| **Location** | **Pin Name** | **Module** | **Function**                                  | **Direction** | **Custom Name** | **Analog** |
| ------------ | ------------ | ---------- | --------------------------------------------- | ------------- | --------------- | ---------- |
| **21**       | RA0          | ADCC       | ANx (ADC Input)                               | input         | IO_RA0          | Yes         |
| **22**       | RA1          | Pins       | GPIO (LED PWM Output)                         | output        | IO_RA1          | No          |
| **23**       | RA2          | DAC1       | DAC1OUTx (Optional analog output / debugging) | output        | IO_RA2          | Yes         |
