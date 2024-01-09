# 🥳 Release notes

### Firmware version 1.2

**Release date:** \
03 January 2024

* Added function to lock/unlock keys by pressing a certain combination.
* Added separate PLC commands to delay relays, command to reset buffers and FCC outputs.
* Added a new PLC command to delay the ECM fan voltage output.
* Fixed a bug related to the SPI driver responsible for communication between the display and the device.
* Fixed a bug related to the incorrect display of the OCC function on the display when changing applications.
* Fixed valve opening/closing with delay.
* Fixed ECM fan max voltage startup to only work if the fan is off.
* Fixed a bug related to  the switching from the ECM fan speed button.
* Fixed display of fan speeds when switching apps.
* Fixed default setting of ECM fan voltages and frost protection temperatures.

### Firmware version 1.1

**Release date:** \
29 November 2023

* Fixed app switching bug, fan and valve not switching properly.
* Fixed the default value for valve open/close time.
* Fixed a bug related to the fan turns on after the valve on time has expired.

### Firmware version 1.0

**Release date:** \
15 November 2023

* Initial firmware release.
