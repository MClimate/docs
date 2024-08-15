# FAQ

### Can MClimate Enterprise work with my LoRaWAN Network Server (LNS) provider

We support a wide range of LNS providers, you can find the full list and the configuration steps required in order to connect to Enterprise in the link below.

[https://docs.mclimate.eu/mclimate-lorawan-devices#integrations-with-network-providers](https://docs.mclimate.eu/mclimate-lorawan-devices#integrations-with-network-providers)

### I changed the Target temperature, but it goes back after a time

Check if the device is not under a Heating Profile in Enterprise and either disable it or adjust the boost time. Learn more in the articles below:

[https://docs.mclimate.eu/mclimate-enterprise/configuration-and-management/buildings/heating-profiles](https://docs.mclimate.eu/mclimate-enterprise/configuration-and-management/buildings/heating-profiles)

[https://docs.mclimate.eu/mclimate-enterprise/advanced-features-and-use-cases/boost-mode](https://docs.mclimate.eu/mclimate-enterprise/advanced-features-and-use-cases/boost-mode)

### What is Child Lock

Child Lock is a functionality that disables the manual control of a device. It is turned off by default, however you can toggle it via a command and/or a button combination. Consult your device's User manual and/or the [MClimate Device Documentation Center](https://docs.mclimate.eu/mclimate-lorawan-devices/) for the specific command.

### How long will my Device's battery life be

MClimate devices last 10+ years with default settings and the included batteries, operating at nominal conditions.

In case you want to obtain an estimation of your battery life, with custom settings, you can use the online calculator below:\
[https://mclimate.eu/pages/lorawan-battery-calculator](https://mclimate.eu/pages/lorawan-battery-calculator)

You can also obtain a Battery estimation directly from your Device Dashboard in Enterprise, learn more in the article linked below:

[https://docs.mclimate.eu/mclimate-enterprise/configuration-and-management/devices/battery-estimation](https://docs.mclimate.eu/mclimate-enterprise/configuration-and-management/devices/battery-estimation)

### How to reset my MClimate devices:

MClimate devices can not be factory reset. They come pre-provisioned with the necessary Dev EUI, App/Join EUI and APP Key for LNS provisioning. These are hard-coded and can not be changed by the client, thus they remain with the factory default settings.

{% hint style="warning" %}
The only way to initiate a new join-request is by power cycling the device or with a specific button combination. Consult your device's User Manual for instructions
{% endhint %}

Any other parameters you can change via downlink commands.

### Can MClimate devices be configured/upgraded via a computer/phone

This is not possible, MClimate devices can only be interacted with via downlink commands or via the MClimate enterprise platform. This is also the best way to Upgrade your firmware via FUOTA (details on the procedure in the [link](firmware-upgrade-over-the-air-fuota.md))

### FCT working voltage

The MClimate FCT (Fan Coil Thermostat) works in the 100-240VAC 50Hz range. It not work on 24VDC itself and can not control 24VDC FCUs (Fan Coil Units).

### How can I decode/parse the payload

We offer payload decoders for all of our devices you can find they in the MClimate LoRaWAN Devices documentation page. The location of the decoder/decoders is the same for every device, in the Uplink decoder section, for example [here](devices/mclimate-vicki-lorawan/vicki-uplink-decoder.md) is the one for Vicki.

### Dev EUI, App EUI and App Key - what are they and how to get them

The aforementioned EUIs and Key are required to register any LoRaWAN device, including MClimate ones with your LoRaWAN Network Server (LNS) of choice. If you purchased a product directly from our online store you will receive an automatic response via email from the address fulfilment@mclimate.eu. The information will be provided in the for of a CSV file.

{% hint style="warning" %}
MClimate devices can not have their Dev EUI, App EUI and App Key changed in any way from the customer. You can't use commands to change them and any reset/power cycle would not change them.
{% endhint %}

If you purchased from one of our distributors, contact them instead.

### Is my TRV compatible with Vicki

Vicki has a M30x1.5 fitting, thus it should be compatible with most such TRVs. However, in case you are unsure, or using a different fitting size you can doublecheck via our [TRV Compatibility tool](https://compatibility-tool.internal.seemelissa.com/).

In case you still can not determine if Vicki is compatible with your heating system contact us at [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu)

### Vicki displays a strange symbol after pressing the button on the back

8, 8о, 88, 77, 55 and so on (basically all numbers outside of the 5-30 temperature range) are codes for functional tests performed on the factory floor. If you have pressed the button on the back you might have ended up with one of the aforementioned displayed.

In order to take the device out of testing mode and into normal operation mode you need to do the following: Press the button on the back - the indicator starts showing "o8" Rotate the device - changes to "o" Mount the device and wait for calibration - it’ll show "77" Demount and press the button on the back - you’ll see "HI"

{% hint style="warning" %}
Vicki can not be reset in any way by the button on the back and pressing it will neither reset it to factory default nor reboot it. DO NOT PRESS the button as it is not intended for normal operation mode.
{% endhint %}

You can refer to the linked video to see the whole procedure. [https://www.youtube.com/shorts/jpvSV9T\_vkk](https://www.youtube.com/shorts/jpvSV9T\_vkk)

### How to power/start MClimate Devices with a solar panel

MClimate devices with a solar panel like the Wireless Thermostat, CO2 Display Lite or the HT Lite come without batteries (or can't use any at all). Their internal supercapacitor is pre-charged and you should be able to power them right away. Look in the manual of the specific product for the location of button, either on the side or on the back, pressing it will activate the device.

### What Fport are used by MClimate device

All Mclimate devices transmit their **uplinks on Fport 2**.

You can send downlinks on any of the following ports: **1, 2, 4-223**

### What is the hole on top of Vicki for

It is not a reset, this is where the H\&T sensor's location. The opening is required to obtain valid readings.

{% hint style="warning" %}
This is not a reset button hole, there is no button there to press. Do not try to reset the device using a pin and pressing in the hole. THIS WILL DAMAGE THE DEVICE.
{% endhint %}

### How many Vickis can be controlled externally

You can control as many Vickis as you like with an external thermostat, in a addition you can take temperature reading externally and forward it to the Vickis. Take a look at the following article to gain insights on how to set up External control and measurement via Enterprise:\
[https://docs.mclimate.eu/mclimate-enterprise/advanced-features-and-use-cases/vicki-external-temperature-control](https://docs.mclimate.eu/mclimate-enterprise/advanced-features-and-use-cases/vicki-external-temperature-control)

### Can the FCT control a split system

The Fan Coil Thermostat is not compatible with AC Split systems. It is designed for Fan Coil Unit (FCU) system control. If you need to control a split system, we recommend the MClimate Melissa:\
[https://mclimate.eu/products/melissa-smart-wi-fi-a-c-controller](https://mclimate.eu/products/melissa-smart-wi-fi-a-c-controller)

### Vicki US915 and FCC compliance

MClimate devices including Vicki are fully compatible with the LoRaWAN 1.0.3 specification. This includes the US915 band. This being said, the device is undergoing FCC certification at the time, which is not yet completed.

### What is the stroke/step of Vicki

According to the datasheet Vicki has a  step of 0.00208mm. This is the linear movement of the piston related to a single step rotation of the motor. However, there is a scaling factor of 4 that needs to be applied for practical measurements.

{% hint style="info" %}
For example, a motor position of 500 steps would mean: 500 x 0.00208 x 4 = 4.16mm. This is how much the piston will extent, pushing the TRV pin, assuming that it has calibrated to 500 steps motor range.
{% endhint %}

### Vicki displays HI but nothing happens

At this point Vicki should have attempted to connect to the LoRaWAN network, check you gateway/LNS for a join request/accept.

Make sure you have properly installed the Vicki head on its backplate (that has been properly fitted to a valve beforehand). If the aforementioned are in order Vicki should start calibrating at this point and enter normal operation mode within a minute or two after calibration has been finished. Refer to the link below for the proper installation procedure:

[https://www.youtube.com/watch?v=4z\_WnS4CDCY](https://www.youtube.com/watch?v=4z\_WnS4CDCY)

### Can I turn the display of Vicki off

This is not possible, a physical interaction with the crown will always results in the display lighting up and showing the state of the device.

In case you want to limit the information your tenants are seeing, for example if the Vicki is controlled fully remotely you could enable the Child Lock functionality, which will result the "Ch" message being displayed only. Lear more about the functionality at the [link](devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/child-lock.md).

### How is Vicki controlling the temperature

If you are using Firmware Version ≥4.3 and up Vickis is using a PI algorithm to dynamically adjust the TRV opening in order to best reach and maintain the desired Target temperature. You can learn more about the algorithm at the [link](devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/operational-modes-and-temperature-control-algorithm/algorithm-1-equal-directional-control.md).

### What is the operating voltage of Vicki and when should I change batteries

Vicki works within the 2.7 - 3.6 VDC range.

_We recommend scheduling a battery replacement once they drop below 2.8VDC to make sure you have no interruption in service, as once the level gets near 2.7VDC there might be insufficient power/force to close some valves._

### What are the Motor position and Motor Range of Vicki

When Vicki is installed it calibrates to the specific TRV it is mounted on. It determines the fully open and fully closed state of the valve and maps them to two parameter values:

Motor Range - corresponds to the fully closed state (determined via the calibration process), depending on the specific TRV this ranges between about 350 and 600

Motor Position - this is the current position of the Vicki's motor, that corresponds to what extend the valve has been closed.

{% hint style="info" %}
Motor position = 0 - the valve is FULLY OPEN

Motor Position = Motor Range - the valve is FULLY CLOSED
{% endhint %}

