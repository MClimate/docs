# ⭐ Getting started

{% hint style="info" %}
For any type of installation, we always recommend adding the devices to your LoRaWAN Network server and installing the gateway first.
{% endhint %}

## 1. Determine your Wiring diagram (application)

{% hint style="danger" %}
**DANGER: 220V**

Do not forget to disable the power supply to the existing thermostat before you attempt any rewiring.
{% endhint %}

Before installation of the MClimate Fan Coil Thermostat (FCT), you have to examine the wiring of the thermostat you are replacing and determine the appropriate application of the FCT.

More on the available Wiring diagrams (applications) is available [here](wiring-diagrams-applications-and-operational-modes.md).

{% hint style="warning" %}
The wire terminals of the FCT can use solid-core wires or stranded wires with ferrules.&#x20;

**DO NOT** leave any wires partially or fully exposed after you mount them on the terminals.
{% endhint %}

### 1.1. Automatic change-over

In case your Fan Coil Unit is 2-pipe type and you use it both for heating in the winter and cooling in the summer, you can add an additional 10k NTC sensor to the OCC port of the FCT and let the FCT determine if it's hot or cold water running in the system and therefore whether it should set the current operational mode to heating or cooling.

## 2. Commissioning and powering up

{% hint style="info" %}
The relay box should be inserted with the wiring terminals pointing up.
{% endhint %}

Once you've wired the FCT and inserted the relay box in the main unit, you can restore the power supply to the thermostat. Once that's done, the FCT should power up and you can check the connection status and switch between modes, fan speeds, etc. to verify the working of the fan and the control of the valve(s).

### 2.1. Mounting the device on the wall

Once you are done with wiring the device, you can use the anti-theft metal bracket to mount the device on the wall. Refer to the [User Manual](./) for more information how to mount the bracket and device.

## 3. Choosing the applicable operational modes for your system

The operational modes are - **Heating, Cooling, Ventilation**. They are responsible for what the user can switch between through the buttons of the device.&#x20;

You can read more about the available operational modes [here](wiring-diagrams-applications-and-operational-modes.md#operational-modes), and as a summary below:

* Heating, Cooling and Ventilation
* Heating and Ventilation
* Cooling and Ventilation

### 3.1. 2-pipe systems:

If you do not opt-in for the automatic change-over, you can control the applicable operational modes (Heating/Cooling/Ventilation) of your system. If you are using the 2-pipe system for both heating in the winter and cooling in the summer, you can use a downlink command to set the appropriate operational mode for the season, e.g.:

* During summer, operational modes should be: Cooling and Ventilation
* During winter, operational modes should be: Heating and Ventilation.

### 3.2. 4-pipe systems:

If you have a 4-pipe system, which runs both hot and cold water, you can still use a downlink command to limit the applicable operational mode - e.g. disable heating.

## 4. Customizing the interface

{% hint style="info" %}
These steps are NOT mandatory.
{% endhint %}

### 4.1 Choosing Min/Max set-point

If you decide to limit the users ability to choose the set point within a certain range, you can define the minimum and maximum set-point as described [here](mclimate-fan-coil-thermostat-device-communication-protocol/on-off-and-target-temperature/target-temperature-ranges.md). Example: Limit between 18 and 23 degrees.

### 4.2 Locking keys

You can decide that you want to lock some of the keys on the device - e.g. disable the mode change button, on/off button, fan speed selection button, etc. More information is available [here](keys-lock.md).

{% hint style="info" %}
If you have any questions, please don't hesitate to consult with our colleagues at _lorawan-support@mclimate.eu_
{% endhint %}
