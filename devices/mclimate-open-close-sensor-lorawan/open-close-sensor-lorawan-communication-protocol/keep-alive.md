# Keep-alive

## **Keep-alive command explanation**

Periodically sent message which contains the most important device data.

For this device, the default keep-alive period is 240 minutes.

The data is described in Table 2. In Table 3 example packet is given.

<table><thead><tr><th width="150">Byte index</th><th width="150">Bit index</th><th width="472.32375189107415">Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>-</td><td>Battery voltage, [mV] = XX * 8 + 1600.</td></tr><tr><td>2</td><td>7:4</td><td>Reserved.</td></tr><tr><td>2</td><td>3</td><td><p>The measured temperature:</p><p>1: Is negative;</p><p>0: Is positive.</p></td></tr><tr><td>2</td><td>2</td><td><p>Thermistor operational status:</p><p>1: Thermistor connection is broken;</p><p>0: The thermistor is connected.</p></td></tr><tr><td>2</td><td>1:0</td><td>Thermistor temperature data, bits [9:8].</td></tr><tr><td>3</td><td>7:0</td><td><p>Thermistor temperature data, bits [7:0]. </p><p>The measurement resolution is 0.1 °C. </p><p>t,[°C]= 10 T[9:0].</p></td></tr><tr><td>4</td><td>-</td><td><p>Event counter      </p><p>Unsigned value, range 0 – 16,777,215.</p><p>Bits[23:16]</p></td></tr><tr><td>5</td><td>-</td><td>Bits [15:8]</td></tr><tr><td>6</td><td>-</td><td>Bits [7:0]</td></tr><tr><td>7</td><td>7:1</td><td>Reserved.</td></tr><tr><td></td><td>0</td><td><p>Sensor status: </p><p>1: Open; </p><p>0: Closed.</p></td></tr></tbody></table>

_Table 2_

<table><thead><tr><th width="150">Payload index</th><th width="150">Value, [hex]</th><th width="150">Bit index</th><th width="448.1538461538462">Meaning</th></tr></thead><tbody><tr><td>0</td><td>01</td><td>-</td><td>Keep-alive</td></tr><tr><td>1</td><td>AB</td><td>-</td><td><p>Battery voltage, [mV] =</p><p>171 * 8 + 1600 = 2968.</p></td></tr><tr><td>2</td><td>00</td><td>7:4</td><td>Reserved.</td></tr><tr><td></td><td></td><td>3</td><td><p>The measured temperature.</p><p>0: Is positive.</p></td></tr><tr><td></td><td></td><td>2</td><td><p>Thermistor operational status.</p><p>0: The thermistor is connected.</p></td></tr><tr><td></td><td></td><td>1:0</td><td><p>Thermistor temperature data, </p><p>bits [9:8] is 0.</p></td></tr><tr><td>3</td><td>D9</td><td>-</td><td><p>Thermistor temperature data, bits [7:0]</p><p>t  = D9 / 10 = 217 / 10 = 21.7 °C.</p></td></tr><tr><td>4</td><td>1B</td><td>-</td><td><p>Count, [HEX]: 1B5CAE.</p><p>The hex value convert to </p><p>decimal =>1 793 198.</p><p>Bits[23:16]</p></td></tr><tr><td>5</td><td>5C</td><td>-</td><td>Bits [15:8]</td></tr><tr><td>6</td><td>AE</td><td>-</td><td>Bits [7:0]</td></tr><tr><td>7</td><td>01</td><td>7:1</td><td>Reserved.</td></tr><tr><td></td><td></td><td>1</td><td><p>Sensor status.</p><p>1: Open.</p></td></tr></tbody></table>

_Table 3_

### **Set keep-alive period command explanation**

Sets the period of the device keep-alive command messages. See table 4 for details.

<table><thead><tr><th width="150">Byte index</th><th width="150">Bit index</th><th width="379.2">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td>02 – The command will set the device keep-alive period.</td></tr><tr><td>1</td><td>-</td><td>XX – keep-alive period in minutes. Value 00 isn’t applicable. Default value: 240min.</td></tr></tbody></table>

_Table 4_

**Example command, \[Hex]:** 020A

The example sets the keep-alive period to 10 minutes.

Note that the keep-alive period must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger keep-alive period, the less battery discharge.&#x20;

### **Get keep-alive period command explanation**

This command is used to get the device keep-alive command messages period. Server sends the command code and the response is sent from the device together with next keep-alive command. The sent command request and the received command response are described in Table 6. The keep-alive in the response is omitted for clarity.

| Byte index | Sent request, \[hex]   | Received response, \[hex]                 |
| ---------- | ---------------------- | ----------------------------------------- |
| 0          | 12 – The command code. | 12 – The command code.                    |
| 1          |                        | XX – device keep-alive period in minutes. |

_Table 5_

**Example command sent from server, \[Hex]:** 12;

**Example command response, \[Hex]:** 120A – Device keep-alive period is 10 minutes.
