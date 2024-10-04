# 🥳 Release notes

### Firmware version 1.6

**Release date:** \
02 September 2024

* **FUOTA** functionality added;
* Bits 5 and 6 at long keep-alive message byte 1 (manual valve open/close indicators) was swapped, fixed now
* Device now exchange radio data in the common way used at all other company devices: accepts one or more get commands in a downlink and appends multiple command responses in uplink. Get command is appended always to long keep-alive command and never to short keep-alive.
* Device sends multiple get commands appended to the 1st uplink.
* Device now can operate with both unconfirmed and confirmed uplinks. By default unconfirmed are used. Since some device events still require confirmation from the server (flood or fraud detection), it has to deal with that. Otherwise long keep-alive message with the related reason will be invoked up to 8 times by the device.

### Firmware version 1.5

**Release date:** \
11 May 2021

* Bug fixed at LoRaWAN MAC Layer

### Firmware version 1.4

**Release date:** \
20 April 2021

* Add a command for device deactivation (0x0B)
* Improve the button press detection logic to handle more than one pressed button at a time

### Firmware version 1.3

**Release date:** \
1 Jan 2021

* Introduction of new, better optimized firmware libraries
* DevEUI, AppEUI, AppKey are not configurable via UART

### Firmware version 1.2

**Release date:** \
31 July 2020

* Bug fix related to power consumption.

### Firmware version 1.1

**Release date:** \
22 July 2020

* Initial firmware release
