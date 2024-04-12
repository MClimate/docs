# Enable/disable manual valve open/close

This command sets whether one can use the open/close buttons to either open or close the valve.

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>05 – The command code</td></tr><tr><td>1</td><td>XX[0] - Set it to 1 to enable manual valve open. Set it to 0 to disable it.<br><strong>Default value is 1 (enabled)</strong><br>XX[1] - Set it to 1 to enable the manual valve close. Set it to 0 to disable it. <strong>Default value is 1 (enabled)</strong><br>XX[7:2] - Reserved</td></tr></tbody></table>

**Example command:** 0x0501

01\[HEX] = 00000001\[BIN]\
\[0] = 1 -> Manual open enabled\
\[1] = 0 -> Manual close disabled

**Example command:** 0x0502

01\[HEX] = 00000010\[BIN]\
\[0] = 0-> Manual open disabled\
\[1] = 1 -> Manual close enabled
{% endtab %}
{% endtabs %}
