# Enable/Disable device flood sensor

This command sets whether the flood sensor is enabled or disabled.

{% hint style="info" %}
If you don't intend to use the flood sensor functionality it is recommended to disable it to reduce battery drain and prolong operational time.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0A – The command code</td></tr><tr><td>1</td><td>XX[0] - Set it to 1 to enable device flood sensor. Set it to 0 to disable device flood sensor.<br><strong>Default value is 1 (enabled)</strong><br>XX[7:1] - Reserved</td></tr></tbody></table>

**Example command:** 0x0A00

00\[HEX] = 00\[DEC] -> Disable the flood sensor
{% endtab %}

{% tab title="GET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>13 – The command code</td></tr><tr><td>1</td><td>XX[0] - Set it to 1 to enable device flood sensor. Set it to 0 to disable device flood sensor.<br>XX[7:1] - Reserved</td></tr></tbody></table>

**Example response:** 0x1301

01\[HEX] = 1\[DEC] -> Enable flood sensing
{% endtab %}
{% endtabs %}
