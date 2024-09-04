---
description: How to decode the keep-alive packet and how to set new keep-alive period
---

# Keep-alive

## **Keep-alive command explanation**

Periodically sent message which contains the most important device data.

The data is described in Table 3. In Table 4 example packet is given.

| **Payload i**ndex | Value |   | Meaning                                                                                              |
| ----------------- | ----- | - | ---------------------------------------------------------------------------------------------------- |
| 0                 | 01    |   | Command byte for this packet.                                                                        |
| 1                 | XX    |   | CO2 value in ppm, bits \[15:8]                                                                       |
| 2                 | XX    |   | CO2 value in ppm, bits \[7:0]                                                                        |
| 3                 | XX    |   | Internal temperature sensor data, bits 15:8 - T\[15:8]                                               |
| 4                 | XX    |   | Internal temperature sensor data, bits 7:0 - T\[7:0]. $$t, [\degree C] = \frac{T[15:0] - 400}{10}$$  |
| 5                 | XX    |   | Relative humidity data. _Relative humidity,_$$[\%] = \frac{XX*100}{256}$$                            |
| 6                 | XX    |   | Device battery voltage. $$Voltage, [mV] = XX * 8 + 1600$$                                            |

_Table 3_

| **Payload i**ndex | Value |   | Meaning                                                                                   |
| ----------------- | ----- | - | ----------------------------------------------------------------------------------------- |
| 0                 | 01    |   | Command byte for this packet.                                                             |
| 1                 | 06    |   |                                                                                           |
| 2                 | 5C    |   | CO2, \[ppm] = 0x065C = 1628.                                                              |
| 3                 | 02    |   |                                                                                           |
| 4                 | 8C    |   | _Temperature_ $$t, [\degree C] = \frac{0x028C - 400}{10} = \frac{652 - 400}{10} = 25.2$$  |
| 5                 | 8B    |   | _Relative humidity,_$$[\%] = \frac{0x8B*100}{256} =  \frac{139*100}{256} = 54.29$$        |
| 6                 | DF    |   | Device battery voltage. $$Voltage, [mV] = 223 * 8 +1600 = 3384$$                          |

_Table 4_

### **Set keep-alive period command explanation**

Sets the period of the device keep-alive command messages. See table 5 for details.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                                              |
| -------------- | ------------- | ------------------------------------------------------------------------------------ |
| 0              | -             | 02 – The command will set the device keep-alive period.                              |
| 1              | -             | XX – keep-alive period in minutes. Value 0x00 isn’t applicable. Default value: 0x0A. |

_Table 5_

**Example command, \[Hex]:** 020A

The example sets the keep-alive period to 10 minutes.

&#x20;Note that the keep-alive period must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger keep-alive period, the less battery discharge. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.

### **Get keep-alive period command explanation**

This command is used to get the device keep-alive command messages period. Server sends the command code and the response is sent from the device together with next keep-alive command. The sent command request and the received command response are described in Table 6. The keep-alive in the response is omitted for clarity.

| **Byte index** | **Bit index** | **Sent request**       | **Received response**                     |
| -------------- | ------------- | ---------------------- | ----------------------------------------- |
| 0              | -             | 12 – The command code. | 12 – The command code.                    |
| 1              | -             |                        | XX – device keep-alive period in minutes. |

_Table 6_

**Example command sent from server:** 0x12;

**Example command response:** 0x1209 – Device keep-alive period is 9 minutes.
