# Uplink types

{% hint style="info" %}
NOTE: Available for firmware version 1.5 or later.
{% endhint %}

### Uplink messages type command explanation

Those commands allow you to manage the **periodic uplink** type of the device - confirmed or unconfirmed.

{% tabs %}
{% tab title="SET" %}
This command is used to set the device uplink message type.

<table><thead><tr><th width="134">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>11 – The command code.</td></tr><tr><td>1</td><td><p>00 – The device sends unconfirmed uplink messages; <strong>Default</strong>.</p><p>01 – The device sends confirmed uplink messages. </p></td></tr></tbody></table>

**Example command, \[Hex]:** 1101 – The server sets the uplink message type to confirmed.
{% endtab %}

{% tab title="GET" %}
This command is used to get the device uplink messages type. Server sends the command code and the response is sent from the device together with the next keep-alive command. The keep-alive in the example is omitted for clarity.



<table data-header-hidden><thead><tr><th width="137.99999999999997">Byte index</th><th width="188">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1B – The command code.</td><td>1B – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – The device uses unconfirmed uplinks;</p><p>01 – The device uses confirmed uplinks.</p></td></tr></tbody></table>

**Example command sent from server, \[Hex]:** 1B;

**Example command response, \[Hex]:** 1B00 - The device sends unconfirmed uplinks.
{% endtab %}
{% endtabs %}

One can set a different uplink type when flood is detected. More info, [here](flood-event-available-configurations.md#flood-event-uplink-messages-type).
