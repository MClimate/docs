# Set flood alarm time

This command sets how long will the flood alarm be on for, in case of the event happening.

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>06 – The command code</td></tr><tr><td>1</td><td>XX - Alarm time in seconds (resolution of 10 seconds). A zero value is forbidden. <strong>Default value is 30 (5 minutes).</strong></td></tr></tbody></table>

**Example command:** 0x0606

06\[HEX] = 06\[DEC] -> Set the alar time to 6x10s = 60s = 1min

In  case of a flood the alarm will be on for 1 minute.
{% endtab %}
{% endtabs %}
