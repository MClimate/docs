# Application of MClimate Vicki to One-pipe steam heating systems

## Introduction

The [MClimate Vicki - LoRaWAN Radiator Thermostat](../devices/mclimate-vicki-lorawan/#general-information) can be used in one-pipe steam heating systems.&#x20;

Installing Thermostatic Radiator Valves (TRVs) and Radiator Thermostats in one-pipe heating systems has been done for many years and leaders in the industry like Danfoss have specialized products for the purpose.&#x20;

Installing TRVs and Radiator thermostats in such systems can lead to substantial savings and improvement of tenants' comfort, as one of frequent complaints from tenants in such buildings is overheating of certain rooms.

If you install TRVs and MClimate Vicki - LoRaWAN Radiator Thermostats, you’d gain monitoring and control capabilities over the systems, potentially centralizing control, schedules and others.

## Prerequisites

{% hint style="warning" %}
* TRV is a Thermostatic Radiator Valve. It’s not the thermostat itself, but rather the mechanical part, which regulates the flow to the radiator.&#x20;
* Radiator Thermostat is a device that is installed on the TRV. It senses the indoor temperature and the tenant can adjust the target temperature in the room, which in turn controls the TRV and the flow through the radiator.
* Online, TRV and Radiator Thermostat are often used as interchangeable terms, while they are not. For the sake of being technically correct, we do not use those two terms interchangeably.
{% endhint %}

The vast majority of buildings in the US using steam heating systems are not prepared for installation of a radiator thermostat. One needs to first fit the radiator with an appropriate TRV and then install the Vicki radiator thermostat.

* Danfoss has an offering for TRVs on one-pipe steam heating systems: [Danfoss RA2000 1PS](https://www.danfoss.com/en-us/products/dhs/radiator-and-room-thermostats/radiator-thermostats/radiator-valves/ra2000-valves/).

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption><p>Danfoss RA2000 TRVs</p></figcaption></figure>

* Once the TRV is installed, one can install Vicki on the TRV, similar to any other radiator thermostat, with the exception that this being a smart device it requires a brief period to calibrate after powering on. Please refer to the official [Vicki Manual](https://3008755228-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-McDr-jr9h3qA888r1Yp%2Fuploads%2FgJvY7Iwik3853aJal02i%2FMClimate-Vicki-LoRaWAN-User-Manual.pdf?alt=media\&token=7e0812bd-5107-487a-94e3-45e24a4659fd) for details on installation.

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption><p>Mounting Vicki on the TRV</p></figcaption></figure>

Given that retrofitting projects would also include installing TRVs and thermostats on every radiator, it is of paramount importance to make sure that the contractor that installs the TRVs has completed the job well. Otherwise, if there’s an issue with the TRV (e.g. vent, etc.), most probably the customer will blame the Radiator Thermostats, while it is not their fault.

## Installation

While a lot can be said about the installation of Vicki, in this document, we’ll limit the information to the context of steam heating systems. For more detailed information about installation of Vicki in general, please refer to the product’s user manual and other documents available on our website [https://mclimate.](https://mclimate.eu)[eu](https://mclimate.eu)

* In this context, Vicki is installed as any other radiator thermostat on a TRV. If you choose to use Danfoss’ solution for one-pipe steam heating systems, you will require an adapter that converts the thread from Danfoss RA to M30x1.5. Given the fact that steam heating systems operate on higher temperatures compared to hydronic heating systems, we recommend usage only of [metal RA adapters, available on our website](https://mclimate.eu/collections/vicki-accessories/products/metal-valve-adapter-danfoss-ra-to-m30-x-1-5).
* If possible, install the TRV and Vicki on the side of the radiator, not directly above. While that’s not always possible, it is highly recommended as the device would be able to operate better on lower temperatures.

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption><p>Side installation of Vicki</p></figcaption></figure>

* We’ve verified that Vicki operates well in temperatures up to 190 degrees Fahrenheit, but the batteries that the device uses ([Energizer Lithium Ultimate AA](https://data.energizer.com/pdfs/l91.pdf)) are with operating temperatures of up to 140F. We’ve found a [study by NASA](https://ntrs.nasa.gov/api/citations/20030112597/downloads/20030112597.pdf), which shows testing results of the same batteries at higher temperatures that are promising, but nevertheless, we highly recommend avoiding installation of the TRV right on top of the radiator.

### How to handle enclosed radiators?

In some buildings, radiators can be enclosed with a metal/wooden cover that hides them from one’s view. While this is a great interior design choice, it means that the temperature sensor of the radiator thermostat wouldn’t be able to sense the room temperature correctly.

In such cases, it is mandatory to use a separate temperature sensor (e.g. [MClimate HT](https://mclimate.eu/products/ht-sensor) or [MClimate WT](https://mclimate.eu/products/mclimate-display-thermostat-lorawan) or any other) that can read the temperature of the room correctly. The information from the external temperature sensor would then be communicated to Vicki using LoRaWAN, Vicki would know what’s the real indoor temperature and will control the flow through the radiator accordingly.

In such cases, we always recommend using the [MClimate Wireless Thermostat](../devices/mclimate-wireless-thermostat/), as it can sense the indoor temperature accurately, but it also allows tenants to set the target temperature of the device(s) that it is connected to.

The connection between MClimate Wireless Thermostat and MClimate Vicki is done on the application-side. The two devices **do not communicate with each other directly**, but information is routed to one-another in the application server (e.g. MClimate Enterprise).

#### Utilizing MClimate Enterprise

* Set Vicki to work in ext. temp sensor mode and associate which device’s temperature should it use. You can do this in the **Control-Advanced** section.

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption><p>External Temperature Sensor settings</p></figcaption></figure>

* Set the Wireless Thermostat to act as a thermostat to one or more Vicki devices, meaning all changes of the target temperature on the WT will be sent to all associated Vicki devices. Also configured from the **Control-Advanced** section, as was with Vicki.

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption><p>Wireless Thermostat Vicki control settings</p></figcaption></figure>

#### Utilizing a 3rd Party Application

* Allow customers to select which temperature sensor should Vicki use AND
* Set Vicki to operational mode “Automatic with external temperature reading” (same as with Enterprise) AND
* Forward the information of the external temperature sensor to Vicki using [appropriate downlink commands](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/external-temperature-measurement).
* If you are using the MClimate Wireless Thermostat, it’s advisable to also forward the target temperature to Vicki(s) using the [appropriate downlink command](https://docs.mclimate.eu/mclimate-lorawan-devices/devices/mclimate-vicki-lorawan/vicki-lorawan-device-communication-protocol/set-motor-position-and-update-target-temperature-command-explanation#set-device-target-temperature-command-explanation).

### General Resources on using TRVs and Radiator Thermostats in steam heating systems

* One-Pipe Steam Systems - Piping and troubleshooting: [https://www.peerlessboilers.com/wp-content/uploads/2018/01/OnePipeSteam.pdf](https://www.peerlessboilers.com/wp-content/uploads/2018/01/OnePipeSteam.pdf)
*   Installing Thermostatic Radiator Valves:

    [https://www.steamheat.tech/try-trvs/try-trvs.html](https://www.steamheat.tech/try-trvs/try-trvs.html)
* [Thermostatic Single Pipe Steam Radiator Vent (TRV): A Solution Looking For A Problem?](https://www.youtube.com/watch?v=hjS5slMqtuA\&ab\_channel=SilentSteamTeam)
* Two-Pipe steam optimization:\
  [Two-Pipe Steam Optimization Simple measures for two- pipe steam systems that enhance efficiency and comfort.](https://www.nyc.gov/assets/nycaccelerator/downloads/pdf/NYCA\_TP\_2pipe.pdf)
* Danfoss Forums on One-Pipe systems\
  [Danfoss Valves on Single Pipe Steam Systems](https://forum.heatinghelp.com/discussion/97595/danfoss-valves-on-single-pipe-steam-systems)
* Dan Foss Thermostatic Radiator Valve Video\
  [Dan Foss Thermostatic Radiator Valve](https://www.youtube.com/watch?v=jWfr1LuvJRs\&ab\_channel=BobsPlumbingVideos)
* Danfoss Single Pipe Steam Valve Video\
  [Danfoss Single Pipe Steam Valve](https://www.youtube.com/watch?v=udg7OkWaLdo\&ab\_channel=ParkSupplyofAmerica)
