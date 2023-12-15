# External temperature measurement

This mode is used when the measurements of Vicki's temperature sensor is not reliable - e.g. there's a cover in front of the radiator.

{% hint style="warning" %}
Keep in mind that this command is only available when the device is in operational mode "**Automatic temperature control with external temperature reading".** To set this operational mode, send downlink "0D02"
{% endhint %}

{% hint style="success" %}
Since firmware >= 4.2, when in Vicki is in "**Automatic temperature control with external temperature reading"**, Vicki reports the set ext. temp value in each keepalive message.
{% endhint %}

## Set External temperature sensor value

This command is applicable when the device is in online automatic control mode with external temperature reading. The server sends this command to Vicki device when it has a new measured temperature by the external sensor. This external temperature will be used by Vicki for the internal temperature control algorithm. The command is described in details in Table 16.

### Set External temperature sensor value with accuracy 1.0

<table data-header-hidden><thead><tr><th width="135">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0F – The command code.</td></tr><tr><td>1</td><td>XX – The ext. temperature in Celsius degrees. The value must be greater than 0°C!</td></tr></tbody></table>

Table 16

**Example downlink:** 0x0F14 – the server notifies Vicki that the measured temperature by the external sensor is 20 degrees Celsius .

### Set External temperature sensor value with accuracy 0.1

{% hint style="info" %}
This command is available for firmware >= 4.2\
The value must be greater than 0°C!
{% endhint %}

<table data-header-hidden><thead><tr><th width="135">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>3C – The command code.</td></tr><tr><td>1</td><td>XX - T[15:8]</td></tr><tr><td>2</td><td>XX - T[7:0]</td></tr><tr><td></td><td>XXXX - T[15:0]= t[Celsius] * 10</td></tr></tbody></table>

**Example downlink:** 0x3C0102 – the server notifies Vicki that the measured temperature by the external sensor is 25.8 degrees Celsius. 25.8\*10 = 258 = 0x0102

### Get External temperature sensor value with accuracy 0.1

<table data-header-hidden><thead><tr><th width="96.33333333333331">Byte index</th><th width="198">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>44 – Command code.</td><td>44 – The command code.</td></tr><tr><td>1</td><td></td><td>Т[15:8]</td></tr><tr><td>2</td><td></td><td>T[7:0]<br>t° = T[15:0]/10</td></tr></tbody></table>

**Example uplink:** 0x440110 - Ext. temp measurement value is 27.2
