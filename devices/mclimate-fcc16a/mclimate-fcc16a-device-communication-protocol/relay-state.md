# Relay state

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="146"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>C1 – The command code.</td></tr><tr><td>1</td><td><p>00 – OFF; <strong>Default state</strong>.</p><p>01 – ON. </p></td></tr></tbody></table>

**Example downlink:** 0xC101 – Turn on the relay.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>B1 – Command code</td><td>B1 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The relay is off;<br>01 - The relay is on;</td></tr></tbody></table>

**Example downlink sent by the server:** 0xB1;

**Example command response:** 0xB101 – The relay is on.
{% endtab %}
{% endtabs %}

