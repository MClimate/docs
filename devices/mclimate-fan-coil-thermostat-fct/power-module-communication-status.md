# Power module communication status

{% tabs %}
{% tab title="GET" %}
When the power module communication status changes, the command is sent together with the next keepalive of the device. The keepalive data in the example below is omitted for clarity.

You can query the power module status at any time with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>75 – The command code.</td></tr><tr><td>1</td><td><p><strong>Occupancy sensor:</strong></p><p>00: Power module communication OK; </p><p>01: Power module communication error. </p></td></tr></tbody></table>

**Example downlink**: 0x7501 – Power module communication error.
{% endtab %}
{% endtabs %}

