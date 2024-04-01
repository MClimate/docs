---
description: Find release notes for firmware of HT LoRaWAN
---

# 🥳 Release notes

### Firmware version 2.4

**Release date:**\
12 Mar 2024

* Stop resetting the device when not joined the LoRaWAN network for 5 attempts.
* Increase default network join period from 3 minutes to 10 minutes.
* Bug fixed regarding conf. uplinks watch-dog period, when keep-alive period changed.
* Decrease the H\&T sensor operating temperature range to 0-60 Celsius.
* Command to read the H\&T sensor model implemented.
* ABC related parameters are retained on LoRaWAN watch-dog reset.
* Improve CO2 sensor error handling, no auto-zero correction on error.
* SHTC3 H\&T sensor is now supported.
* 1st auto-zeroing is now the standard 8 days period.
* Put the measured CO2 value in the range \[400ppm:5000ppm] when needed.
* Command to set CO2 boundary levels (0x1E) now accepts as high values as 5000ppm. Was 2000ppm.
* Command to read the LoRaWAN MAC region implemented.

### Firmware version 2.3

**Release date:**\
28 Sep 2022

* Bug fix of internal sensor communication over UART

### Firmware version 2.2

**Release date:**\
18 Jul 2022

* Support for both Cozir and Sense air Sunshine CO2 sensor modules.
* Devices now sends most important configuration information with the 1st uplink after the Join procedure.
* Now the MCU is sleeping during the LED commands execution.
* FUOTA functionality added.

{% hint style="info" %}
The FUOTA functionality differs from the FUOTA that's being used by the LoRa Alliance. In order to update the firmware version of devices, they should be connected to MClimate's cloud. It takes around 1500 downlinks to perform FUOTA. Due to duty-cycle limitations of the gateways, we recommend staging the FUOTA in smaller batches in case your installation is sizeable.

Feel free to reach out to [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to acquire more details on the process.
{% endhint %}

### Firmware version 1.3

**Release date:**\
13 Dec 2021

* RGB LED test indication at power-up added.
* Device auto-detects and works with HDC1010/HDC2010 H\&T sensors.
* Fix the initial notification periods values. Turn off the buzzer notifications by default.
* 1st CO2 auto-zeroing done after 2 hours instead of 12 hours.
* Cozir sensor digital filter now is set internally at initiation, instead of setting it with LoRaWAN command.
* Reset the device when not joined the LoRaWAN network for 5 attempts.

### Firmware version 1.2

**Release date:**\
21 Jul 2021

* Bug fixes in internal EEPROM.
