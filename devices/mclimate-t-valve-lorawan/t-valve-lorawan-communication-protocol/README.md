# T-Valve LoRaWAN communication protocol

## Foreword

In the current section, we explain in detail what are the specific commands that the device supports.&#x20;

If you want to make yourself familiar with the details of how this device operates, please read through all articles.

## Communication concepts related to LoRaWAN standard

* Supported LoRaWAN MAC protocol version: 1.0.1;
* Supported LoRaWAN device Class: A;
* LoRaWAN MAC Port:&#x20;
  * Uplinks: 2.&#x20;
  * **Downlinks: 1, 2, 4-223;**
* Maximum application payload size: Maximum allowed by document “LoRaWAN regional parameters” for DataRate 0 for the given region. In most of the cases this is 51 bytes;
* Consult the document “LoRaWAN regional parameters” for additional technical information (Especially for RX2 window timings);
