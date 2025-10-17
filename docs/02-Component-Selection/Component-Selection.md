---
title: Component Selection
---

## Voltage Regulator Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](LM7805.png)<br> TI LM7805CT/NOPB<br>$0.75/each<br>[Link to product](https://www.digikey.at/en/products/detail/texas-instruments/LM7805CT-NOPB/3901929?srsltid=AfmBOopTMflYUGFDdDmnUsD8TNz4yrmp66EBxTwRtfcOCVvsSaKWJ1qR)                 | \* Easy to heatsink<br>\* Compatible with PSoC<br>\* Up to 1–1.5 A                                               | \* Higher dropout (~2 V); can run hot → bigger thermal budget<br>|
| ![](MCP1825S.png)<br> Microchip MCP1825S-5002E/DB <br> $0.70/each <br> [Link to product](https://www.digikey.com/en/products/detail/microchip-technology/MCP1825S-5002E-DB/1636099?) | \* 500 mA LDO <br>\* lower dropout than 7805 <br> \* compact SOT-223 package | * SMD reflow/soldering skill needed <br>\* less tolerant of big thermal loads                                                         |
| ![](AMS1117.png)<br> AMS1117-5.0<br>$0.13/each<br>[Link to product](https://www.digikey.com/en/products/detail/evvo/AMS1117-5-0/24370130?)                 | \* 1 A rating<br>\* Compact<br>                                               | \* Moderate dropout (~1.1–1.3 V) <br>\* Current higher than some LDOs <br>\* Dip in quality|

**Choice:** MCP1825S-5002

**Rationale:** Meets the project’s 500 mA requirement with lower dropout than a 7805, reducing heat when input headroom is small; SOT-223 footprint keeps the PCB compact while still manageable to solder. Price and availability are also solid.

## Op-Amp Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](LM358.png)<br> TI LM358<br>$0.50/each<br>[Link to product](https://www.digikey.com/en/product-highlight/t/texas-instruments/lm358-dual-operational-amplifiers?)                 | \* Dual amp; single-supply 5 V operation<br>\* Tolerant of inputs near ground| \* Not rail-to-rail in/out<br>\* Input bias & offset higher than modern CMOS parts|
| ![](MCP6002.png)<br> MCP6002-E/P <br> $0.60/each <br> [Link to product](https://www.digikey.com/en/products/detail/microchip-technology/MCP6002-E-P/683196?) | \* Rail-to-rail I/O <br>\* Great at 5 V or 3.3 V <br> \* Good for sensor buffering | * Lower GBW (1 MHz) may limit high-speed filtering                                                         |
| ![](TLV2372IDR.png)<br> TLV2372IDR<br>$1.45/each<br>[Link to product](https://www.digikey.com/en/products/detail/texas-instruments/TLV2372IDR/381216?)                 | \* Rail-to-rail<br>\* 3 MHz GBW; more headroom<br>\* low power per channel                                               | \* Higher cost <br>\* SOIC/T&R variants may require SMD rework skills|

**Choice:** MCP6002

**Rationale:** For an ambient-light signal into the PIC’s ADC, rail-to-rail I/O, low power, and clean operation at 5 V are more valuable than bandwidth. MCP6002 gives simpler headroom management than LM358 with minimal cost increase.

## Light Sensor Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](TEMT6000x01.png)<br> TEMT6000X01<br>$0.90/each<br>[Link to product](https://www.mouser.com/ProductDetail/Vishay-Semiconductors/TEMT6000X01?qs=%2Fjqivxn91ccZGXDwz0wGxg%3D%3D&srsltid=AfmBOooQdB74AbB3cmws8rrGCeFrnCZulZ_kDPwcyoM4WwAIF_F-DG09)                 | \* Simple analog output<br>\* Fast response and tiny footprint <br>\* Works directly with op-amp/ADC| \* Output is non-linear vs. lux<br>\* Requires biasing and calibration <br>\* Sensitive to angle/spectrum|
| ![](BH1750FvI.png)<br> BH1750FVI <br> $4.00/each <br> [Link to product](https://www.sunrom.com/p/digital-light-sensor-bh1750fvi?) | \* Reports lux directly via I²C <br>\* Minimal analog design | * Requires I²C + library <br>\* Fixed spectrum/transfer function <br>\* Module size > bare sensor                                                         |
| ![](VEML7700.png)<br> Adafruit VEML7700 Lux Sensor - I2C Light Sensor - STEMMA QT / Qwiic<br>$5.00/each<br>[Link to product](https://www.adafruit.com/product/4162?srsltid=AfmBOorBHSPB9NFLJcU5ez7-J4arau8XeTmrqw6rngzxuV2-He8xyOAv)                 | \* Wide 0–120 klux, 16-bit <br>\* adjustable gain/integration <br>\* 3.3/5 V friendly and accurate lux output                                               | \* I²C interface required|

**Choice:** TEMT6000

**Rationale:** Since there is already an ADC channel, TEMT6000 keeps BOM cost and firmware complexity low while providing fast analog response. If calibrated, it’s sufficient for relative brightness feedback to the LED driver.
