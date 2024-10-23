# Uplink types

{% tabs %}
{% tab title="SET" %}
#### This command is used to set  uplink message type.

<table data-header-hidden><thead><tr><th width="111">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>11 – The command code.</td></tr><tr><td>1</td><td><p>00 – The device sends unconfirmed uplink messages;<br><strong>Default</strong> message type for the device</p><p>01 – The device sends confirmed uplink messages.</p></td></tr></tbody></table>

**Example command:** 0x1101 – The server sets the uplink message type to confirmed.
{% endtab %}

{% tab title="GET" %}
#### This command is used to get uplink messages type.

<table data-header-hidden><thead><tr><th width="99.99999999999997">Byte index</th><th width="168">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1B – Command code.</td><td>1B – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – The device uses unconfirmed uplinks uplinks;</p><p>01 – The device uses confirmed uplinks.</p></td></tr></tbody></table>

**Example command:** 0x1B;

**Example response:** 0x1B00 - The device sends unconfirmed uplinks.

The keep-alive in the example above is omitted for clarity.
{% endtab %}
{% endtabs %}
