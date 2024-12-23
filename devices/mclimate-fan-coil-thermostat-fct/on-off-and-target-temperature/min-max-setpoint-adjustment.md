# Target temperature ranges

## SET/GET target temperature ranges (reparate ranges for cooling and heating)

{% hint style="info" %}
These commands are available for devices with firmware version ≥ 1.6
{% endhint %}

#### These commands are used to set/get the possible min. and max. target temperature values of heating and cooling mode.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>16 – The command code.</td></tr><tr><td>1</td><td>XX – Heating target temp. limit min.<br><strong>Default value:</strong> 0x05 (5°C).</td></tr><tr><td>2</td><td>XX – Heating target temp. limit max.<br><strong>Default value:</strong> 0x1E (30°C).</td></tr><tr><td>3</td><td>XX – Cooling target temp. limit min.<br><strong>Default value:</strong> 0x05 (5°C).</td></tr><tr><td>4</td><td>XX – Cooling target temp. limit max.<br><strong>Default value:</strong> 0x1E (30°C).</td></tr></tbody></table>

**Example command:** 0x161018141D: \
– Sets the target temp. limit min to 16°C and the target temp. limit max. to 24°C of heating mode;\
– Sets the target temp. limit min to 20°C and the target temp. limit max. to 29°C of cooling mode.
{% endtab %}

{% tab title="GET" %}
The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="94.99999999999997"></th><th width="184"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>17 – Command code</td><td>17 – Command code</td></tr><tr><td>1</td><td> </td><td>XX – Heating target temp. limit min.</td></tr><tr><td>2</td><td></td><td>XX – Heating target temp. limit max.</td></tr><tr><td>3</td><td></td><td>XX - Cooling target temp. limit min.</td></tr><tr><td>4</td><td></td><td>XX - Cooling target temp. limit max.</td></tr></tbody></table>

**Example command:** 0x17;

**Example response:** 0x171018141D: \
– The target temp. limit min. is 16°C and the target temperature limit max. is 24°C of heating mode;\
– The target temp. limit min. is 20°C and the target temperature limit max. is 29°C of cooling mode.
{% endtab %}
{% endtabs %}

The allowed temperature range is 5...30°C (1°C resolution) for both heating and cooling mode.

## SET/GET target temperature range (single range for cooling and heating)

{% hint style="info" %}
These commands are available for devices with firmware versions ≤ 1.5 and ≥ 1.8
{% endhint %}

{% tabs %}
{% tab title="f.w. ≤ 1.5" %}
#### These commands are used to set/get the possible min. and max. target temperature values.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="155"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code.</td></tr><tr><td>1</td><td>XX – Lower temperature limit min.<br><strong>Default value:</strong> 0x00 (0°C).</td></tr><tr><td>2</td><td>XX – Upper temperature limit max.<br><strong>Default value:</strong> 0x28 (40°C).</td></tr></tbody></table>

**Example command:** 0x081018 – Sets the lower temp. limit to 16°C and the upper temp. limit to 24°C.
{% endtab %}

{% tab title="GET" %}
The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="133"></th><th width="183"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>15 – Command code</td><td>15 – Command code</td></tr><tr><td>1</td><td></td><td>XX - Lower temperature limit min.</td></tr><tr><td>2</td><td></td><td>XX - Upper temperature limit max.</td></tr></tbody></table>

**Example command:** 0x15;

**Example response:** 0x151018 – The lower temp. limit is 16°C and the upper temperature limit is 24°C.
{% endtab %}
{% endtabs %}

The allowed lower temperature range is 0...38°C (1°C resolution).

The allowed upper temperature range is 0...40°C (1°C resolution).
{% endtab %}

{% tab title="f.w. ≥ 1.8" %}
#### These commands are used to set the possible min. and max. target temperature values of heating and cooling mode.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="155"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code.</td></tr><tr><td>1</td><td>XX – Lower temperature limit min.<br><strong>Default value:</strong> 0x05 (5°C).</td></tr><tr><td>2</td><td>XX – Upper temperature limit max.<br><strong>Default value:</strong> 0x1E (30°C).</td></tr></tbody></table>

**Example command:** 0x081018 – Sets the lower temp. limit to 16°C and the upper temp. limit to 24°C.
{% endtab %}

{% tab title="GET" %}
The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="133"></th><th width="183"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>15 – Command code</td><td>15 – Command code</td></tr><tr><td>1</td><td></td><td>XX - Heating target temp. limit min.</td></tr><tr><td>2</td><td></td><td>XX - Heating target temp. limit max.</td></tr></tbody></table>

**Example command:** 0x15;

**Example response:** 0x151018 – The target temp. limit min. is 16°C and the target temperature limit max. is 24°C of heating mode;
{% endtab %}
{% endtabs %}

The allowed temperature range is 5...30°C (1°C resolution) for both heating and cooling mode.
{% endtab %}
{% endtabs %}

## SET/GET target temperature ranges - unoccupied

{% hint style="info" %}
These commands are available for devices with firmware version ≥ 1.6

Only available for applications with 3-speed fan.
{% endhint %}

These commands are used to set/get the possible min. and max. target temperature values of heating and cooling mode - unoccupied.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>76 – The command code.</td></tr><tr><td>1</td><td>XX – Heating target temp. limit min. - unoccupied.<br><strong>Default:</strong> 0x05 (5°C).</td></tr><tr><td>2</td><td>XX – Heating target temp. limit max. - unoccupied.<br><strong>Default:</strong> 0x1E (30°C).</td></tr><tr><td>3</td><td>XX – Cooling target temp. limit min. - unoccupied.<br><strong>Default:</strong> 0x05 (5°C).</td></tr><tr><td>4</td><td>XX – Cooling target temp. limit max. - unoccupied.<br><strong>Default:</strong> 0x1E (30°C).</td></tr></tbody></table>

**Example command:** 0x761018141D: \
– Sets the target temp. limit min to 16°C and the target temp. limit max. to 24°C of heating mode - unoccupied;\
– Sets the target temp. limit min to 20°C and the target temp. limit max. to 29°C of cooling mode - unoccupied.
{% endtab %}

{% tab title="GET" %}
The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="94.99999999999997"></th><th width="187"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>77 – Command code</td><td>77 – Command code</td></tr><tr><td>1</td><td> </td><td>XX – Heating target temp. limit min. - unoccupied.</td></tr><tr><td>2</td><td></td><td>XX – Heating target temp. limit max. - unoccupied.</td></tr><tr><td>3</td><td></td><td>XX - Cooling target temp. limit min. - unoccupied.</td></tr><tr><td>4</td><td></td><td>XX - Cooling target temp. limit max. - unoccupied.</td></tr></tbody></table>

**Example command:** 0x77;

**Example response:** 0x771018141D: \
– The target temp. limit min. is 16°C and the target temperature limit max. is 24°C of heating mode - unoccupied;\
– The target temp. limit min. is 20°C and the target temperature limit max. is 29°C of cooling mode - unoccupied.
{% endtab %}
{% endtabs %}

The allowed temperature range is 5...30°C (1°C resolution).
