# Control target temperature and/or motor position

## Set device target temperature command explanation.

This command is applicable only in online automatic control mode or in online automatic control mode with external temperature reading. The command sets the temperature to be reached by the device internal control algorithm. It’s described in details in Table 15.

<table data-header-hidden><thead><tr><th width="138.33333333333331">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0E – The command code.</td></tr><tr><td>1</td><td>XX – The desired temperature in Celsius degrees. The value must be inside the range of allowed device working temperatures (Set with command code 0x08).</td></tr></tbody></table>

Table 15

**Example command:** 0x0E16 – sets the device target temperature to 22 Celsius degrees.

## Set motor position and update target temperature command explanation

In Table 8 is described the data which the server sends to Vicki to set new target temperature and new motor position.

<table data-header-hidden><thead><tr><th width="133">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>31 – The command will set Vicki motor position and target temperature</td></tr><tr><td>1</td><td>XX – Motor position in steps – MSB</td></tr><tr><td>2</td><td>XX – Motor position in steps – LSB</td></tr><tr><td>3</td><td><p>XX – Target temperature to be shown on the LED display when the rotary encoder is moved.</p><p>Currently 0x05 &#x3C;= XX &#x3C;= 0x1E</p></td></tr></tbody></table>

Table 8

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
