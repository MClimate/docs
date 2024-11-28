# Sensors measurement settings

## Sensors measurement blind time

When you press the button on the device, it measures temperature, humidity and light intensity. There is a period after each press that subsequent button presses are ignored in.

{% tabs %}
{% tab title="SET" %}
This command sets the the measuring blind time in minutes.

<table data-header-hidden><thead><tr><th width="131"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>46 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Measuring blind time in minutes.<br><strong>Default</strong> <strong>value 0x01=1min.</strong></td></tr></tbody></table>

**Example downlink**: 0x460E – when we separate the value of the time from the command code we get 0x**0E,** which is 14 min.
{% endtab %}

{% tab title="GET" %}
This command gets the currently set value in minutes.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="104"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>47 – The command code</td></tr><tr><td>1</td><td>-</td><td>Measuring blind time in minutes.</td></tr></tbody></table>

**Example command: 0x47**

**Example response:** 0x**47**0F – when we separate the value of the time from the command code we get 0x0&#x46;**,** which is 15 min.
{% endtab %}
{% endtabs %}

## Sensors measurement period

The commands sends the time between each sensor reading. The device takes a new reading every period and refreshes the data on the display.

{% tabs %}
{% tab title="SET" %}
Set the measurement period.

<table data-header-hidden><thead><tr><th width="139"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>48 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Measurement period in minutes.<br><strong>Default</strong> <strong>value 0x05=5min.</strong> Value 0x00 isn’t applicable.</td></tr></tbody></table>

**Example command**: 0x480A – Set the measurement period the 0x0A=10min.
{% endtab %}

{% tab title="GET" %}
Get the measurement period.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>49 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Measurement period in minutes.</td></tr></tbody></table>

**Example command: 0x49**

**Example command**: 0x**49**0A – when we separate the command code value we get the measurement period of 0x0A=10min.
{% endtab %}
{% endtabs %}
