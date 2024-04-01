# 📖 CO2 Sensor LoRaWAN Device communication protocol

## Foreword

In the current section, we explain in detail what are the specific commands that the device supports.&#x20;

If you want to make yourself familiar with the details of how this device operates, please read through all articles.

{% hint style="warning" %}
Please mind that notifications can require a lot of energy depending on your configuration. E.g. if you power on the LED or Buzzer for more than the default parameters, batteries will be depleted faster.

Same is true for the CO2 check interval configuration as well as for the uplink interval. \
The default values are what we recommend. We give you the flexibility to adjust them, but deviating the default values might shorten the battery life of your devices!
{% endhint %}

## Communication concepts related to LoRaWAN standard

* Supported LoRaWAN MAC protocol version: 1.0.3;
* Supported LoRaWAN device Class: A;
* LoRaWAN MAC Port: Uplink messages: 2. Downlink messages: 1, 2, 4-223;
* Maximum application payload size: Maximum allowed by document “LoRaWAN regional parameters” for DataRate 0 for the given region. In most of the cases this is 51 bytes;
* Consult the document “LoRaWAN regional parameters” for additional technical information (Especially for RX2 window timings);

## Document versions history

| **Date**   | **Version** | **Author**     | **Comment**        |
| ---------- | ----------- | -------------- | ------------------ |
| 01.06.2021 | V1.0        | Martin Peevski | Initial draft      |
| 28.06.2021 | V1.1        | Martin Peevski | New commands added |
