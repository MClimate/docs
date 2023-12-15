# Target Temperature & Temperature range

## Target temperature

You can change the target temperature with the following command set.

{% tabs %}
{% tab title="SET" %}
You can set the target temperature with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>2E – The command code.</td></tr><tr><td>1</td><td>XX – Target temperature value</td></tr></tbody></table>

**Example downlink**: 0x2E17 – Sets the target temperature to 0x17=23°C
{% endtab %}

{% tab title="GET" %}
This command gets the target temperature. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>2F – Command code</td><td>2F – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Target temperature value</td></tr></tbody></table>

**Example downlink sent by the server:** 0x2F;

**Example command:** 0x2F1B – The target temperature is 0x1B=27°C
{% endtab %}
{% endtabs %}

The allowed target temperature range is (5°C – 30°C) by default.

## Manual change from the thermostat's buttons

With this command your application server can understand when the target temperature has been manually changed from the device physically - somebody clicked the buttons on the device and set a specific target temp.

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>30 – Command code</td></tr><tr><td>1</td><td>17 - Target temperature is manually set to 23°C</td></tr></tbody></table>

## Target temperature range

You can change the range of selection of target temperature on the device. By default, the user can select between 5 and 30 degrees Celsius.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code.</td></tr><tr><td>1</td><td>XX – lower temperature limit. Min. allowed/Default value: 0x05 (5 Celsius degrees).</td></tr><tr><td>2</td><td>XX – upper temperature limit. Max. allowed/Default value: 0x1E (30 Celsius degrees).</td></tr></tbody></table>

**Example downlink**: 0x081018 – Sets the lower temp. limit to 16 Celsius degrees and the upper temp. limit to 24 Celsius degrees
{% endtab %}

{% tab title="GET" %}
This command is used to get the possible min. and max. target temperature values. Server sends the command code as a downlink and the response is sent from the device together with the next keep-alive command. The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>15 – Command code</td><td>15 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Min. target temperature value</td></tr><tr><td>2</td><td></td><td>XX - Max. target temperature value</td></tr></tbody></table>

**Example downlink sent by the server:** 0x15;

**Example command:** 0x15051E – The lower temp. limit is 5°C and the upper temperature limit is 30°C.
{% endtab %}
{% endtabs %}

## Delay on target temperature change

Since people usually take some time to decide on a target temperature, we wait for a certain period after the last change before the device sends an immediate uplink.

The allowed delay range that can be set is 0 seconds – 255 seconds.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="136"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>35 – The command code.</td></tr><tr><td>1</td><td>XX – Time delay in seconds. <strong>The default value is 10sec.</strong></td></tr></tbody></table>

**Example command:** 0x350F – The delay that is set is 15sec.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>36 – Command code</td><td>36 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Delay for sending the target temperature</td></tr></tbody></table>

Example downlink sent from server: 0x36;

Example uplink response: 0x360F – The delay for sending the target temperature is 15sec.
{% endtab %}
{% endtabs %}

