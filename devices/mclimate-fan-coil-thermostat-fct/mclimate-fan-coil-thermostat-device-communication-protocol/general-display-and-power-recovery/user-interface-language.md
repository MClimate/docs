# User interface language

{% hint style="info" %}
This command is available for devices with firmware version ≥ 1.8.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
This command is used to set the user interface language.

<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>9A – The command code.</td></tr><tr><td>1</td><td><p>00 – English;  <strong>Default</strong>.</p><p>01 – French. </p></td></tr></tbody></table>

**Example command:** 0x9A01 – The server sets the user interface language French.
{% endtab %}

{% tab title="GET" %}
This command is used to get the user interface language.

<table data-header-hidden><thead><tr><th width="99.99999999999997">Byte index</th><th width="168">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>9B – Command code.</td><td>9B – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – English; </p><p>01 – French. </p></td></tr></tbody></table>

**Example command:** 0x9B;

**Example response:** 0x9B01 - The user interface language is French.
{% endtab %}
{% endtabs %}
