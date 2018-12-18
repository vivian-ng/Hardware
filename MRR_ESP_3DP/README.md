# MRR ESP 3DP
# 3D printer control board based on ESP32

This is a bare-minimum 3D printer control board based on the ESP32 microcontroller, which comes with built-in WiFi and BlueTooth.

** Work in progress! Do not attempt production using this schematic! **</br>
** Current version: v0.6 **

Features:
- Able to use up to 4 stepper drivers: X, Y, Z, and E0
- 12V or 24V input power supply
- Separate power supply for the heat bed
- X, Y, and Z min endstops
- Allows the use of a Z-axis probe, such as an inductive sensor, running on the input supply voltage (12V or 24V)
- AUX1 connector for use with an external host, such as the closed-source MKS TFT32
- A jumper for selecting Vout (either 3.3V or 5V)
- A jumper for selecting the source for 5V (either from the input power supply, or from USB)
- Add support for TMC2130 and TMC2208 drivers which can be enabled by configuring jumpers
  - Set MS1, MS2, MS3 jumpers to SPI, RST jumper to TMC, and TMC_SEL jumper to SPI to enable TMC2130 SPI mode
  - Set RST jumper to TMC and TMC_SEL jumper to UART to enable TMC2208 UART mode
  - For TMC2130 SPI mode, connect corresponding motor (X, Y, Z, or E0) on CS_PIN header to available ESP32 pin


Released under CERN Open Hardware Licence v1.2. See LICENSE.txt for details.
