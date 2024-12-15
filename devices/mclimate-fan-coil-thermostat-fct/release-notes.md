# 🥳 Release notes

### Firmware version 1.8 <a href="#firmware-version-1.6" id="firmware-version-1.6"></a>

**Release date:** \
15 December 2024

* NEW - radio command to remotely power cycle the device - [A5](mclimate-fan-coil-thermostat-device-communication-protocol/reset-device.md).
* NEW - radio command to select [UI language](mclimate-fan-coil-thermostat-device-communication-protocol/general-display-and-power-recovery/user-interface-language.md).
* In this firmware version, the [target temperature range](on-off-and-target-temperature/min-max-setpoint-adjustment.md#set-get-target-temperature-range) radio command has been returned.
* Fixed an issue related to temperature measurement and readings.

### Firmware version 1.6

**Release date:** \
06 September 2024&#x20;

* Added French UI.
* Added additional fan modes.
* The Fan now runs for X minutes (adjustable setting) on LOW speed after the setpoint temperature has been reached in order to coo off the heating element (safety feture).
* Changed default target temperature min/max values ​​from 0-40C to 5-30C.
* When the device is in unoccupied mode, the target temperature and fan speed can be set using the buttons and the radio commands.
* Added min/max temperature range occupied/unoccupied.
* Added payload info when the change-over happens.
* Added different min/max temperature depending on the mode.
* Fixed bug related to incorrect operation of frost protection at negative measured temperature.
* Fixed bug related to application 2 and 3 being incorrectly displayed as 2 - pipe system instead of 4 - pipe in the application menu (installer menu) of the devices.
* Fixed bug related to wrong reporting of manually changed target temperature when changed by buttons and up to 10 sec changed by radio command.
* Fixed bug: When the device is in ventilation mode and a radio command is sent to set the target temperature, this temperature is shown on the device display.
* Fixed bug: When two radio commands are sent to the device before the "Duty cycle" time expires, the device only responds to the last one.

### Firmware version 1.5

**Release date:** \
19 April 2024

* Added improvements for AS923 radio region.

### Firmware version 1.4

**Release date:** \
04 March 2024

* Settings changed with the buttons now have a 5 second delay (to avoid rapid switching when cycling through fan speeds for example).
* Removed the black bar at the bottom of the display when the device is turned off.
* Тhe default temperature compensation value of the measured temperature has been changed from 0°C to -1.4°C.
* А bug related to sending the first radio packet has been fixed.
* Fixed "GET fan speed" command to return correct values for a 3-speed fan.

### Firmware version 1.3

**Release date:** \
19 January 2024

* Added app menu key unlock feature.
* Added functionality to select an app with buttons from the app menu.

### Firmware version 1.2

**Release date:** \
03 January 2024

* Added function to lock/unlock keys by pressing a certain combination.
* Added functionality for [Automatic Temperature control mode with external temperature reading](external-temperature-measurement.md#id-1.-automatic-temperature-control-mode-with-external-temperature-reading).
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
