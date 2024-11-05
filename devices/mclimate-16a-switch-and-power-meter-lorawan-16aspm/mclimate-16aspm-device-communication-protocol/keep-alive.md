# Keep-alive

## Keep-alive decoding

The Keep-alive is a periodically sent message which contains the most important device data.

The data is described in the table below, where an example is also given in a second table.

{% hint style="warning" %}
Current below 100mA is not registered and measured, thus a device consuming less than this threshold would produce keep-alives with 0 values for the current, power and the accumulated energy will not increase.

This will not impact functionality otherwise and the connected appliance will still be powered correctly.
{% endhint %}

{% tabs %}
{% tab title="f.w.  ≥ 1.3" %}
<table><thead><tr><th width="87.66666666666669">Byte</th><th width="100">Bit Index</th><th width="77">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td><strong>01</strong></td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>7</td><td>X</td><td>Set to 1 when the temperature is negative.</td></tr><tr><td>1</td><td>6:0</td><td>XX</td><td>Internal temperature sensor data – T[°C].</td></tr><tr><td>2</td><td>-</td><td>XX</td><td>Energy data, bits - E[31:24].  </td></tr><tr><td>3</td><td>-</td><td>XX</td><td>Energy data, bits - E[23:16].  </td></tr><tr><td>4</td><td>-</td><td>XX</td><td>Energy data, bits - E[15:8].  </td></tr><tr><td>5</td><td>-</td><td>XX</td><td><p>Energy data, bits - E</p><p>[7:0]. <br>Energy [kWh] = E[31:0] / 1000.</p></td></tr><tr><td>6</td><td>-</td><td>XX</td><td>Power data, bits - [15:8]. </td></tr><tr><td>7</td><td>-</td><td>XX</td><td>Power data, bits - [7:0]. <br>Power, [W]. </td></tr><tr><td>8</td><td>-</td><td>XX</td><td>Voltage, [V].</td></tr><tr><td>9</td><td>-</td><td>XX</td><td>Current data, bits - [15:8]. </td></tr><tr><td>10</td><td>-</td><td>XX</td><td><p>Current data, bits - [7:0]. </p><p>Current, [mA].</p></td></tr><tr><td>11</td><td>-</td><td>XX</td><td><p>Relay state:</p><p>0x00 - OFF;<br>0x01 - ON.</p></td></tr></tbody></table>

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="96">Bit index</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td><strong>01</strong></td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>7</td><td><strong>0</strong></td><td>0: The temperature is positive.</td></tr><tr><td>1</td><td>6:0</td><td><strong>1C</strong></td><td><p>Internal temperature sensor:</p><p><strong>0x1C</strong> = 28°C.</p></td></tr><tr><td>2</td><td>-</td><td><strong>03</strong></td><td>Energy data, bits - E[31:24]. </td></tr><tr><td>3</td><td>-</td><td><strong>4A</strong></td><td>Energy data, bits - E[23:16].</td></tr><tr><td>4</td><td>-</td><td><strong>24</strong></td><td>Energy data, bits - E[15:8]. </td></tr><tr><td>5</td><td>-</td><td><strong>18</strong></td><td>Energy data, bits - E[7:0]. <br>Energy [kWh] = E[31:0] / 1000.<br>Energy = <strong>0x34A2418</strong> / 1000 = 55 190,552kWh.</td></tr><tr><td>6</td><td>-</td><td><strong>05</strong></td><td>Power data, bits - [15:8]. </td></tr><tr><td>7</td><td>-</td><td><strong>D9</strong></td><td>Power data, bits - [7:0]. <br><strong>0x05D9</strong> = 1497W. </td></tr><tr><td>8</td><td>-</td><td><strong>E7</strong></td><td>Voltage:<br><strong>0xE7</strong> = 231V.</td></tr><tr><td>9</td><td>-</td><td><strong>19</strong></td><td>Current data, bits - [15:8]. </td></tr><tr><td>10</td><td>-</td><td><strong>52</strong></td><td><p>Current data, bits - [7:0].  </p><p><strong>0x1952</strong> = 6482mA.</p></td></tr><tr><td>11</td><td>-</td><td><strong>01</strong></td><td><p>Relay state:</p><p><strong>0x01</strong> - ON.</p></td></tr></tbody></table>
{% endtab %}

{% tab title="f.w. ≤ 1.2" %}
<table><thead><tr><th width="93.66666666666669">Byte</th><th width="100">Bit Index</th><th width="77">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td><strong>01</strong></td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>-</td><td>XX</td><td>Internal temperature sensor data – T[°C].</td></tr><tr><td>2</td><td>-</td><td>XX</td><td>Energy data, bits - E[31:24].  </td></tr><tr><td>3</td><td>-</td><td>XX</td><td>Energy data, bits - E[23:16].  </td></tr><tr><td>4</td><td>-</td><td>XX</td><td>Energy data, bits - E[15:8].  </td></tr><tr><td>5</td><td>-</td><td>XX</td><td><p>Energy data, bits - E</p><p>[7:0]. <br>Energy [kWh] = E[31:0] / 1000.</p></td></tr><tr><td>6</td><td>-</td><td>XX</td><td>Power data, bits - [15:8]. </td></tr><tr><td>7</td><td>-</td><td>XX</td><td>Power data, bits - [7:0]. <br>Power, [W]. </td></tr><tr><td>8</td><td>-</td><td>XX</td><td>Voltage, [V].</td></tr><tr><td>9</td><td>-</td><td>XX</td><td>Current data, bits - [15:8]. </td></tr><tr><td>10</td><td>-</td><td>XX</td><td><p>Current data, bits - [7:0]. </p><p>Current, [mA].</p></td></tr><tr><td>11</td><td>-</td><td>XX</td><td><p>Relay state:</p><p>0x00 - OFF;<br>0x01 - ON.</p></td></tr></tbody></table>

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="96">Bit index</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td><strong>01</strong></td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>-</td><td><strong>1C</strong></td><td><p>Internal temperature sensor:</p><p><strong>0x1C</strong> = 28°C.</p></td></tr><tr><td>2</td><td>-</td><td><strong>03</strong></td><td>Energy data, bits - E[31:24]. </td></tr><tr><td>3</td><td>-</td><td><strong>4A</strong></td><td>Energy data, bits - E[23:16].</td></tr><tr><td>4</td><td>-</td><td><strong>24</strong></td><td>Energy data, bits - E[15:8]. </td></tr><tr><td>5</td><td>-</td><td><strong>18</strong></td><td>Energy data, bits - E[7:0]. <br>Energy [kWh] = E[31:0] / 1000.<br>Energy = <strong>0x34A2418</strong> / 1000 = 55 190,552kWh.</td></tr><tr><td>6</td><td>-</td><td><strong>05</strong></td><td>Power data, bits - [15:8]. </td></tr><tr><td>7</td><td>-</td><td><strong>D9</strong></td><td>Power data, bits - [7:0]. <br><strong>0x05D9</strong> = 1497W. </td></tr><tr><td>8</td><td>-</td><td><strong>E7</strong></td><td>Voltage:<br><strong>0xE7</strong> = 231V.</td></tr><tr><td>9</td><td>-</td><td><strong>19</strong></td><td>Current data, bits - [15:8]. </td></tr><tr><td>10</td><td>-</td><td><strong>52</strong></td><td><p>Current data, bits - [7:0].  </p><p><strong>0x1952</strong> = 6482mA.</p></td></tr><tr><td>11</td><td>-</td><td><strong>01</strong></td><td><p>Relay state:</p><p><strong>0x01</strong> - ON.</p></td></tr></tbody></table>
{% endtab %}
{% endtabs %}

## Keepalive period

{% tabs %}
{% tab title="SET" %}
This command is used to set the period of the keep-alive command messages.

<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – Command code to set keepalive period</td></tr><tr><td>1</td><td>XX – keep-alive period in minutes. Value 0x00 isn’t applicable.<br><strong>Default value 0A = 10min.</strong></td></tr></tbody></table>

The keep-alive in the example is omitted for clarity.

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

{% hint style="warning" %}
Note that the period value must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.
{% endhint %}
