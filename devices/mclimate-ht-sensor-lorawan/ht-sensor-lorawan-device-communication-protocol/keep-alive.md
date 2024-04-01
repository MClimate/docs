---
description: How to decode the keep-alive packet and how to set new keep-alive period
---

# Keep-alive

## **Keep-alive command explanation**

Periodically sent message which contains the most important device data.

The data is described in Table 3. In Table 4 example packet is given.

| **Payload** | **Value** |          | **Meaning**                                                                                                                                                                                                        |
| ----------- | --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0           | 01        |          | Command byte for this packet.                                                                                                                                                                                      |
| 1           | XX        |          | Internal temperature sensor data, bits 15:8 – T\[15:8].                                                                                                                                                            |
| 2           | XX        |          | <p>Internal temperature sensor data, bits 7:0 - T[7:0].</p><p>  <span class="math">t,[ \degree C] = \frac{T[15:0] - 400 }{10}</span> </p>                                                                          |
| 3           | XX        |          | Relative Humidity data. $$RH, [ \%] = \frac{XX*100}{256}$$                                                                                                                                                         |
| 4           | XX        |          | Device battery voltage.  $$Vb, [mV] = XX * 8 + U, [mV]=1600$$                                                                                                                                                      |
| 5           | XX        | Bits 7:3 | Reserved.                                                                                                                                                                                                          |
|             |           | Bit 2    | <p>External thermistor operational status:</p><p>1: Thermistor connection is broken;</p><p>0: The thermistor is properly connected.</p>                                                                            |
|             |           | Bits 1:0 | <p>External thermistor temperature data, </p><p>bits 9:8 - T[9:8]</p>                                                                                                                                              |
| 6           | XX        |          | <p>External thermistor temperature data,</p><p>bits 7:0 - T[7:0]. The measurement resolution is  <span class="math">0.1 \degree C</span> .</p><p><span class="math">t, [\degree C] = \frac{T[9:0]}{10}</span> </p> |

_Table 3_

| **Payload** | **Value** |          | **Meaning**                                                                                                                                                 |
| ----------- | --------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0           | 01        |          | Command byte for this packet.                                                                                                                               |
| 1           | 02        |          | Internal temperature sensor data, bits 15:8 – T\[15:8].                                                                                                     |
| 2           | 88        |          | Temperature data, bits 7:0. $$t,[ \degree C] = \frac{648 - 400 }{10} = 24.8$$                                                                               |
| 3           | 80        |          | Relative humidity, $$RH, [\%] = \frac{128 * 100}{256} = 5$$                                                                                                 |
| 4           | AB        |          | Battery voltage, $$Vb, [mV] = 171 * 8+Um, [mV]=1600 = 1968$$                                                                                                |
| 5           | 02        | Bits 7:3 | Reserved.                                                                                                                                                   |
|             |           | Bit 2    | <p>External thermistor operational status:</p><p>1: Thermistor connection is broken;</p><p>0: The thermistor is properly connected.</p>                     |
|             |           | Bits 1:0 | <p>External thermistor temperature data, </p><p>bits 9:8 - T[9:8]</p>                                                                                       |
| 6           | 9C        |          | <p>External thermistor temperature data, bits </p><p>7:0 - T[7:0]. <span class="math">t, [\degree C] = \frac{0x29C}{10} = \frac{668}{10} = 66.8</span> </p> |

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

&#x20;Note that the keep-alive period must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger keep-alive period, the less battery discharge. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.\


### **Get keep-alive period command explanation**

This command is used to get the device keep-alive command messages period. Server sends the command code and the response is sent from the device together with next keep-alive command. The sent command request and the received command response are described in Table 6. The keep-alive in the response is omitted for clarity.

| **Byte index** | **Bit index** | **Sent request**       | **Received response**                     |
| -------------- | ------------- | ---------------------- | ----------------------------------------- |
| 0              | -             | 12 – The command code. | 12 – The command code.                    |
| 1              | -             |                        | XX – device keep-alive period in minutes. |

_Table 6_

**Example command sent from server:** 0x12;

**Example command response:** 0x1209 – Device keep-alive period is 9 minutes.
