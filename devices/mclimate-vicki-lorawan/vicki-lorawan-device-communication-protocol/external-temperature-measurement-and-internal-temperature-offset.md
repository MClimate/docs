# External temperature measurement and internal temperature offset

This mode is used when the measurements of Vicki's temperature sensor is not reliable - e.g. there's a cover in front of the radiator.

{% hint style="warning" %}
Keep in mind that this command is only available when the device is in operational mode "**Automatic temperature control with external temperature reading".** To set this operational mode, send downlink "0D02"
{% endhint %}

{% hint style="warning" %}
If you are in "02 – Online automatic control mode with external temperature reading" mode the Vicki will use an external temperature reading. This will affect it Open window detection capabilities. It will still use its internal readings to determine whether or not the window has been opened, not the external temperature measurement.
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

## Internal Temperature Offset

This command allows you to offset the internally measured temperature by +/- 5°C.

{% tabs %}
{% tab title="SET" %}
This command sets the desired temperature offset.

<table data-header-hidden><thead><tr><th width="131.66666666666666">Byte index</th><th width="138">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>53 – Command code.</td><td>53 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – offset parameter value, where<br>XX = (offset, [°C] + 4.928) / 0.176</td></tr></tbody></table>

Tabulated values for example offsets:

offset, \[°C] = (XX - 28) \* 0.176 = (0-28)\* 0.176=-28\* 0.176=-4.928=-5°C

Offset -5°C -> XX = 00\[HEX] -> Command: **0x5300**\
Offset -4°C -> XX = 05\[HEX]-> Command: **0x5305**\
Offset -3°C -> XX = 0B\[HEX]-> Command: **0x530B**\
Offset -2°C -> XX = 11\[HEX] -> Command: **0x5311**\
Offset -1°C -> XX = 16\[HEX] -> Command: **0x5316**\


Offset 0°C -> XX = 1C\[HEX] -> Command: **0x531C**\


Offset 1°C -> XX = 22\[HEX] -> Command: **0x5322**\
Offset 2°C -> XX = 27\[HEX] -> Command: **0x5327**\
Offset 3°C -> XX = 2D\[HEX] -> Command: **0x532D**\
Offset 4°C -> XX = 33\[HEX] -> Command: **0x5333**\
Offset 5°C -> XX = 38\[HEX] -> Command: **0x5338**
{% endtab %}

{% tab title="GET" %}


This command gets the current temperature offset.

<table data-header-hidden><thead><tr><th width="135.20724027353867">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>54 – The command code.</td></tr><tr><td>1</td><td>XX – offset parameter value</td></tr></tbody></table>

**Example command:** 0x5438,

38\[HEX]=56\[DEC]\
offset, \[°C] = (XX - 28) \* 0.176 = (56-28)\* 0.176=28\* 0.176=4.928=5°C
{% endtab %}
{% endtabs %}
