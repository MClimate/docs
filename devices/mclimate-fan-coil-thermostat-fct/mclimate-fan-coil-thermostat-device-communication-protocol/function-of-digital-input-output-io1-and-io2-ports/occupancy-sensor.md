# Occupancy sensor

In case you've decided to fit an occupancy sensor, below you can find additional commands to adjust the set-point (in case of heating or cooling) and the fan speed when the room is unoccupied.

## Cooling set-point unoccupied&#x20;

You can change the cooling set-point with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the cooling set-point with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>56 – The command code.</td></tr><tr><td>1</td><td>XX – Cooling set-point value.<br><strong>Default value:</strong> 0x19 (25°C)</td></tr></tbody></table>

**Example downlink**: 0x5617 – Sets the cooling set-point to 0x17 - 23°C.
{% endtab %}

{% tab title="GET" %}
#### This command gets the cooling setpoint. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>57 – Command code</td><td>57 – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - Cooling setpoint value.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x57;

**Example command:** 0x5717 – The cooling setpoint is 0x17 - 23°C
{% endtab %}
{% endtabs %}

The allowed cooling set-point range is 5...30°C (1°C  resolution) by default.

## Heating set-point unoccupied

You can change the heating set-point with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the heating set-point with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>58 – The command code.</td></tr><tr><td>1</td><td>XX – Heating set-point value.<br><strong>Default value:</strong> 0x11 (17°C)</td></tr></tbody></table>

**Example downlink**: 0x5814 – Sets the heating set-point to 0x14 - 20°C.
{% endtab %}

{% tab title="GET" %}
#### This command gets the heating setpoint. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>59 – Command code</td><td>59 – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - Heating setpoint value.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x59;

**Example command:** 0x5914 – The heating setpoint is 0x14 - 20°C
{% endtab %}
{% endtabs %}

The allowed heating set-point range is 5...30°C (1°C  resolution) by default.

## Fan Speed unoccupied

You can change the fan speed with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the fan speed with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>5C – The command code.</td></tr><tr><td>1</td><td>00: Low.<br><strong>Default value.</strong><br>01: Automatic.<br>02: Do not change.</td></tr></tbody></table>

**Example downlink**: 0x5C01 – Sets the fan speed to 0x01: Automatic fan speed.
{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5D – Command code</td><td>5D – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - Fan speed value.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x5D;

**Example command:** 0x5D01 – The fan speed is 0x01: Automatic fan speed.
{% endtab %}
{% endtabs %}

