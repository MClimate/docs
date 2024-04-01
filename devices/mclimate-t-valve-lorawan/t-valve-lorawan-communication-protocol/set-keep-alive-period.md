# Set keep-alive period

This command sets the keep-alive period.

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>07 – The command code</td></tr><tr><td>1</td><td>XX - Keep live period in minutes (resolution is 1 minutes)<br><strong>Default value is 5 minutes</strong></td></tr></tbody></table>

**Example command:** 0x070A

0A\[HEX] = 10\[DEC] -> Set the keep-alive period to 10 minutes
{% endtab %}
{% endtabs %}
