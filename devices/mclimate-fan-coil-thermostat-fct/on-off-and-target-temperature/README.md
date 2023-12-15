# ON/OFF & Target temperature

## Device ON/OFF status

You can change the device ON/OFF status with the following command set.

{% tabs %}
{% tab title="SET" %}
#### Set the status of the device.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>66 – The command code.</td></tr><tr><td>1</td><td>00: Turn off the device. <strong>Default value.</strong><br>01: Turn on the device.</td></tr></tbody></table>

**Example command:** 0x6601 – Turn on the device.
{% endtab %}

{% tab title="GET" %}
#### Get the status of the device.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>67 – Command code</td><td>67 – Command code</td></tr><tr><td>1</td><td> </td><td>00: The device is off.<br>01: The device is on.</td></tr></tbody></table>

**Example command:** 0x67;

**Example response:** 0x6701 – The device is on.
{% endtab %}
{% endtabs %}

## Changing the current operational mode

Information on how to change between Heating/Cooling/Ventilation is available [here](../wiring-diagrams-applications-and-operational-modes.md#allowed-operational-modes).

## Target temperature

You can change the target temperature with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the target temperature with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>2E – The command code.</td></tr><tr><td>1</td><td>XX - T[15:8].</td></tr><tr><td>2</td><td>XX - T[7:0].</td></tr></tbody></table>

T\[15:0] = Ttarget\[°C] \* 10;

**Example command**: 0x2E0102;

Set target temperature - 25,8°C \* 10 = 258 \[DEC]  => 0x0102 \[HEX].
{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>2F – Command code</td><td>2F – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - T[15:8].</td></tr><tr><td>2</td><td></td><td>XX - T[7:0].</td></tr></tbody></table>

Ttarget\[°C] = T\[15:0] / 10;

**Example command:** 0x2F;

**Example response:** 0x2F0102;

0x0102 \[HEX] = 258 \[DEC] => Ttarget = 258 / 10 = 25,8°C.
{% endtab %}
{% endtabs %}

The allowed target temperature range is 0...40°C (0.1°C resolution).

## **Manual change from the thermostat's buttons**

This command lets the Application Server that the target temperature has been manually (physically) changed from the device - the button on the devices has been pressed, setting a specific target temperature .

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>30 – Command code</td></tr><tr><td>1</td><td>XX - T[15:8].</td></tr><tr><td>2</td><td>XX - T[7:0].</td></tr></tbody></table>

Ttarget\[°C] = T\[15:0] / 10;

**Example uplink**: 0x300102;

0x0102 \[DEC] = 258 \[DEC] => Ttarget = 258 / 10 = 25,8°C.

## Configuring the target temperature step

You can change the target temperature step, when buttons are used. E.g. when the current target temperature is 22.0C and the step is 0.5C, if the user clicks the up button once, the target temperature will become 22.5C

{% tabs %}
{% tab title="SET" %}
#### You can set the target temperature step with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>03 – The command code.</td></tr><tr><td>1</td><td>XX - Tstep[°C] * 10. <strong>Default value:</strong> 0x05 (0,5°C)</td></tr></tbody></table>

**Example command**: 0x030F;

Sets the temperature step - 1,5°C \* 10 = 15 \[DEC] => 0x0F \[HEX].


{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature step. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>05 – Command code</td><td>05 – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - Tstep[°C] * 10.</td></tr></tbody></table>

**Example command:** 0x05;

**Example response:** 0x050F;

0x0F - convert to DEC 15 => Tstep = 15 / 10 = 1,5°C.
{% endtab %}
{% endtabs %}

The allowed target temperature step range is 0.1...10°C (0.1°C max resolution).

### Measured temperature sensor compensation

{% hint style="info" %}
This is applies to the measured temperature.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
#### This command is used to set the compensation temperature values.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>5A – The command code.</td></tr><tr><td>1</td><td>00: Positive compensation.<br>01: Negative compensation.</td></tr><tr><td>2</td><td>XX - Tcomp[°C] * 10. <strong>Default value:</strong> 0x00 (0°C).</td></tr></tbody></table>

**Example command:** 0x5A0115;

Set the negative temp. compensation - 0x01\[HEX].

Set the compensation temperature - 2,1°C \* 10 = 21\[DEC] => 0x15\[HEX].
{% endtab %}

{% tab title="GET" %}
#### This command is used to get the compensation temperature values.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5B – Command code</td><td>5B – Command code</td></tr><tr><td>1</td><td> </td><td>00: Compensation is positive.<br>01: Compensation is negative.</td></tr><tr><td>2</td><td></td><td>XX - Tcomp[°C] * 10.</td></tr></tbody></table>

Tcomp\[°C] = XX / 10;

**Example command:** 0x15;

**Example response:** 0x5B0115;&#x20;

0x01 - The compensation is negative.

Convert 0x15\[HEX] = 21\[DEC] => Tcomp = 21 / 10 = 2,1°C.
{% endtab %}
{% endtabs %}

**Note:** The allowed range is -5...5°C (0,1°C resolution).
