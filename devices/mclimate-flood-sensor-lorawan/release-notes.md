# 🥳 Release notes

### Firmware version 1.5

**Release date:**\
18 May 2023

* Now the most important device's settings are sent together with the first uplink.
* Added a bit to the [keepalive](flood-sensor-lorawan-communication-protocol/keep-alive.md) to indicate when the measured temperature is negative.
* Added command to [get keepalive period](flood-sensor-lorawan-communication-protocol/keep-alive.md#keepalive-period).
* Added command to GET the [Acoustic and LED alarm duration](flood-sensor-lorawan-communication-protocol/flood-event-available-configurations.md#acoustic-and-led-alarm-duration).
* Added commands to SET and GET the [radio watch dog configurations](flood-sensor-lorawan-communication-protocol/network-related-settings.md#communication-watch-dog).
* Added commands to SET and GET the [radio join-retry period](flood-sensor-lorawan-communication-protocol/network-related-settings.md#join-retry-period).
* Added commands to SET and GET the [device periodic uplink message type](flood-sensor-lorawan-communication-protocol/uplink-types.md#device-uplink-messages-type-command-explanation).
* Added commands to SET and GET the [Flood event uplink messages type](flood-sensor-lorawan-communication-protocol/flood-event-available-configurations.md#flood-event-uplink-messages-type).
* Added commands to SET and GET the [Alarm Uplink periodicity](flood-sensor-lorawan-communication-protocol/flood-event-available-configurations.md#alarm-uplink-periodicity).
* Added command to [Read device hardware and firmware version](flood-sensor-lorawan-communication-protocol/read-firmware-and-hardware-version.md).
* Added FUOTA functionality.

{% hint style="info" %}
The FUOTA functionality differs from the FUOTA that's being used by the LoRa Alliance. In order to update the firmware version of devices, they should be connected to MClimate's cloud. It takes around 1500 downlinks to perform FUOTA. Due to duty-cycle limitations of the gateways, we recommend staging the FUOTA in smaller batches in case your installation is sizeable.

Feel free to reach out to [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to acquire more details on the process.
{% endhint %}

### Firmware version 1.4

**Release date:**\
3 August 2022

* Added functionality when starting the device sends a message after 20 sec.
* Fixed issue adjusting the keep-alive time.
* Fixed issue with LED indication during flood event.
* Fixed an issue with saving credentials on device startup.

### Firmware version 1.3

**Release date:**\
3 June 2022

* The temperature is added to the payload packet to be sent.
* The default keep-alive period of 3 minutes has been changed to 60 minutes.

### Firmware version 1.2

**Release date:**\
11 October 2021

* Fix flood detect, tamper detect, and buzzer notify time.
* Change the read temperature command to the read device parameters.

### Firmware version 1.1

**Release date:**\
9 June 2021

* Fix the MAC command to read the battery level.

### Firmware version 1.0

**Release date:**\
4 March 2021

* Initial version
