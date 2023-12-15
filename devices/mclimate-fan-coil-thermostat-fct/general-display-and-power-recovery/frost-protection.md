# Frost Protection

The frost protection feature is developed to keep your building's structural integrity safe in case of decreasing temperatures.

The logic behind the **Frost Protection** is as follows:

* If the Frost protection is enabled AND
* If the Measured Temperature < Frost Protection Temperature Threshold, THEN
  * If the device is off, it turns on
  * Set-point is set to Frost Protection Set-Point
  * Device switches to heating (IF AVAILABLE as per the applications (wiring diagrams))
  * An icon is shown on the display
  * Frost protection status is reflected in the keep-alive.

To exit the mode, you can:

* Either interact with the device's buttons (e.g. change target temp) OR
* Send a downlink to change target temp, on/off, mode, fan speed.
* If you exit the frost protection mode, but the measured temperature is below the Frost Protection Temperature Threshold, the function will reactivate and execute the protection steps again.

## Frost protection ON/OFF status

You can change the frost protection ON/OFF status with the following command set.

{% tabs %}
{% tab title="SET" %}
#### Set the frost protection status.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>4E – The command code.</td></tr><tr><td>1</td><td>00: Turn off the frost protection. <br>01: Turn on the frost protection. <strong>Default value.</strong></td></tr></tbody></table>

**Example command:** 0x4E01 – Turn on the frost protection.
{% endtab %}

{% tab title="GET" %}
#### Get the frost protection status.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>4F – Command code</td><td>4F – Command code</td></tr><tr><td>1</td><td> </td><td>00: The frost protection is off.<br>01: The frost protection is on.</td></tr></tbody></table>

**Example command:** 0x4F;

**Example response:** 0x4F01 – The frost protection is on.
{% endtab %}
{% endtabs %}

## Frost protection set-point and threshold temperature

This command is used to set the frost protection set-point and threshold temperature values.

{% tabs %}
{% tab title="SET" %}
#### Set the frost protection set-point and threshold.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>50 – The command code.</td></tr><tr><td>1</td><td>XX – Threshold temperature value. <strong>Default value:</strong> 0x07 (7°C).</td></tr><tr><td>2</td><td>XX – Set-point temperature value. <strong>Default value:</strong> 0x08 (8°C).</td></tr></tbody></table>

**Example command:** 0x500609 – Sets the threshold temperature to 6°C and the Set-point temperature to 9°C.
{% endtab %}

{% tab title="GET" %}
#### Get the frost protection set-point and threshold.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>51 – Command code</td><td>51 – Command code</td></tr><tr><td>1</td><td> </td><td>XX – Threshold temperature value.</td></tr><tr><td>2</td><td></td><td>XX – Setpoint temperature value.</td></tr></tbody></table>

**Example command:** 0x51;

**Example response:** 0x510609 – The threshold temperature is 6°C and the setpoint temperature is 9°C.
{% endtab %}
{% endtabs %}

The allowed range is 0...20°C (1°C resolution).

## Frost protection status

When the frost protection status changes, the command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
#### You can read the frost protection status with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>6E – The command code.</td></tr><tr><td>1</td><td><p><strong>Occupancy sensor:</strong></p><p>   00: The frost protection is not running; </p><p>   01: The frost protection is running. </p></td></tr></tbody></table>

**Example downlink**: 0x6E01 – The frost protection running.
{% endtab %}
{% endtabs %}
