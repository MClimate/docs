---
description: >-
  How is the temperature measured by Vicki and other products affected by the
  indoor environment?
---

# How to solve Large space heating issues

## Major important points

First and foremost – you should take into account that a room can’t have a completely uniform temperature over its entire volume. The temperature in a room is a gradient and not homogeneous – if you put 10 sensors in a room at different heights, they all will have slightly different readings. And that’s natural, since physics teach us that the hot air rises and cold air drops down.

Another important point is that comfort is subjective, there is a correlation between temperature and comfort, but one does not equate the other. Comfort is a combination of many factors – temperature of the room, humidity, temperature of walls, floor, surfaces, etc., plus there is the subjective factor too.

Measuring the temperature in the room is critical for Vicki’s good operation. However, due to many external factors, you might have noticed a “wrong” reading in some cases.

Vicki uses a high-quality temperature and humidity sensor by Texas Instruments. The readings you are seeing are correct with a very small margin of tolerance. If you see a temperature reading from Vicki that you don’t like – it’s not the device, it’s the external factors.

Contrary to common believe, measuring temperature near radiators is actually an excellent placement, since radiators are hot and cause a lot of convection. Air is heated by the radiator, rises up and draws fresh air into the radiator (check out the image below).

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>Unobstructed radiator convection</p></figcaption></figure>

Naturally, a radiator that’s 30cm high will measure a different temperature than a radiator that’s at 1m height. That’s normal and is the status quo even with the manual thermostatic valves.

Now to the external factors – if you have a cover on top/in front of the radiator, the readings will definitely be different, since the covers are affecting the convection. If you have a baseboard/sill on top of the radiator, it would again cause slightly different measured temperature. Same would happen if the Vicki is covered by a curtain or is too close to e.g., a cabinet/sofa, as those things would naturally impede the natural flow of the air (check out the image below for reference).

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Obstructed radiator convection</p></figcaption></figure>

## Strategies to improve the measurement & control

Method 1: Use an external temperature sensor

Air temperature, especially in large spaces cannot be homogeneous over the whole area, there is no avoiding this, completely. Thus, for larger volumes or rooms where the air circulation is impeded by a e.g., cover, it is recommended to use an external sensor. This ensures that the point of measurement can be exactly where desired (as the radiator head cannot be moved away from it), there can even be multiple external temperature sensors to control Vicki heads on different radiators if need be (for a very large space).

Once you have the external temperature sensor, you can put Vicki in operational mode “Automatic control with external temperature sensor” and send the ext. temperature measurements to Vicki using downlinks. The Application Server should be responsible of routing the ext. temp measurement to Vicki. We suggest that you send a downlink to Vicki only in case the temperature has changed, in order to improve network traffic.

In case you are using the MClimate Enterprise (SaaS), it is very easy to link an external sensor with a single or a group of Vickis.

This strategy works well with the MClimate Wireless Thermostat LoRaWAN, which can also change the setpoint of Vicki(s).

{% embed url="https://mclimate.eu/products/mclimate-display-thermostat-lorawan" %}

Method 2: Adjust higher target temp for comfort

Perhaps the most straightforward and intuitive solution is to make a subjective decision on the target temperature and manually adjust it up or down based on one’s perception. Adding a few degrees up or down to the target temperature can very easily solve the issue, simply find out what is comfortable for you and your client instead of 21 set e.g. 22. The valve will try to achieve this temperature which will result in a better feeling overall.

Method 3: Use temperature offset

Soon we’ll add a new firmware functionality that would allow you to adjust the measured temperature, compensating based on your preference and the particular space and installation. This way you can set it based on the subject’s preferences for that particular space. We cannot, however provide you with a timeline for the feature, but it’ll look a little something like:

* Let’s say the measured temp is 21.2 degrees
* You put an offset of -1.2 degrees
* Vicki will control the radiator valve based on 21.2-1.2 = 20.0 degrees C.
