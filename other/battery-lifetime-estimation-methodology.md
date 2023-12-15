---
description: >-
  The following page aims to describe the technical approach taken while
  assessing the battery lifetime of MClimate devices and its' particular use in
  the MClimate LoRaWAN Battery Lifetime Calculator.
---

# Battery Lifetime Estimation Methodology

## Foreword

The [MClimate LoRaWAN Battery Lifetime Calculator](https://mclimate.eu/pages/lorawan-battery-calculator) is a tool that integrates all of MClimate's LoRaWAN devices and gives you the opportunity to accurately forecast the battery life of an MClimate LoRaWAN device under specific conditions.

This page aims to give a technical overview of the methodology used to create the calculator.&#x20;

## Methodology

One can break the overall consumption of an MClimate LoRaWAN Device in multiple pieces and assess their impact on the annual consumption of a device. The specific calculation strictly depends on the device type. Two examples of such a break-down are given after this section.

We have analysed the energy consumption behaviour of all our devices using an Ampere meter data-logger collecting 100,000 samples per second, giving us rich data to analyse.&#x20;

First we break down the behaviour of all our devices in separate pieces, e.g. \
&#x20;\- What's the idle consumption for 60m?\
&#x20;\- What's the energy required to transmit a message at SF12, SF11, etc.\
&#x20;\- What's the power required to take 1 temperature and humidity measurement?\
&#x20;\- What's he power required to take 1 CO2 measurement\
et cetera. More information about the specific components for each device as to be found [here](battery-lifetime-estimation-methodology.md#consumption-breakdown).

![Example of 1 CO2 measurement (MClimate CO2 Sensor and Notifier)](<../.gitbook/assets/1 co2 measurement.png>)

![Example of a "Check" button press (MClimate CO2 Sensor and Notifier)](<../.gitbook/assets/button press.png>)

![Example of a visual and acoustical notification (MClimate CO2 Sensor and Notifier)](../.gitbook/assets/Beep+lights\(medium\).png)

![Example of a 1 minute idle (sleep) mode (MClimate CO2 Sensor and Notifier)](<../.gitbook/assets/1m sleep.png>)

While looking at the examples above, please be aware that you should be looking at the values in the lower right corner that measure the charge (in Coulomb) for the selected area of the graphic.

Second, we create a mathematical model of each device using the collected data from the previous step. This model is the backbone of our LoRaWAN Battery Lifetime calculator and allows you to input the right data for your specific use-case of an MClimate device. You might notice that we've also incorporated a variable "Battery performance". As we recommend using Energizer Lithium Ultimate (L91) AA batteries, we've fixed this to 80% as recommended by Energizer, but you are free to also choose other values.&#x20;

{% hint style="warning" %}
The Join-Request and Join-Accept procedures are not taken into account when calculating the battery life of a device. If notice your device has troubles connecting to the network (e.g. frequently restarting fCnt or many Join-Requests), please consider optimising your network by adding an additional gateway. Also, please make sure to read the device's documentation about WDP (Watch-Dog Parameters).
{% endhint %}

{% hint style="info" %}
The Things Stack has been used for the performed tests. It's very important to mention that you should aim to optimize your network so that the downlinks are delivered in RX1 instead of RX2, so that the device does not consume more energy opening both RX windows. TTS uses DR3 for RX2, which further optmizes the battery life of any LoRaWAN device.
{% endhint %}

## Consumption breakdown

### MClimate Vicki LoRaWAN

Vicki is a LoRaWAN radiator thermostat. The energy-consuming activities are as follows:\
&#x20;\- Idle (sleep) consumption\
&#x20;\- Moving the motor by X steps\
&#x20;\- Measuring temperature\
&#x20;\- Data transfer on different SF

### MClimate CO2 Sensor and Notifier

The MClimate CO2 Sensor and Notifier is a CO2 sensor using NDIR technology. It also has a buzzer, an RGB LED to notify if the CO2 level is dangerous. It also has a button to manually check what the current level of CO2 is. The energy-consuming activities are as follows:\
&#x20;\- Idle (sleep) consumption\
&#x20;\- One CO2 measurement\
&#x20;\- **Default** Buzzer + RGB LED notification for bad CO2 level (please note that you can change the configuration)\
&#x20;\- "Check" button - consumption of the MCU and RGB LED once the button is clicked.\
&#x20;\- Data transfer on different SF

### **MClimate HT Sensor**

The MClimate HT sensor is a compact indoor Temperature and Humidity sensor. The energy-consuming activities are as follows:\
&#x20;\- Idle (sleep) consumption\
&#x20;\- Temperature and humidity measurement\
&#x20;\- Data transfer on different SF

### MClimate Flood Sensor

The MClimate Flood sensor is a beautiful and compact flood sensor. The energy-consuming activities are as follows:\
&#x20;\- Idle (sleep) consumption\
&#x20;\- Checking for flood\
&#x20;\- Data transfer on different SF

### MClimate T-Valve

MClimate T-Valve is a water valve that can enable or disable the flow in a system. The energy-consuming activities are as follows:\
&#x20;\- Idle (sleep) consumption\
&#x20;\- Shutting the valve on/off\
&#x20;\- Data transfer on different SF

## Default values of the calculator

You may notice that many of the calculator's fields are pre-filled with default values. E.g. in Vicki, the default number of daily steps during a heating season, is 280. That's a value derived from analysing over 2000 Vicki devices over the course of 2 heating seasons. The devices were installed in residential buildings. Another example is the CO2 "Average Daily sound notifications", which were again derived from analysing multiple devices installed at different types of buildings and their behaviour over a 2-month period of time.

Feel free to change those default values to what you believe is the case for your specific IoT application. Also feel free to use the default values and trust our analysis of tens of thousands of MClimate devices deployed in various buildings around the world.
