# 🆕 MClimate CO2 Display

<figure><img src="../../.gitbook/assets/MClimate-CO2-Display-Header-Image" alt=""><figcaption></figcaption></figure>

{% file src="../../.gitbook/assets/MClimate-CO2-Display-Datasheet.pdf" %}
MClimate CO2 Display - Datasheet English
{% endfile %}

{% file src="../../.gitbook/assets/MClimate-CO2-Display-User-Manual.pdf" %}
MClimate CO2 Display - User Manual English
{% endfile %}

## General Information

MClimate CO2 Display LoRaWAN is a stand-alone CO2 sensor powered entirely by solar energy using an organic solar panel. The device features a 2.9" e-ink screen, sensor for movement (PIR), temperature and humidity sensor, LUX sensor and NDIR CO2 sensor. The user can see the current levels of CO2 as well as historical trend. The device sends an uplink when it detects movement as well as periodically. The data from the CO2 Display can be used in any LoRaWAN-compatible system, incl. Building Management Systems to control demand-based ventilation. Sensor information can be exposed as datapoints in Modbus, BACnet and KNX systems through the use of a special gateway.

Learn more about MClimate Smart Building Solutions:

{% embed url="https://mclimate.eu/pages/smartbuildings" fullWidth="false" %}

### Features

* Solar-powered and battery free
* CO2 Sensor (NDIR)
* PIR Sensor
* LUX Sensor
* 2.9" e-ink display
* Temperature and Humidity Sensor
* Anti-theft bracket
* FUOTA
* Child lock

## Power supply

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

### 1. CO2 sensor

* Resolution: 1ppm
* Accuracy: ±(30ppm +3% of reading)
* Range: 0-5000ppm

### 2. Temperature sensor

* Resolution: 0,1°C
* Accuracy: ±0,2°C (typ) - ±0,7°C (max)

<img src="../../.gitbook/assets/temperature_accuracy" alt="" data-size="original">

### 3. Humidity sensor

* Resolution: 2%
* Accuracy: ±3% (typ) - ±3% (max)

<img src="../../.gitbook/assets/humidity_accuracy" alt="" data-size="original">

### 4. PIR sensor (movement)

* View of angle: X = 100° ; Y = 90°

![](../../.gitbook/assets/pir\_diagram.png)

### 5. LUX sensor

* Resolution: 1 LUX
* Accuracy: ±10%
* Range: 0 - 10 000 LUX

### 6. Organic Solar Cell

<figure><img src="../../.gitbook/assets/organic_solar_cell_diagrams.png" alt=""><figcaption></figcaption></figure>

## Mounting warning

<figure><img src="../../.gitbook/assets/wireless-thermostat-placement-warning (1).png" alt=""><figcaption></figcaption></figure>

If you have any questions, feel free to reach out to us at [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu)
