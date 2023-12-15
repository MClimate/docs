# Uplink types

{% tabs %}
{% tab title="SET" %}
### Set uplink messages type command explanation.

This command is used to set Wireless Thermostat uplink message type.&#x20;



<table data-header-hidden><thead><tr><th width="131">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>11 – The command code.</td></tr><tr><td>1</td><td><p>00 – Wireless Thermostat sends unconfirmed uplink messages; <strong>Default</strong>.</p><p>01 – Wireless Thermostat sends confirmed uplink messages. </p></td></tr></tbody></table>

**Example command:** 0x1101 – The server sets the uplink message type to confirmed.
{% endtab %}

{% tab title="GET" %}
### Get uplink messages type command explanation

This command is used to get Wireless Thermostat uplink messages type. Server sends the command code and the response is sent from the Wireless Thermostat together with the next keep-alive command. The keep-alive in the example is omitted for clarity.



<table data-header-hidden><thead><tr><th width="137.99999999999997">Byte index</th><th width="192">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1B – Command code.</td><td>1B – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – Wireless Thermostat uses unconfirmed uplinks uplinks;</p><p>01 – Wireless Thermostat uses confirmed uplinks.</p></td></tr></tbody></table>

**Example command sent from server:** 0x1B;

**Example command response:** 0x1B00 => Wireless Thermostat sends unconfirmed uplinks
{% endtab %}
{% endtabs %}



