---
title: Power Budget (Roshan Roy Geoffrey Joe)
---

## Overview

This subsystem is powered from an external 9 V DC wall adapter, which feeds the LM7805 linear regulator to provide a stable +5 V rail for all circuitry. The updated schematic includes the PIC18F57Q43 Curiosity Nano microcontroller board, the GP2Y0A21YK0F distance sensor, the MCP6002 low-power dual op-amp configured as a non-inverting amplifier, a status LED driven by PWM, and a small bias network used for signal conditioning. All of these components draw power exclusively from the +5 V rail. Based on datasheet values and measured expectations, the total operating load on the +5 V rail is 93 mA. Applying a standard 25 percent safety margin increases the required current capacity to 116.25 mA. The LM7805 regulator can supply up to 500 mA, leaving more than 380 mA of available headroom for reliable operation. This ensures that the subsystem remains well within the regulator’s limits while maintaining stable performance across all expected operating conditions.

![Power Budget](PowerBudget.png)

The power budget as a PDF download is available [*here*](PowerBudgetRoshan.pdf), and a Microsoft Excel Sheet [*here*](PowerBudgetRoshan.xlsx).

## Power Budget Analysis and Conclusions

To estimate the power needs of my subsystem, I created a power budget by listing all major active components—the PIC18F57Q43 Curiosity Nano, the GP2Y0A21YK0F distance sensor, the MCP6002 op-amp, the PWM status LED, and the bias network—and documenting their expected current draw from datasheets or typical operating values. Summing these loads produced a subtotal of 93 mA on the regulated 5 V rail, and applying a 25 percent safety margin increased the required capacity to 116.25 mA. Comparing this requirement to the LM7805 regulator’s 500 mA capability confirmed that the subsystem has more than enough available headroom for safe operation. The analysis also highlighted that because the LM7805 is a linear regulator dropping 9 V to 5 V, it must dissipate excess power as heat, especially during extended use. Although the current design meets all power requirements comfortably, the power budget process led to the conclusion that a switching regulator would be a more efficient and thermally stable choice for a Version 2.0 redesign.