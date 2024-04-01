# Reload emergency openings

This command sets the allowed emergency openings of the valve.

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>04 – The command code</td></tr><tr><td>1</td><td>XX - Number of allowed emergency openings.<br><strong>Maximum: 15 times</strong></td></tr></tbody></table>

**Example command:** 0x040A

0A\[HEX] = 10\[DEC] -> Set the allowed emergency openings to 10 times
{% endtab %}
{% endtabs %}
