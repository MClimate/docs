# 🥳 Release notes

### Firmware version 1.6

**Release date:** \
06 December 2024

* NEW - radio command to remotely power cycle the device - [A5](network-related-settings-and-others.md#reset-device).
* Fixed an issue related to temperature measurement and readings.

### Firmware version 1.5

**Release date:** \
07 June 2024

* Changed reset button hold time from 10 seconds to 5 seconds.

### Firmware version 1.4

**Release date:** \
08 April 2024

* [New command to set target temperature with 0.1°C resolution.](target-temperature-and-temperature-range.md#target-temperature-with-resolution-0.1-c)
* Changed target temperature function to display temperature with 0.1°C resolution.
* [New commands to set a target temperature step.](target-temperature-and-temperature-range.md#target-temperature-range)
* [New functionality and commands for temperature control with temperature hysteresis.](target-temperature-and-temperature-range.md#temperature-hysteresis)
* [New functionality and commands for temperature sensor compensation.](target-temperature-and-temperature-range.md#measured-temperature-sensor-compensation)
* Changed start byte of keep-alive packet from 01 to 81 and added another byte to collect target temperature with 0.1°C resolution.

### Firmware version 1.3

**Release date:** \
15 November 2023

* Added the voltage thresholds start-up mechanism.
* Further improvements of the display communication.&#x20;
* Correct the conditions of the set target temperature command.

### Firmware version 1.2

**Release date:** \
28 June 2023

* Further improvements of the PIR sensor.

### Firmware version 1.1

**Release date:** \
26 April 2023

* Improvements of the PIR sensor
  * The PIR sensor powers off when the radio/display are active.&#x20;
  * The default blind period of the PIR sensor has been changed to 10min.

### Firmware version 1.0

**Release date:** \
13 April 2023

* Initial firmware release
