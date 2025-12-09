---
title: Power Budget (Roshan Roy Geoffrey Joe)
---

## Overview

This subsystem is powered from an external 9 V DC wall adapter, which feeds the LM7805 linear regulator to provide a stable +5 V rail for all circuitry. The updated schematic includes the PIC18F57Q43 Curiosity Nano microcontroller board, the GP2Y0A21YK0F distance sensor, the MCP6002 low-power dual op-amp configured as a non-inverting amplifier, a status LED driven by PWM, and a small bias network used for signal conditioning. All of these components draw power exclusively from the +5 V rail. Based on datasheet values and measured expectations, the total operating load on the +5 V rail is 93 mA. Applying a standard 25 percent safety margin increases the required current capacity to 116.25 mA. The LM7805 regulator can supply up to 500 mA, leaving more than 380 mA of available headroom for reliable operation. This ensures that the subsystem remains well within the regulator’s limits while maintaining stable performance across all expected operating conditions.

![Power Budget](PowerBudget.png)

## Resouces

The power budget as a PDF download is available [*here*](PowerBudgetRoshan.pdf), and a Microsoft Excel Sheet [*here*](PowerBudgetRoshan.xlsx).