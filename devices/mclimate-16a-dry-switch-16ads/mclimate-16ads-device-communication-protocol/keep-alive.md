# Keep-alive

## Keep-alive decoding

Periodically sent message which contains the most important device data.

The data is described in the table below, where an example is also given in a second table.

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="108">Bit Index</th><th width="77">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td><strong>01</strong></td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>7</td><td>X</td><td>Set to 1 when the temperature is negative.</td></tr><tr><td>1</td><td>6:0</td><td>XX</td><td>Internal temperature sensor data – T[°C].</td></tr><tr><td>2</td><td>-</td><td>XX</td><td><p>Relay state:</p><p>0x00 - OFF;<br>0x01 - ON.</p></td></tr></tbody></table>

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="89">Bit index</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td><strong>01</strong></td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>7</td><td>0</td><td>0: The temperature is positive.</td></tr><tr><td>1</td><td>6:0</td><td><strong>1C</strong></td><td><p>Internal temperature sensor:</p><p><strong>0x1C</strong> = 28°C.</p></td></tr><tr><td>2</td><td>-</td><td><strong>01</strong></td><td><p>Relay state:</p><p><strong>0x01</strong> - ON.</p></td></tr></tbody></table>

### Keepalive period

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – Command code to set keepalive period</td></tr><tr><td>1</td><td>XX – keep-alive period in minutes. Value 0x00 isn’t applicable.<br><strong>Default value 0A = 10min.</strong></td></tr></tbody></table>

**Example command:** 0x020F

The example sets the keep-alive period to 15 minutes.
{% endtab %}

{% tab title="GET" %}
This command is used to get the period of the keep-alive command messages. Server sends the command code and the response is sent from the device together with the next keep-alive command.&#x20;

The keep-alive in the example is omitted for clarity.

<table data-header-hidden><thead><tr><th width="131.66666666666666">Byte index</th><th width="136">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – device keep-alive period in minutes.</td></tr></tbody></table>

**Example command sent from server:** 0x12;

**Example command response:** 0x120F – the keep-alive is 15 minutes.
{% endtab %}
{% endtabs %}
