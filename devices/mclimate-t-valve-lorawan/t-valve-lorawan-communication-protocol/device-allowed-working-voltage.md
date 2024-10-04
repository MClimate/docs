# Device allowed working voltage

This command sets the allowed working voltage. If the battery voltage drops below the set value the valve state is automatically set to open and can’t be changed anymore.

{% hint style="danger" %}
Setting a value less than 0x1F is not acceptable as it is not sufficient for the operation of the onboard MCU and/or radio!
{% endhint %}

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>09 – The command code</td></tr><tr><td>1</td><td>XX - Allowed working voltage<br>XX = (Voltage[mV] - 1600) / 8<br><strong>Default value is 1850mV</strong></td></tr></tbody></table>

**Example command:** 0x0932

32\[HEX] = 50\[DEC]

50 = (Voltage\[mV] - 1600) / 8\
Voltage\[mV] = 50 x 8 + 1600 = 400 + 1600 = 2000mV = 2V

Set the working voltage to 2 Volts
{% endtab %}

{% tab title="GET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>11 – The command code</td></tr><tr><td>1</td><td>XX - Allowed working voltage<br>XX = (Voltage[mV] - 1600) / 8</td></tr></tbody></table>

**Example response:** 0x111F

1F\[HEX] = 31\[DEC]

31 = (Voltage\[mV] - 1600) / 8\
Voltage\[mV] = 31 x 8 + 1600 = 248 + 1600 = 1848mV = 1.848V

The device will stop working when the voltage drops below 1.848V
{% endtab %}
{% endtabs %}
