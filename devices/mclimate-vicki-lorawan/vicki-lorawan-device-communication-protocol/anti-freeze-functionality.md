# Anti-freeze functionality

Vicki has a built-in anti-freeze functionality based on its internal temperature readings. You can set a certain temperature threshold and if the internally measured temperature crosses it the functionality will be activated/deactivated.

If the anti-freeze functionality is active the current target temperature is overwritten by the anti-freeze target temperature and a keep-alive message is sent to notify the server (bit 3 in byte 8 in the keep-alive packet is the flag for active/inactive functionality state).

{% hint style="info" %}
The anti-free target temperature can be set with a resolution of 1°C. When the anti-freeze functionality has been deactivated the previously set target temperature is restored.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
Set the anti-free functionality parameter values.

<table data-header-hidden><thead><tr><th width="136.33333333333331">Byte index</th><th width="94">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>49 – The command code.</td></tr><tr><td>1</td><td></td><td>XX - activation threshold temperature</td></tr><tr><td>2</td><td></td><td>XX - deactivation threshold temperature</td></tr><tr><td>3</td><td></td><td>XX - anti-freeze target temperature</td></tr></tbody></table>

**Example command:** 0x493C5A07

3C\[HEX] = 60\[DEC]\
Activation threshold = 60 / 10 = 6°C\
**Default value is 6°**\
If the temperature falls below 6°C Vicki will go into anti-freeze mode setting a new target temperature.

5A\[HEX] = 90\[DEC]\
Deactivation threshold = 90 / 10 = 9°C\
**Default value is 9°C**\
If the temperature goes over 9°C Vicki will resume normal operation and restore its previously configured target temperature.

07\[HEX] = 7\[DEC]\
Anti-freeze target temperature = 7°C\
**Default value is 7°C**
{% endtab %}

{% tab title="GET" %}
Get the anti-free functionality parameter values.

<table data-header-hidden><thead><tr><th width="97">Byte index</th><th width="134">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>4A – Command code.</td><td>4A – The command code.</td></tr><tr><td>1</td><td></td><td>XX - activation threshold temperature</td></tr><tr><td>2</td><td></td><td>XX - deactivation threshold temperature</td></tr><tr><td>3</td><td></td><td>XX - anti-freeze target temperature</td></tr></tbody></table>

**Example command response:** 0x4A3C5A07

3C\[HEX] = 60\[DEC]\
Activation threshold = 60 / 10 = 6°C\
**Default value is 6°C**

5A\[HEX] = 90\[DEC]\
Deactivation threshold = 90 / 10 = 9°C\
**Default value is 9°C**

07\[HEX] = 7\[DEC]\
Anti-freeze target temperature = 7°C\
**Default value is 7°C**
{% endtab %}
{% endtabs %}
