---
description: Find release notes for firmware of HT LoRaWAN
---

# 🥳 Release notes

### Firmware version 2.2

**Release date:**\
21 Mar 2024

* If there is an invalid humidity value both temperature and humidity are still reported.

### Firmware version 2.1

**Release date:**\
5 Feb 2024

* SHTC3 H\&T sensor is now supported.
* Handle properly invalid humidity values got by HDC2010 and don't discard the temperature value in such cases.
* Radio command to get the LoRaWAN region implemented.

### Firmware version 2.0

**Release date:**\
2 February 2023

* FUOTA mechanism released

{% hint style="info" %}
The FUOTA functionality differs from the FUOTA that's being used by the LoRa Alliance. In order to update the firmware version of devices, they should be connected to MClimate's cloud. It takes around 1500 downlinks to perform FUOTA. Due to duty-cycle limitations of the gateways, we recommend staging the FUOTA in smaller batches in case your installation is sizeable.

Feel free to reach out to [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to acquire more details on the process.
{% endhint %}

* Join-retry period changed to 10m.
  * Removed logic for device restart after 5 unsuccessful joins.
* Devices now send full configuration information with the first uplink after the Join procedure.
* Bugfix: Watch-dog period for unconfirmed uplinks now correctly updating after changing the keepalive period.

### Firmware version 1.7

**Release date:**\
9 Feb 2023

* Decrease the H\&T sensor operating temperature range to -20 to 60 Celsius and reset the sensor in case temperature outside that range is read.

### Firmware version 1.6

**Release date:**\
23 May 2022

* Improvements on testing logic (production level).

### Firmware version 1.5

**Release date:**\
25 Nov 2021

* Introduction of RTC time based measurement.
* Improvements on the T\&H measurement logic.
* Device mode check LED indication changed..
* HDC2010 sensor support.

### Firmware version 1.4

**Release date:**\
25 Aug 2021

* Start next temp. measurement after radio Tx done event.
* Periodic battery level measurement.
* RGB LED test indication at power-up added.
