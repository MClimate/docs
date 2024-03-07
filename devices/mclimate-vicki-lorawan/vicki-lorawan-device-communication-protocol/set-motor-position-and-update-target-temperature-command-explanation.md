# Control target temperature and/or motor position and range

## Set target temperature with resolution 1.0°C

This command is applicable only in online automatic control mode or in online automatic control mode with external temperature reading. The command sets the temperature to be reached by the device internal control algorithm. It’s described in details in the table below.

<table data-header-hidden><thead><tr><th width="138.33333333333331">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0E – The command code.</td></tr><tr><td>1</td><td>XX – The desired temperature in Celsius degrees. The value must be inside the range of allowed device working temperatures (Set with command code 0x08).</td></tr></tbody></table>

**Example command:** 0x0E16 – sets the device target temperature to 22 Celsius degrees.

## Target temperature with resolution 0.1°C

{% tabs %}
{% tab title="SET" %}
The desired target temperature should be pre-multiplied by 10 to get the value to be send.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>51 – The command code.</td></tr><tr><td>1</td><td>XX - Tt [15:8]</td></tr><tr><td>2</td><td>XX - Tt [7-0]</td></tr></tbody></table>

Target temperature = Tt \[15:0] / 10

**Example command:** 0x510102 => Tt = 0102\[HEX]=258\[DEC]

Target temperature = 258 / 10 = 25.8

{% hint style="info" %}
The desired target temperature should be pre-multiplied by 10 to get the value to be sent.\
If later the target temperature is adjusted manually by rotating the device outer ring, the new value will be with accuracy 1.0°C
{% endhint %}
{% endtab %}

{% tab title="GET" %}
This command response is automatically prepended to the keep-alive message when the target temperature isn't integer. The device will not respond to server requests with command code 0x52.

<table data-header-hidden><thead><tr><th width="132.66666666666666">Byte index</th><th width="149">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>52 – Command code.</td><td>52 – The command code.</td></tr><tr><td>1</td><td></td><td>XX - Tt [15:8]</td></tr><tr><td>2</td><td></td><td>XX - Tt [15:8]</td></tr></tbody></table>

**Example response:** 0x520102 => Tt = 0102\[HEX]=258\[DEC]

Target temperature = 258 / 10 = 25.8
{% endtab %}
{% endtabs %}

## Set valve openness in percentage

{% tabs %}
{% tab title="SET" %}
The desired valve openness in percentage.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>4E – The command code.</td></tr><tr><td>1</td><td>XX - Valve openness percentage</td></tr></tbody></table>

**Example command:** 0x4E0A

0A\[HEX] = 10 \[DEC] = 10%

The valve will open 10% of its maximum capabilities.
{% endtab %}
{% endtabs %}

## Valve openness range in percentage

The effective device motor range is used to limit the valve open and close by the internal PI control algorithm. Thus, it's not used when the device operates in "Manual control" mode.

{% hint style="info" %}
By default this range is set to 100% for both parameters, making it possible for the valve to be closed and opened entirely.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
The desired range in percentage.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>45 – The command code.</td></tr><tr><td>1</td><td>XX - Mar parameter<br>Default is 0x00</td></tr><tr><td>2</td><td>XX - Mir parameter<br>Default is 0x64</td></tr></tbody></table>

Max openness \[%] = 100-Mar

Min openness \[%] = Mir

**Example command:** 0x450A5A

Mar = 0A\[HEX] = 10\[DEC] => Max openness = 100-10=90%\
The int. PI algorithm will be capable to **open the valve** to 90% of the motor range.

Min = 5A\[HEX] = 90\[DEC] => Min openness = 90%\
The int. PI algorithm will be capable to **close the valve** to 90% of the motor range.&#x20;

{% hint style="info" %}
Not allowed to set values that result in Min - Max < 10%.
{% endhint %}
{% endtab %}

{% tab title="GET" %}
This command gets the openness range to which the valve can be opened.

<table data-header-hidden><thead><tr><th width="132.66666666666666">Byte index</th><th width="149">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>50 – Command code.</td><td>50 – The command code.</td></tr><tr><td>1</td><td></td><td>XX - Mar parameter</td></tr><tr><td>2</td><td></td><td>XX - Mir parameter</td></tr></tbody></table>

**Example response:** 0x500064&#x20;

Max openness \[%] = 100-Mar

Min openness \[%] = Mir

Mar = 00\[HEX] = 00\[DEC] => Max openness = 100-0 =100%\
The int. PI algorithm will be capable to **open the valve** fully.

Min = 64\[HEX] = 100\[DEC] => Min openness = 100%\
The int. PI algorithm will be capable to **close the valve** fully.
{% endtab %}
{% endtabs %}

## Set motor position and update target temperature command explanation

In the table below is described the data which the server sends to Vicki to set new target temperature and new motor position.

<table data-header-hidden><thead><tr><th width="133">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>31 – The command will set Vicki motor position and target temperature</td></tr><tr><td>1</td><td>XX – Motor position in steps – MSB</td></tr><tr><td>2</td><td>XX – Motor position in steps – LSB</td></tr><tr><td>3</td><td><p>XX – Target temperature to be shown on the LED display when the rotary encoder is moved.</p><p>Currently 0x05 &#x3C;= XX &#x3C;= 0x1E</p></td></tr></tbody></table>

**Example command:** 0x31012C1D – Set Vicki motor position to 300 and target temperature to 29.

{% hint style="danger" %}
When moving the valve, make sure the difference between the current motor position and the desired motor position is >= 17 steps! If you specify a lower amount of steps, the device will misbehave!
{% endhint %}

## Set motor position only

{% hint style="info" %}
This feature is available in firmware >= 4.0
{% endhint %}

This command is used to set desired motor position. It can be used when the temperature control is managed by the server. The allowed motor position to set is limited internally to 800 steps (0x0320).

<table data-header-hidden><thead><tr><th width="137"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>2D – The command code.</td></tr><tr><td>1</td><td>XX – Motor position in steps - MSB.</td></tr><tr><td>2</td><td>XX – Motor position in steps – LSB.</td></tr></tbody></table>

{% hint style="danger" %}
When moving the valve, make sure the difference between the current motor position and the desired motor position is >= 17 steps! If you specify a lower amount of steps, the device will misbehave!
{% endhint %}

Example command, \[Hex]: 0x2D01F4 – Set the motor position to 500 steps.
