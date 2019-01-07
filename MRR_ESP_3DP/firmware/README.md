This directory contains ZIP files of firmware which works with the MRR ESP 3DP board.

MRR ESP 3DP board works with the [Marlin fork](https://github.com/luc-github/Marlin) currently under development by [Luc](https://github.com/luc-github). This fork provides WiFi support as well as a web UI based on Luc's [ESP3D](https://github.com/luc-github/ESP3D). Snapshots of the repo will be posted here. You can download the ZIP file, unpack it, and edit the Configuration.h and Configuration_adv.h to suit the size of your printer, drivers, etc. If you are using TMC2130 drivers in SPI mode, you will also need to edit pins_ESP32.h to specify the CS pins for the drivers. The fork has been tested to compile under Arduino IDE 1.8.5 using Arduino-ESP32 core v1.0.0 (stable release).

If you are using an external host such as the MKS TFT32 or Octoprint, you can also use Marlin 2.0, which has ESP32 support. However, this does not come with WiFi nor a web UI.

When flashing firmware, use a baud rate of 115200.

# Instructions for setting up WiFi

Once the firmware has been flashed for the first time, there is a need to do an initial setup for the WiFi settings.<br>
In Arduino IDE, open up the terminal to connect to the board. Then, type in the following commands 1 to 3 to set up the board in station mode (connect to an existing WiFi router). To set up in AP mode, use commands 1, 4, and 5.

1. `M586 P0 S1 R80`<br>
Enable HTTP on port 80.<br>
Replace `R80` with `Rxx` (xx is the port number) to run the HTTP server on another port.

2. `M587 S"abcd" P"12345" I192.168.0.25`<br>
WiFi settings; the above will connect to a SSID of `abcd` with password `12345` and attempt to use a static address of `192.168.0.25` (note: the quotation marks are necessary for SSID and password). Change `abcd`, `12345`, and `192.168.0.25` to your own values. `I192.168.0.25` can be left out if a static address is not needed.

3. `M588 S1 P1`<br>
This will start up WiFi in station mode, using the settings set by `M587`. The IP address of the webserver will be displayed in the terminal. Use this IP address to connect to the webserver. For example, going to `http://192.168.0.25:80/` on your web browser following the above example.

4. `M589 S"ESP32" P"12345" I192.168.10.1`<br>
WiFi settings; the above will create an access point with SSID of `ESP32` and password `12345`, and the webserver will be on IP address `192.168.10.1` (note: the quotation marks are necessary for SSID and password). WPA2 security will be used by default.

5. `M588 S2 P1`<br>
This will start up WiFi in AP mode, using the settings set by `M589`.

For more about the web UI, see Luc's [ESP3D-WEBUI](https://github.com/luc-github/ESP3D-WEBUI) repository.
