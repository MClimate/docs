# Set LED behavior

This command controls the LEDs on the top cover of the device. You can select any of the 4 and adjust its light pattern and the time it on for.

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – The command code</td></tr><tr><td>1</td><td><em>XX – LED ID</em><br>00 - LED responsible for Open<br>01 - LED responsible for Close<br>02 - LED responsible for Leakage<br>03 - LED responsible for Flood</td></tr><tr><td>2</td><td><em>XX – LED behavior</em><br>01 - ON<br>02 - Blink fast<br>03 - Blink slow<br>04 - OFF</td></tr><tr><td>3</td><td>XX - duration for the specified LED behavior in seconds. If zero, do it until next LED related command is received or the verify button is pressed.</td></tr></tbody></table>

**Example command:** 0x02020214

02\[HEX] = 02\[DEC] -> activate the Leakage LED

02\[HEX] = 02\[DEC] -> make the LED Blink fast

14\[HEX] = 20\[DEC] -> make the LED Blink for 20 seconds
{% endtab %}
{% endtabs %}
