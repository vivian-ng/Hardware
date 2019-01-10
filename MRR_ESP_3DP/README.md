# MRR ESP 3DP
## 3D printer control board based on ESP32

This is a bare-minimum 3D printer control board based on the ESP32 microcontroller, which comes with built-in WiFi and BlueTooth.

** Work in progress! Do not attempt production using this schematic! **<br>
** Current version: v0.6 **<br>
** Warning: There is a design problem with v0.6. The 5V output from the LM2596-5 may exceed 5.5V due to the inductor being used having a current rating much lower than required. A supply voltage of more than 5.5V is beyond the operating range of the 74HCT02. This will cause the 74HCT02 to break down, sending current to the MOSFETs. **

Features:
- Able to use up to 4 stepper drivers: X, Y, Z, and E0
- 12V to 24V input power supply
- Separate power supply for the heat bed
- X, Y, and Z min endstops (v0.6 and earlier: no filters; v0.7 onwards will add a capacitor as a filter; please use endstops, such as the ones designed by Makerbot, that has their own debouncing circuits)
- Allows the use of a Z-axis probe, such as an inductive sensor, running on the input supply voltage (12V or 24V)
- AUX1 connector for use with an external host, such as the closed-source MKS TFT32
- A jumper for selecting Vout (either 3.3V or 5V)
- A jumper for selecting the source for 5V (either from the input power supply, or from USB)
- Add support for TMC2130 and TMC2208 drivers which can be enabled by configuring jumpers (**Untested!!!**)
  - Set MS1, MS2, MS3 jumpers to SPI, RST jumper to TMC, and TMC_SEL jumper to SPI to enable TMC2130 SPI mode
  - Set RST jumper to TMC, enable PD_UART (TX, RX) jumpers, and TMC_SEL jumper to UART to enable TMC2208 UART mode (Note: Jumpers for TMC2208 UART mode will be removed in v0.7 as there are not enough pins to support at least 2 drivers (X and Y))
  - For TMC2130 SPI mode, connect corresponding motor (X, Y, Z, or E0) on CS_PIN header to available ESP32 pin
- Physical size of 99mm by 99mm. Mounting holes are 3.5mm in diameter, with centers 3.75mm from the edges.
- "BOOT" button can be used to reset the board.

# Selection Jumpers

There are jumpers for:
- 5V_SEL: Selection of input power to use. Either from external power supply (PWR), or from USB. Set the jumper to USB when connecting to a computer for flashing firmware.
- Vout_SEL: Set the Vout pins voltage to either 5V or 3.3V.
- TMC_SEL: When using TMC drivers (TMC2130 or TMC2208). Set to SPI when using TMC2130 in SPI mode, or UART when using TMC2208 in UART mode.
- PD_UART: These two jumpers (TX, RX) must be enabled when using TMC2208 in UART mode. (to be removed in v0.7)
- MS1, MS2, MS3: Enable/disable these jumpers for microstepping. When using TMC2130 in SPI mode, enable the other side (SPI) of the jumper.
- RST/TMC: Enable RST side when not using SPI or UART modes with TMC drivers. Enable TMC side when using TMC2130 in SPI mode or TMC2208 in UART mode (UART to be removed in v0.7).

## TMC2130 in SPI mode

- Set the motor jumpers to SPI instead of MS1/MS2/MS3, and to TMC instead of RST.
- Set "TMC_SEL" jumper to TMC.
- Connect the respective "CS_PIN" (X, Y, Z, E) to the pin you want to use for CS of that motor. You will need to use a female-to-female jumper cable.

## TMC2208 in UART mode (to be removed in v0.7)

- Set motor jumper to TMC instead of RST. MS1/MS2 can be used for microstepping.
- Set "TMC_SEL" jumper to UART.
- Enable "PD_UART" (TX, RX) jumpers.

# Firmware

Marlin 2.0 has added support for ESP32. This board was based on the initial pins definition used. <br>
In addition, [Luc](https://github.com/luc-github) has been working on a Marlin fork which incorporates part of his ESP3D webUI into Marlin itself.

## Flashing firmware

- You should be able to flash firmware through the USB port. Depending on your operating system, you may need to install drivers for the CH340. Please use Google or another search engine to find the right CH340 driver for your operating system.
- To flash firmware by directly connecting to TX/RX pins, you will need to connect IO0 and IO2 to GND, then reboot (press "BOOT" button) to enter flash mode. After flashing the firmware, disconnect IO0 and IO2 from GND, and press "BOOT" button again to reboot into normal mode.
- Use a baud rate of 115200.

# Pins

To be added

# License
Released under CERN Open Hardware Licence v1.2. See LICENSE.txt for details.
