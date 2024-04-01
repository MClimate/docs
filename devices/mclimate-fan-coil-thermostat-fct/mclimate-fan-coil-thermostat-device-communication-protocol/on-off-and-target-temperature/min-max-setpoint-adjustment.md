# Min/Max Setpoint adjustment

{% tabs %}
{% tab title="SET" %}
#### This command is used to set the possible min. and max. target temperature values.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code.</td></tr><tr><td>1</td><td>XX – lower temperature limit. Min.  <strong>Default value:</strong> 0x00 (0°C).</td></tr><tr><td>2</td><td>XX – upper temperature limit. Max. <strong>Default value:</strong> 0x28 (40°C).</td></tr></tbody></table>

**Example command:** 0x081018 – Sets the lower temp. limit to 16°C and the upper temp. limit to 24°C.
{% endtab %}

{% tab title="GET" %}
#### This command is used to get the possible min. and max. target temperature values. The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>15 – Command code</td><td>15 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - min. target temperature value.</td></tr><tr><td>2</td><td></td><td>XX - max. target temperature value.</td></tr></tbody></table>

**Example command:** 0x15;

**Example response:** 0x151018 – The lower temp. limit is 16°C and the upper temperature limit is 24°C.
{% endtab %}
{% endtabs %}

The allowed lower temperature range is 0...38°C (1°C resolution).

The allowed upper temperature range is 0...40°C (1°C resolution).
