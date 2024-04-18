# Target Temperature & Temperature range

## Target temperature with resolution 0.1°C

{% hint style="info" %}
This command is available for devices with firmware version >= 1.4
{% endhint %}

You can change the target temperature with the following command set.

{% tabs %}
{% tab title="SET" %}
You can set the target temperature with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>50 – The command code.</td></tr><tr><td>1</td><td>XX - T[15:8].</td></tr><tr><td>2</td><td>XX - T[7:0].</td></tr></tbody></table>

T\[15:0] = Ttarget\[°C] \* 10;

**Example command**: 0x500102;

Set target temperature - 25,8°C \* 10 = 258 \[DEC]  => 0x0102 \[HEX].
{% endtab %}

{% tab title="GET" %}
This command gets the target temperature. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>51 – Command code</td><td>51 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - T[15:8].</td></tr><tr><td>2</td><td></td><td>XX - T[7:0].</td></tr></tbody></table>

Ttarget\[°C] = T\[15:0] / 10;

**Example command:** 0x51;

**Example response:** 0x510102;

0x0102 \[HEX] = 258 \[DEC] => Ttarget = 258 / 10 = 25,8°C.
{% endtab %}
{% endtabs %}

The allowed target temperature range is (5°C – 30°C) by default.

## Target temperature with resolution 1.0°C

You can change the target temperature with the following command set.

{% tabs %}
{% tab title="SET" %}
You can set the target temperature with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>2E – The command code.</td></tr><tr><td>1</td><td>XX – Target temperature value</td></tr></tbody></table>

**Example downlink**: 0x2E17 – Sets the target temperature to 0x17 = 23°C.
{% endtab %}

{% tab title="GET" %}
This command gets the target temperature. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>2F – Command code</td><td>2F – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Target temperature value</td></tr></tbody></table>

**Example downlink sent by the server:** 0x2F;

**Example command:** 0x2F1B – The target temperature is 0x1B = 27°C.
{% endtab %}
{% endtabs %}

The allowed target temperature range is (5°C – 30°C) by default.

## Manual change from the thermostat's buttons

With this command your application server can understand when the target temperature has been manually changed from the device physically - somebody clicked the buttons on the device and set a specific target temp.

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

* _**Manual target temperature change with resolution 0.1°C.**_

{% hint style="info" %}
This command is available for devices with firmware version >= 1.4
{% endhint %}

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>54 – Command code</td></tr><tr><td>1</td><td>XX - T[15:8].</td></tr><tr><td>2</td><td>XX - T[7:0].</td></tr></tbody></table>

Tmanual\[°C] = T\[15:0] / 10;

**Example command:** 0x540102;

0x0102 \[HEX] = 258 \[DEC] => Tmanual = 258 / 10 = 25,8°C.



* _**Manual target temperature change with resolution 1.0°C.**_

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>30 – Command code</td></tr><tr><td>1</td><td>17 - Target temperature is manually set to 23°C.</td></tr></tbody></table>

## Target temperature range

You can change the range of selection of target temperature on the device. By default, the user can select between 5 and 30 degrees Celsius.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code.</td></tr><tr><td>1</td><td>XX – lower temperature limit. Min. allowed/ Default value: 0x05 (5°C).</td></tr><tr><td>2</td><td>XX – upper temperature limit. Max. allowed/ Default value: 0x1E (30°C).</td></tr></tbody></table>

**Example downlink**: 0x081018 – Sets the lower temp. limit to 16°C and the upper temp. limit to 24°C.
{% endtab %}

{% tab title="GET" %}
This command is used to get the possible min. and max. target temperature values. Server sends the command code as a downlink and the response is sent from the device together with the next keep-alive command. The keepalive data is omitted from the response for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>15 – Command code</td><td>15 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Min. target temperature value.</td></tr><tr><td>2</td><td></td><td>XX - Max. target temperature value.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x15;

**Example command:** 0x15051E – The lower temp. limit is 5°C and the upper temperature limit is 30°C.
{% endtab %}
{% endtabs %}

## Delay on target temperature change

Since people usually take some time to decide on a target temperature, we wait for a certain period after the last change before the device sends an immediate uplink.

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

**Note:** Acceptable values: 0...255sec. (1sec. resolution).

## Configuring the target temperature step

{% hint style="info" %}
This command is available for devices with firmware version >= 1.4
{% endhint %}

You can change the target temperature step, when buttons are used. E.g. when the current target temperature is 22.0°C and the step is 0.5°C, if the user clicks the up button once, the target temperature will become 22.5°C

{% tabs %}
{% tab title="SET" %}
You can set the target temperature step with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>52 – The command code.</td></tr><tr><td>1</td><td>XX - Tstep[°C] * 10.  <strong>Default value:</strong> 0x05 (0.5°C)</td></tr></tbody></table>

**Example command**: 0x520F;

Sets the temperature step - 1.5°C \* 10 = 15 \[DEC] => 0x0F \[HEX].
{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature step. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>53 – Command code</td><td>53 – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - Tstep[°C] * 10.</td></tr></tbody></table>

**Example command:** 0x53;

**Example response:** 0x530F;

0x0F - convert to DEC 15 => Tstep = 15 / 10 = 1.5°C.
{% endtab %}
{% endtabs %}

**Note:** Acceptable values: 0.1...10°C (0.1°C resolution).

## Temperature hysteresis

{% hint style="info" %}
This command is available for devices with firmware version >= 1.4
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="136"></th><th></th></tr></thead><tbody><tr><td><strong>Byte Index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>4E - The command code</td></tr><tr><td>1</td><td>XX = Temperature hysteresis value, multiplied by 10. <strong>Default value:</strong> 0x02 (0.2°C)</td></tr></tbody></table>

**Example downlink:**

0x4E03 - sets the temperature hysteresis to 0.3°C.
{% endtab %}

{% tab title="GET" %}
<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>4F – The command code.</td><td>4F – The command code.</td></tr><tr><td>1</td><td> </td><td>XX - Temperature hysteresis value, multiplied by 10.</td></tr></tbody></table>

**Example uplink:**

0x4F03 - The temperature hysteresis is 0.3°C.
{% endtab %}
{% endtabs %}

**Note:** Acceptable values: 0.1...25.5°C (0.1°C resolution).

### Measured temperature sensor compensation

{% hint style="info" %}
This command is available for devices with firmware version >= 1.4

This is applies to the measured temperature.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
This command is used to set the compensation temperature values.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>55 – The command code.</td></tr><tr><td>1</td><td>00: Positive compensation.<br>01: Negative compensation.</td></tr><tr><td>2</td><td><p>XX - Tcomp[°C] * 10. <strong>Default value: 0x0000</strong> (0°C). </p><p></p></td></tr></tbody></table>

**Example command:** 0x550115;

Set the negative temp. compensation - 0x01\[HEX].

Set the compensation temperature - 2.1°C \* 10 = 21\[DEC] => 0x15\[HEX].
{% endtab %}

{% tab title="GET" %}
#### This command is used to get the compensation temperature values.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>56 – Command code</td><td>56 – Command code</td></tr><tr><td>1</td><td> </td><td>00: Compensation is positive.<br>01: Compensation is negative.</td></tr><tr><td>2</td><td></td><td>XX - Tcomp[°C] * 10.</td></tr></tbody></table>

Tcomp\[°C] = XX / 10;

**Example command:** 0x56;

**Example response:** 0x560115;&#x20;

0x01 - The compensation is negative.

Convert 0x15\[HEX] = 21\[DEC] => Tcomp = 21 / 10 = 2,1°C.
{% endtab %}
{% endtabs %}

**Note:** The allowed range is -5...5°C (0.1°C resolution).
