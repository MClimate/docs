# Keep-alive

## **Keep-alive command explanation**

Periodically sent message which contains the most important device data.

For this device, the default keep-alive period is 240 minutes.

The data is described in Table 3. In Table 4 example packet is given.

<table data-header-hidden><thead><tr><th>Payload index</th><th>Value</th><th width="150"></th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Payload index</strong></td><td><strong>Value, [hex]</strong></td><td><strong>Bit index</strong></td><td><strong>Meaning</strong></td></tr><tr><td>0</td><td>01</td><td>-</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>XX</td><td>-</td><td>Device battery voltage.<span class="math">Voltage , [mV right ] = XX ∗ 8 + 1600</span></td></tr><tr><td>2</td><td>XX</td><td>Bits 7:3</td><td>Reserved.</td></tr><tr><td></td><td></td><td>Bit 2</td><td><p>Thermistor operational status:</p><p>1: Thermistor connection is broken;</p><p>0: The thermistor is properly connected.</p></td></tr><tr><td></td><td></td><td>Bits 1:0</td><td>Thermistor temperature data, bits [9:8] - T[9:8]</td></tr><tr><td>3</td><td>XX</td><td>-</td><td>Thermistor temperature data, bits [7:0] - T[7:0]. The measurement resolution is 0.1.<span class="math">℃</span><br><span class="math">t , [° C ] = \frac{T [9 : 0]} {10}</span></td></tr><tr><td>4</td><td>XX</td><td>-</td><td>Button press event data.</td></tr></tbody></table>

_Table 3_

<table data-header-hidden><thead><tr><th>Payload index</th><th>Value</th><th width="150"></th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Payload index</strong></td><td><strong>Value, [hex]</strong></td><td><strong>Bit index</strong></td><td><strong>Meaning</strong></td></tr><tr><td>0</td><td>01</td><td>-</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>AB</td><td>-</td><td>Device battery voltage.<span class="math">Voltage , [mV] = 171 ∗ 8 + 1600 = 2968</span></td></tr><tr><td>2</td><td>02</td><td>Bits 7:3</td><td>Reserved.</td></tr><tr><td></td><td></td><td>Bit 2</td><td><p>Thermistor operational status:</p><p>0: The thermistor is properly connected.</p></td></tr><tr><td></td><td></td><td>Bits 1:0</td><td>Thermistor temperature data, bits 9:8 - T[9:8]</td></tr><tr><td>3</td><td>9B</td><td>-</td><td><p>Thermistor temperature data, bits 7:0 - T[7:0]. The measurement resolution is 0.1.<span class="math">℃</span></p><p><span class="math">t , [° C ] = \frac{0x29B} {10} = \frac{667} {10} = 66.7</span></p></td></tr><tr><td>4</td><td>03</td><td>-</td><td>Button event data = 3 (three) button presses.</td></tr></tbody></table>

_Table 4_

### **Set keep-alive period command explanation**

Sets the period of the device keep-alive command messages. See table 5 for details.

<table data-header-hidden><thead><tr><th width="150">Byte index</th><th width="450.4285714285714">Hex value – Meaning</th><th data-hidden>Bit index</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td><td>Bit index</td></tr><tr><td>0</td><td>02 – The command will set the device keep-alive period.</td><td>-</td></tr><tr><td>1</td><td><p>XX – keep-alive period in minutes.</p><p>Value 00 isn’t applicable.</p><p>Default value: 240 min.</p></td><td>-</td></tr></tbody></table>

_Table 5_

**Example command, \[Hex]:** 020A

The example sets the keep-alive period to 10 minutes.

Note that the keep-alive period must respect the LoRaWAN messages duty cycle limitations.    Otherwise the message will be sent when this is allowed.

### **Get keep-alive period command explanation**

This command is used to get the device keep-alive command messages period. Server sends the command code and the response is sent from the device together with next keep-alive command. The sent command request and the received command response are described in Table 6. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="157.09737827715355">Byte index</th><th width="150">Sent request</th><th width="316.1538461538462">Received response</th><th data-hidden>Bit index</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request, [hex]</strong></td><td><strong>Received response, [hex]</strong></td><td><strong>Bit i</strong>ndex</td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td><td>-</td></tr><tr><td>1</td><td></td><td>XX – device keep-alive period in minutes.</td><td>-</td></tr></tbody></table>

_Table 6_

**Example command sent from server, \[HEX]:** 12;

**Example command response, \[HEX]:** 120А – Device keep-alive period is 10 minutes.
