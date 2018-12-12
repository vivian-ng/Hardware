# MRR STM32F4 3DPshield
# 3D printer shield for use with STM32F407VET6 development boards

This is a 3D printer shield for STM32F407VET6 development boards. The design is in the fashion of RAMPS shields available for ATMEGA2560 boards.

** Work in progress! Do not attempt production using this schematic! **

Features:
- Able to use up to 5 stepper drivers: X, Y, Z, E0 and E1
- 12V or 24V input power supply
- Separate power supply for the heat bed
- X, Y, and Z min endstops
- Allows the use of a Z-axis probe, such as an inductive sensor, running on the input supply voltage (12V or 24V)
- AUX1 connector for use with an external host, such as the closed-source MKS TFT32
- A jumper for selecting the source for 5V (either from the input power supply, or from USB)

Released under CERN Open Hardware Licence v1.2. See LICENSE.txt for details.
