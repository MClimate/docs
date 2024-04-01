# 📖 Flood Sensor LoRaWAN communication protocol

## Foreword <a href="#foreword" id="foreword"></a>

In the current section, we explain in detail what are the specific commands that the device supports.If you want to make yourself familiar with the details of how this device operates, please read through all articles.

## Communication concepts related to LoRaWAN standard <a href="#communication-concepts-related-to-lorawan-standard" id="communication-concepts-related-to-lorawan-standard"></a>

* Supported LoRaWAN MAC protocol version: 1.0.1 for f.w. < 1.5 and 1.0.3 for f.w. >= 1.5 ;
* Supported LoRaWAN device Class: A;
* LoRaWAN MAC Port: Uplink messages: 2. Downlink messages: 1, 2, 4-223;
* Maximum application payload size: Maximum allowed by document “LoRaWAN regional parameters” for DataRate 0 for the given region. In most of the cases this is 51 bytes;
* Consult the document “LoRaWAN regional parameters” for additional technical information (Especially for RX2 window timings);

