# MClimate Wireless Thermostat



<figure><img src="../../.gitbook/assets/MClimate Wireless Thermostat Header" alt=""><figcaption></figcaption></figure>

{% file src="../../.gitbook/assets/MClimate-Wireless-Thermostat-Datasheet.pdf" %}
Datasheet
{% endfile %}

{% file src="../../.gitbook/assets/Wireless-Thermostat-User-Manual.pdf" %}
User Manual
{% endfile %}

### General information <a href="#general-information" id="general-information"></a>

MClimate Wireless Thermostat is a stand-alone thermostat powered entirely by solar energy using an organic solar panel.&#x20;

The device features a 2.9" e-ink screen, sensor for movement (PIR), temperature and humidity sensor, LUX sensor and 3 buttons. The user can change the target temperature and see current indoor conditions.&#x20;

The device sends an uplink after any event as well as periodically. The data from the Wireless Thermostat can be used in any LoRaWAN-compatible system, incl. Building Management Systems to control different appliances in the building.

Learn more about MClimate Smart Building Solutions:



{% embed url="https://mclimate.eu/pages/smartbuildings" %}

Purchase MClimate Wireless Thermostat:

{% embed url="https://mclimate.eu/products/mclimate-display-thermostat-lorawan?variant=47859106808140" %}

## Features <a href="#features" id="features"></a>

* Solar-powered
* PIR sensor
* LUX sensor
* E-ink display
* Temperature & humitity sensor
* 3 buttons
* Anti-theft bracket
* FUOTA
* Child lock
*   Sensing only mode

    (no target temp displayed)

## Power supply <a href="#power-supply" id="power-supply"></a>

* Solar-powered Lithium-ion capacitor (LIC)&#x20;
  * AND/OR 2 or 4xAA 1.5VDC batteries&#x20;
  * AND/OR USB-C
* **Operating voltage:**
  * 2.5-3.8VDC powered by Solar Panel
  * 2-3.6VDC powered by batteries
  * 5VDC powered from USB-C
* **Expected battery life (depending on configuration and environment):**&#x20;
  * Indefinite powered by solar - up to 21 days in complete darkness
  * 10+ years powered by AA batteries
* _**Device does not operate with rechargeable batteries!**_&#x20;

## Compatibility

* LoRaWAN 1.0.3, class A device, EU868
* Encryption: LoRaWAN End-to-end encryption (AES-CTR)
* Activation: OTAA
* Link budget: 130dB
* RF Transmit Power: 14dB

## Sensors

### 1. Temperature sensor

* Resolution: 0,1°C
* Accuracy: ±0,2°C (typ) - ±0,7°C (max)

<img src="../../.gitbook/assets/temperature_accuracy" alt="" data-size="original">

### 2. Humidity sensor

* Resolution: 2%
* Accuracy: ±3% (typ) - ±3% (max)

<img src="../../.gitbook/assets/humidity_accuracy" alt="" data-size="original">

### 3. PIR sensor (movement)

* View of angle: X = 100° ; Y = 90°

![](../../.gitbook/assets/pir_diagram.png)

### 4. LUX sensor

* Resolution: 1 LUX
* Accuracy: ±10%
* Range: 0 - 10 000 LUX

### 5. Organic Solar Cell

<figure><img src="../../.gitbook/assets/organic_solar_cell_diagrams.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}


The device uses its internal supercapacitor as its main source of power, which is directly charged via the solar cell. When its voltage drops below a certain threshold the device stops operating until it is recharged sufficiently.

In case you are using batteries/USB the following logic applies:

1. Supercapacitor is discharged first (no battery/USB power is utilized).
2. When the supercapacitor voltage drops to the voltage of the batteries/USB it starts charging from the batteries/USB. Thus, the device is effectively powered by the batteries/USB, however it is still through the supercapacitor.
3. If at this point the batteries discharge sufficiently or USB power is no longer supplied the supercapacitor will discharge below the operational threshold and the device will turn off.
4. When and if the supercapacitor recharges sufficiently, it becomes the main power source, and so on...
{% endhint %}

## Mounting warning

<figure><img src="../../.gitbook/assets/wireless-thermostat-placement-warning (1).png" alt=""><figcaption></figcaption></figure>

If you have any questions, feel free to reach out to us at [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu)
