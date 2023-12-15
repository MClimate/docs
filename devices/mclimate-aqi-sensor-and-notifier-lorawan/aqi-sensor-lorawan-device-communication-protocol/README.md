# AQI Sensor LoRaWAN Device communication protocol

## Foreword

In the current section, we explain in detail what are the specific commands that the device supports.&#x20;

If you want to make yourself familiar with the details of how this device operates, please read through all articles.

## Communication concepts related to LoRaWAN standard

* Supported LoRaWAN MAC protocol version: 1.0.3;
* Supported LoRaWAN device class: A;
* LoRaWAN MAC Port: Uplink messages: 2. Downlink messages: 1, 2, 4-223;
* Maximum application payload size: Maximum allowed by document “LoRaWAN regional parameters” for DataRate 0 for the given region. In most of the cases this is 51 bytes;
* Consult the document “LoRaWAN regional parameters” for additional technical information (Especially for RX2 window timings);

## Document versions history

| **Date**   | **Version** | **Author**     | **Comment**                                         |
| ---------- | ----------- | -------------- | --------------------------------------------------- |
| 2020       | V1.0        | Martin Peevski | Initial draft                                       |
| 20.11.2020 | V1.1        | Martin Peevski | Chapters 2.1 and 3.1 updated.                       |
| 17.12.2020 | 1.2         | Martin Peevski | Added commands for device buzzer and LED’s control. |
| 25.02.2021 | 1.3         | Martin Peevski | Fix wrong command explanation at Table 16.          |
