---
description: Find release notes for firmware of Vicki LoRaWAN
---

# 🥳 Release notes

### Firmware version 4.2

**Release date:**\
26 July 2023

* Further improvements on the new micro/half stepping motor driver, resulting in better battery consumption.
* Maximum motorRange increased from 800 steps to 860 steps
* The first temperature control algorithm, called [Equal Direction Control](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/algorithm-1-equal-directional-control.md) is removed.
* A [new PI algorithm](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/algorithm-3-proportional-integral.md) is introduced and is now the default algorithm.
* New command for [ext. temp measurement](vicki-lorawan-device-communication-protocol/external-temperature-measurement.md#set-external-temperature-sensor-value-with-accuracy-0.1) setting with accuracy 0.1 (previous accuracy was 1.0, old command is preserved).&#x20;
  * New command to [GET the ext. temp measurement value](vicki-lorawan-device-communication-protocol/external-temperature-measurement.md#get-external-temperature-sensor-value-with-accuracy-0.1) is implemented.
  * When the device is in operational mode with ext. temperature sensor, the ext. temperature value in the memory in the device is reported with each keepalive.
* New command for [open window detection](vicki-lorawan-device-communication-protocol/open-window-detection.md#open-window-commands-with-delta-t-0.1-accuracy) with delta accuracy of 0.1 (previous accuracy was 1.0, old command is preserved).
* The device now does not reply immediately to a downlink unless it contains a GET command.
* The device now replies immediately to a downlink command for new target temperature.
* [Force-attach](vicki-lorawan-device-communication-protocol/force-close.md#force-attach-a-vicki) a valve - overwrite of the button that the backplate presses to indicate the device is mounted. If you send this command, Vicki will try to calibrate even if it's not correctly installed on a backplate. If there's no backplate and valve at all, calibration will not be successful.
  * This command can be used in cases when an already installed device starts reporting motorRange of 0.
  * Keep in mind that the 5th bit in the 8th byte of the keepalive indicates whether the backplate button is pressed at all.

{% hint style="info" %}
If your devices are running firmware version 4.0 or higher, they are eligible for FUOTA upgrade to 4.2. Please get in touch with us at [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to coordinate the process.
{% endhint %}

{% hint style="warning" %}
Known issues:

* If device is frequently recalibrated, motorRange might decrease.&#x20;
  * Workaround: Avoid recalibrating frequently. motorRange is fixed when the device is manually removed from the backplate and mounted again.
{% endhint %}

### Firmware version 4.1

**Release date:**\
23 February 2023

{% embed url="https://youtu.be/e21qiqs0K1k" %}

* Use microstepping/halfstepping (dependent on the hardware version) to drive the motor. This decreases very significantly the sound that Vicki generates during motor rotation.
* Added command to [change AppEUI & AppKey](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/network-related-settings#change-appeui-and-appkey).
* Added a [command to control whether child-lock is disabled when device goes offline](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/child-lock#child-lock-behavior-when-device-goes-offline).
* Added a bit to the [keepalive](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/keep-alive) to report whether Vicki is attached to a backplate or not.
* Added a bit to the [keepalive](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/keep-alive) to report whether Vicki thinks it’s online or offline. Refer to [Network-related settings](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/network-related-settings) for more information how Vicki undestands if it's online or offline.
* Change default re-join period from 3 to 10 minutes. Remove full device reboot in case it has not connected to a LoRaWAN network for the last 10 tries.
* Proportional algorithm now closes the valve with single movement when target temperature is exceeded.
* Enriched the diagnostics information – added info on the humidity and temperature IC.
* Allow motor recalibration after initial unsuccessful calibration.
* Make it harder to enter functional test mode (88 showing on the display).
* Bugfix: Device now processes WDP \[confirmed] correctly.
* Bugfix: After Watch-Dog reset, the device retains its operational mode.
* Bugfix: Improve rotary encoder’s logic, so the display of Vicki is not randomly activated.
* Bugfix: Resolve issue with LoRaWAN MAC Layer freezing from f.w. 4.0&#x20;

{% hint style="info" %}
If your devices are running firmware version 4.0, they are eligible for FUOTA upgrade to 4.1. Please get in touch with us at [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to coordinate the process.
{% endhint %}

### Firmware version 4.0

**Release date:** \
12 April 2022

* FUOTA mechanism released

{% hint style="info" %}
The FUOTA functionality differs from the FUOTA that's being used by the LoRa Alliance. In order to update the firmware version of devices, they should be connected to MClimate's cloud. It takes around 1500 downlinks to perform FUOTA. Due to duty-cycle limitations of the gateways, we recommend staging the FUOTA in smaller batches in case your installation is sizeable.

Feel free to reach out to [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) to acquire more details on the process.
{% endhint %}

* Force-close functionality improved. Improved over-voltage detection when valve is near fully closed position.
* Devices now send full configuration information with the first uplink after the Join procedure.
* Downlink for [remote device reset](vicki-lorawan-device-communication-protocol/network-related-settings.md#remote-reset-the-device) is implemented
* Downlink for [setting only the motorPosition](vicki-lorawan-device-communication-protocol/set-motor-position-and-update-target-temperature-command-explanation.md#set-motor-position-only) is implemented
* Updated section of documentation - ["Operational modes, temperature control algorithms, target temperature and motor control"](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/)
  * Introduced commands to [get/set the temperature control algorithm being used](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/#temperature-control-algorithm-selection-and-retrieval).
* Additional temperature control algorithm introduced - called "Proportional control"
  * Default temperature control algorithm in f.w. >= 4.0
  * [Get/set commands for the parameters of the algorithm - proportional gain and period](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/algorithm-2-proportional-control.md#proportional-temperature-control-algorithm-parameters)
* Bugfix - Device now retains operational mode "Automatic with external temperature sensor" after reset.
* Bugfix - Manual target temperature change command is sent only when the target temperature is changed manually by rotating the Vicki (by hand).

{% hint style="warning" %}
Known issues

* The device may stop sending periodic uplinks due to the MAC layer of the LoRaWAN Stack freezing. The device is affected only if it works with unconfirmed uplink type. The device re-joins the network once the Watch-Dog period elapses and device realises it's offline.
  * **Suggested resolution:**
    * You can minimise the downtime of the device by re-configuring the WDP for unconfirmed uplinks to e.g. 2h.&#x20;
      * You MUST alter the DevStatusReq period in your LNS to at least once every hour.&#x20;
* When changing the keepalive period, the WDP \[unconfirmed] does not refresh.&#x20;
  * **Resolution**
    * With one downlink, first change the keepalive period, then set the WDP again.
{% endhint %}

### Firmware version 3.6

**Release date:**\
12 December 2021

* Minor bugfixes and updates
  * If pFirstLast or pNext is less than 17 steps, move the motor with 17 steps.
  * If one wants to move the motor with less than 17 steps, move the motor with 17 steps.
* Preparation for FUOTA mechanism release

Known issues:

* When device is in operational mode "Automatic with external temperature sensor" and it restarts due to power-off or Communications watch-dog, the device backs off to "Automatic" operational mode.
  * Suggested fix on production: When you send the external temperature measurement to Vicki, always append the command to switch to operational mode "automatic with external temperature sensor" - "0D02"
* [Manual target temperature change command](vicki-lorawan-device-communication-protocol/manual-target-temperature-change.md) is sent whenever the target temperature is changed, even through a downlink command.

### Firmware version 3.5

**Release date:**\
02 December 2021

* **Improved temperature measurement resolution from 0.62 to 0.18 degrees Celsius**
* **Special command if the** [**target temperature has been changed manually**](vicki-lorawan-device-communication-protocol/manual-target-temperature-change.md) **by the customer (by hand).**
* [**Open Window function**](vicki-lorawan-device-communication-protocol/open-window-detection.md) **change - Vicki fully closes the valve, regardless of motorPosition specified.**
* **Changed default parameters:**
  * **Operational mode** - changed from manual to **automatic**
  * **Keepalive interval** - changed from 3 to **10 minutes**
  * **tDiff (open/close)** - changed from 1 to **0 degrees**
  * **Uplink type** - changed from confirmed to **unconfirmed**
* Send first keepalive packet as soon as the device completes Join procedure.
* Added support for [Advanced Motor Force Control](broken-reference) of Vicki.
* Improvement of the calibration mechanism
* Bugfix - in previous firmware device reported -40 degrees after the communication watch-dog has restarted it.
* Bugfix - report battery voltage values above 3.5VDC correctly

Known issues:

* If pFirstLast or pNext is less than 17 steps, the device misbehaves
* If one moves the motor with less than 17 steps in either directions, the device misbehaves
* When device is in operational mode "Automatic with external temperature sensor" and it restarts due to power-off or Communications watch-dog, the device backs off to "Automatic" operational mode.

### Firmware version 3.4

**Release date:** \
07 January 2021

* Minor bugfixes
  * Allow keepalive interval to be greater than 21 minutes
* The internal temperature control algorithm now uses force close to close the valve.
* Introduce WDP (Communication Watch-Dog Parameters);  [Set WDP parameters](vicki-lorawan-device-communication-protocol/network-related-settings.md#set-device-radio-communication-watch-dog-parameters-command-explanation); [Get WDP parameters](vicki-lorawan-device-communication-protocol/network-related-settings.md#get-device-radio-communication-watch-dog-parameters-command-explanation)

Known issues:

* When the WDP activates and restarts the device, the first reading of the temperature is -40.
* If battery voltage is > 3.5VDC, the device reports 2VDC. The device continues working correctly.
* When device is in operational mode "Automatic with external temperature sensor" and it restarts due to power-off or Communications watch-dog, the device backs off to "Automatic" operational mode.

### Firmware version 3.3

**Release date:** \
27 October 2020

* Add Cooling mode as primary operational mode; [Set device primary operational mode](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/#set-device-primary-operational-mode); [Get device primary operational mode](vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/#get-device-primary-operational-mode)
* Minor bugfixes

Known issues:

* Keepalive interval cannot exceed 21 minutes
* When device is in operational mode "Automatic with external temperature sensor" and it restarts due to power-off or Communications watch-dog, the device backs off to "Automatic" operational mode.

### Firmware version 3.2

**Release date:** \
28 September 2020

* Initial release of Vicki LoRaWAN
