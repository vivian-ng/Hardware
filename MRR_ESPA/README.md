# MRR ESP 3DP
## 3D printer control board based on ESP32

This is a bare-minimum 3D printer control board based on the ESP32 microcontroller, which comes with built-in WiFi and BlueTooth.

**Work in progress! Do not attempt production using this schematic!**<br>
**Current version: v0.7**<br>
Note: v0.8 will be migrated to KiCad so that the files can be more accessible to everyone who wishes to modify them.<br>

Features:
- Able to use up to 4 stepper drivers: X, Y, Z, and E0
- 12V to 24V input power supply
- Separate power supply for the heat bed
- X, Y, and Z min endstops (v0.6 and earlier: no filters; v0.7 onwards added a capacitor as a filter; please use endstops, such as the ones designed by Makerbot, that have their own debouncing circuits)
- Allows the use of a Z-axis probe, such as an inductive sensor, running on the input supply voltage (12V to 24V)
- AUX1 connector for use with an external host, such as the closed-source MKS TFT32
- A jumper for selecting Vout (either 3.3V or 5V) (to be removed in v0.8)
- Automatic selection of 5V source from either power supply or USB
- Supports TMC2130 drivers in SPI mode which can be enabled by configuring jumpers (**Untested!!!**)
  - Set MS1, MS2, MS3 jumpers to SPI, RST jumper to TMC, and TMC_SEL jumper to SPI to enable TMC2130 SPI mode
  - For TMC2130 SPI mode, connect corresponding motor (X, Y, Z, or E0) on CS_PIN header to available ESP32 pin
- Physical size of 99mm by 99mm. Mounting holes are 3.5mm in diameter, with centers 3.75mm from the edges.
- "BOOT" button can be used to reset the board.

# Selection Jumpers

There are jumpers for:
- Vout_SEL: Set the Vout pins voltage to either 5V or 3.3V. (to be removed in v0.8)
- MS1, MS2, MS3: Enable/disable these jumpers for microstepping. When using TMC2130 in SPI mode, enable the other side (SPI) of the jumper.
- RST/TMC: Enable RST side when not using SPI mode with TMC drivers. Enable TMC side when using TMC2130 in SPI mode.
- MOS_EN: Leave jumper open to disable any outputs to MOSFETs. (to be removed in v0.8)

## TMC2130 in SPI mode

- Set the motor jumpers to SPI instead of MS1/MS2/MS3, and to TMC instead of RST.
- Connect the respective "CS_PIN" (X, Y, Z, E) to the pin you want to use for CS of that motor. You will need to use a female-to-female jumper cable. Currently, unused pins are SDA, SCL, and IO0, which allows for up to three TMC2130 drivers to be used in SPI mode.

# Firmware

Marlin 2.0 has added support for ESP32. This board was based on the initial pins definition used. <br>
In addition, [Luc](https://github.com/luc-github) has been working on a Marlin fork which incorporates part of his ESP3D webUI into Marlin itself.

## Flashing firmware

- You should be able to flash firmware through the USB port. Depending on your operating system, you may need to install drivers for the CH340. Please use Google or another search engine to find the right CH340 driver for your operating system.
- To flash firmware by directly connecting to TX/RX pins, you will need to connect IO0 to GND, then reboot (press "BOOT" button) to enter flash mode. After flashing the firmware, disconnect IO0 from GND, and press "BOOT" button again to reboot into normal mode.
- Use a baud rate of 115200.

# Pins

To be added

# License
Released under CERN Open Hardware Licence v1.2. See LICENSE.txt for details.

## Warning

- This product uses high currents which may cause fires. Use with caution.
- Do not use input voltages higher than 24V. Input current must not exceed 15A.
- Do not attempt to use more than 15A for the heated bed. While the MOSFET is capable of such currents, the connectors are not. If you need more than 15A, use an external MOSFET.
- Do not attempt to use more than 5A for the hot end. While the MOSFET is capable of such currents, the connectors are not. If you need more than 5A, use an external MOSFET.
- Do not reverse polarity.
- The breakout and endstop pins are rated for 3.3V, which is the voltage the ESP32 operates at. Attempting to feed inputs above 3.3V to these pins may damage the board.
- It is recommended to power the board only via USB (i.e. turn off PSU power supply) when flashing the board.
- Use the same PSU to power both VIN and VBED; the GND rail on the board is common to board VIN and VBED, and using different PSUs for these power inputs (with different ground levels) may have dangerous effects.

## Disclaimer

This product is provided as-is. While care has been taken to design a safe product, it is the user's responsibility to make sure precautions are taken to prevent damage or injury when using this product. This includes adhering to all warnings provided. By using this product, the user accepts responsibility to bear all liabilities from any damage or injury arising from the use of this product.
