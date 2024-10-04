# Request Long data packet

This command requests from the device a Long Keep-alive data packet that provides more information on its state.

{% hint style="warning" %}
The packet is not generated immediately, but replaces the next short keep-alive packet (it effectively is sent when the time for the next keep-alive has elapsed).
{% endhint %}

{% tabs %}
{% tab title="GET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code</td></tr></tbody></table>
{% endtab %}
{% endtabs %}
