---
description: Find release notes for firmware of HT LoRaWAN
---

# 🥳 Release notes

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

