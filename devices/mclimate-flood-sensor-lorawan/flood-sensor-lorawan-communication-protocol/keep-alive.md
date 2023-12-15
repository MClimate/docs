# Keep-alive

## **Keep-alive command explanation**

Periodically sent message which contains the most important device data. The default keep-alive period is 60 minutes.



The data is described in Table 2. In Table 3 example packet is given.

<table><thead><tr><th width="150">Byte index</th><th width="150">Bit index</th><th width="454.6540284360189">Meaning</th></tr></thead><tbody><tr><td>0</td><td>7:5</td><td><p>000: Keep-alive; </p><p>001: Reserved;</p><p>010: Flood detected by device sensor; </p><p>100: Box tamper switch detected.</p></td></tr><tr><td></td><td>4</td><td>Reserved.</td></tr><tr><td></td><td>3</td><td><p>0: No box tamper detected; </p><p>1: Box tamper detected.</p></td></tr><tr><td></td><td>2</td><td>Reserved.</td></tr><tr><td></td><td>1</td><td><p>0: No flood detected; </p><p>1: Flood detected.</p></td></tr><tr><td></td><td>0</td><td>Reserved.</td></tr><tr><td>1</td><td>7:0</td><td>Battery voltage, [mV] = (bits7:0)*16</td></tr><tr><td>2</td><td>7</td><td><p>0: The temperature is positive; </p><p>1: The temperature is negative. </p><p><strong>NOTE:</strong> This bit is used in firmware version 1.5 or later.</p></td></tr><tr><td></td><td>6:0</td><td>Temperature sensor value in Celsius degrees.</td></tr></tbody></table>

_Table 2._



Example of sending a packet from the device to the server: **\[Hex]:** 42C21A

<table><thead><tr><th width="150">Payload index</th><th width="106">Value</th><th width="104">Bit index</th><th width="366.1538461538462">Meaning</th></tr></thead><tbody><tr><td>0</td><td>42</td><td>7:5</td><td><p>010: Flood detected</p><p> by device sensor. </p></td></tr><tr><td></td><td></td><td>4</td><td>Reserved.</td></tr><tr><td></td><td></td><td>3</td><td>0: No box tamper detected.</td></tr><tr><td></td><td></td><td>2</td><td>Reserved.</td></tr><tr><td></td><td></td><td>1</td><td>1: Flood detected.</td></tr><tr><td></td><td></td><td>0</td><td>Reserved.</td></tr><tr><td>1</td><td>C2</td><td>7:0</td><td><p>Battery voltage</p><p>[mV] = (194)*16 = 3104.</p></td></tr><tr><td>2</td><td>1A</td><td>7</td><td><p>0: The temperature is positive. </p><p><strong>NOTE:</strong> This bit is used in firmware version 1.5 or later.</p></td></tr><tr><td></td><td></td><td>6:0</td><td>The temperature is 26 Celsius degrees.</td></tr></tbody></table>

_Table 3._

### Keepalive period

{% tabs %}
{% tab title="Set keep-alive period" %}
<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>05 – Command code to set keepalive period.</td></tr><tr><td>1</td><td><p>XX – keep-alive period in minutes. </p><p>Data byte MSB.</p></td></tr><tr><td>2</td><td><p>XX – keep-alive period in minutes.  </p><p>Data byte LSB. </p><p>Value 0x00 isn’t applicable. Default value: 60min. </p><p>The maximum value that can be set is 240 hours.</p></td></tr></tbody></table>

**Example command, \[Hex]:** 05000A - The example sets the keep-alive period to 10 minutes.

Note that the period value must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger period value, the less battery discharge. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.
{% endtab %}

{% tab title="Get keep-alive period" %}
This command is used to get the Flood sensor period of the keep-alive command messages. Server sends the command code and the response is sent from the device together with the next keep-alive command. The keep-alive in the example is omitted for clarity.

{% hint style="info" %}
**NOTE:** This command is available for firmware version 1.5 or later.
{% endhint %}

<table data-header-hidden><thead><tr><th width="137.66666666666666">Byte index</th><th width="225">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td></tr><tr><td>1</td><td></td><td><p>XX – keep-alive period in minutes. </p><p>Data byte MSB.</p></td></tr><tr><td>2</td><td></td><td><p>XX – keep-alive period in minutes. </p><p>Data byte LSB.</p></td></tr></tbody></table>

**Example command sent from server, \[Hex]:** 12;

**Example command response, \[Hex]:** 12003C – The Flood sensor keep-alive is 60 minutes.
{% endtab %}
{% endtabs %}
