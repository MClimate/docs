---
description: How to decode the keep-alive packet and how to set new keep-alive period
---

# Keep-alive

## **Keep-alive command explanation**

Periodically sent message which contains the most important device data.

The data is described in Table 3. In Table 4 example packet is given.



| **Payload i**ndex | Value |          | Meaning                                                                                                                                                                                                                                                                                                                                            |
| ----------------- | ----- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0                 | 01    |          | Command byte for this packet.                                                                                                                                                                                                                                                                                                                      |
| 1                 | XX    |          | sAQI bits 8:1 – sAQI\[8:1].                                                                                                                                                                                                                                                                                                                        |
| 2                 | XX    | Bit 7    | <p>sAQI bit 0 – sAQI[0]. Result value is calculated as:</p><p> <span class="math">sAQI = sAQI[8:0] * 16</span> </p>                                                                                                                                                                                                                                |
|                   |       | Bits 6:2 | <p>AQI bits 4:0 – AQI[4:0]. Result value is calculated as:</p><p><span class="math">AQI = AQI[4:0] * 16</span></p>                                                                                                                                                                                                                                 |
|                   |       | Bits 1:0 | CO2eq bits 9:8 – CO2eq\[9:8].                                                                                                                                                                                                                                                                                                                      |
| 3                 | XX    |          | <p>CO2eq bits 7:0 – CO2eq[7:0]. Result value is calculated as:</p><p><span class="math">CO2eq, [ppm] = CO2eq[9:0] * 32</span> </p>                                                                                                                                                                                                                 |
| 4                 | XX    |          | <p>VOC bits 7:0 – VOC[7:0]. Result value is calculated as:</p><p><span class="math">VOC, [ppm] = VOC[7:0]*4</span></p>                                                                                                                                                                                                                             |
| 5                 | XX    |          | Relative humidity data. _Relative humidity,_$$[\%] = \frac{XX*4}{10}$$                                                                                                                                                                                                                                                                             |
| 6                 | XX    |          | Pressure data, bits 10:3 – P\[10:3].                                                                                                                                                                                                                                                                                                               |
| 7                 | XX    | Bits 7:5 | <p>Pressure data, bits 2:0 – P[2:0]. Result value is calculated as:</p><p><span class="math">P, [hPa] = \frac{P[10:0] * 40 + 30000}{100}</span> </p>                                                                                                                                                                                               |
|                   |       | Bits 4:0 | Temperature data, bits 10:6 – T\[10:6].                                                                                                                                                                                                                                                                                                            |
| 8                 | XX    | Bits 7:2 | <p>Temperature data, bits 5:0 – T[5:0]. Result value is calculated as:</p><p><span class="math">t, [\degree C] = \frac{T[10:0] - 400}{10}</span> </p>                                                                                                                                                                                              |
|                   | XX    | Bits 1:0 | <p>Air quality related parameters accuracy:</p><p>0: Sensor data is unreliable (Sensor stabilization);</p><p>1: Low accuracy, to reach higher accuracy please expose sensor   </p><p>    once to good air (for about hour) and bad air for auto- </p><p>    trimming;</p><p>2: Medium accuracy: auto-trimming ongoing;</p><p>3: High accuracy.</p> |
| 9                 | XX    |          | Device battery voltage. $$Voltage, [mV] = XX*8 + 1600$$                                                                                                                                                                                                                                                                                            |

_Table 3_

| **Payload i**ndex | Value |          | Meaning                                                                                                                                               |
| ----------------- | ----- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0                 | 01    |          | Command byte for this packet.                                                                                                                         |
| 1                 | 07    |          | sAQI\[8:1] = 0x07.                                                                                                                                    |
| 2                 | A4    | Bit 7    | <p> sAQI[0] = 0x01.</p><p> <span class="math">sAQI = sAQI[8:0] * 16 = 0x0F * 16 = 240</span> </p>                                                     |
|                   |       | Bits 6:2 | $$AQI = AQI[4:0] * 16 = 0x09 * 16 = 144$$                                                                                                             |
|                   |       | Bits 1:0 | CO2eq\[9:8] = 0x00.                                                                                                                                   |
| 3                 | 4C    |          | <p>CO2eq[7:0] = 0x4C</p><p><span class="math">CO2eq, [ppm] = CO2eq[9:0] * 32 = 0x4C * 32 = 2432</span> </p>                                           |
| 4                 | 03    |          | $$VOC, [ppm] = VOC[7:0]*4 = 0x03*4 = 12$$                                                                                                             |
| 5                 | 53    |          | _Relative humidity,_$$[\%] = \frac{0x53*4}{10} = 33.2$$                                                                                               |
| 6                 | C9    |          | P\[10:3] = 0xC9.                                                                                                                                      |
| 7                 | A9    | Bits 7:5 | <p>P[2:0] = 0x05</p><p><span class="math">P, [hPa] = \frac{P[10:0] * 40 + 30000}{100} = \frac{0x64D * 40 + 30000}{100} = 945.2</span> </p>            |
|                   |       | Bits 4:0 | Temperature data, bits 10:6 – T\[10:6].                                                                                                               |
| 8                 | E3    | Bits 7:2 | <p>Temperature data, bits 5:0 – T[5:0]</p><p><span class="math">t, [\degree C] = \frac{T[10:0] - 400}{10} = \frac{0x278 - 400}{10} = 23.2</span> </p> |
|                   |       | Bits 1:0 | Air quality related parameters accuracy: 3                                                                                                            |
| 9                 | CD    |          | $$Voltage, [mV] = CD*8 + 1600 = 205 * 8 + 1600 = 3240$$                                                                                               |

_Table 4_

### **Set keep-alive period command explanation**

Sets the period of the device keep-alive command messages. See table 5 for details.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                                              |
| -------------- | ------------- | ------------------------------------------------------------------------------------ |
| 0              | -             | 02 – The command will set the device keep-alive period.                              |
| 1              | -             | XX – keep-alive period in minutes. Value 0x00 isn’t applicable. Default value: 0x03. |

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

**Example command sent from server:** 0x12;

**Example command response:** 0x1209 – Device keep-alive period is 9 minutes.
