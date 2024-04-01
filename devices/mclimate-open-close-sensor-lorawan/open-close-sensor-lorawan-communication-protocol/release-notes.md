# 🥳 Release notes

### Firmware version 1.2

**Release date:** \
20 January 2023

* Added functionality to send device settings in the first radio packet to the server.
* Added device startup delay and LED test functionality.
* Fixed bug with command response after one iteration.
* Fixed bug regarding conf. uplinks watch-dog period, when keep-alive period changed.
* Removed the device reset functionality when you have not joined the LoRaWAN network for 5 attempts.

### Firmware version 1.1

**Release date:** \
23 September 2022

* FUOTA mechanism released

{% hint style="info" %}
The FUOTA functionality differs from the FUOTA that's being used by the LoRa Alliance. In order to update the firmware version of devices, they should be connected to MClimate's cloud. It takes around 1500 downlinks to perform FUOTA. Due to duty-cycle limitations of the gateways, we recommend staging the FUOTA in smaller batches in case your installation is sizeable.

Feel free to reach out to [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to acquire more details on the process.
{% endhint %}

### Firmware version 1.0

**Release date:** \
7 July 2022

* Initial firmware release
