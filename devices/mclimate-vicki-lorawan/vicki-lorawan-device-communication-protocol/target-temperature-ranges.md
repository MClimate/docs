# Target temperature ranges

### Temperature ranges GET/SET commands explanation

{% tabs %}
{% tab title="SET" %}
### Set temperature ranges command explanation.

&#x20;This command is used to set the possible min. and max. target temperature values. In Table 11 is described the data the server sends to set these values.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>08 – The command code.</td></tr><tr><td>1</td><td>XX – lower temperature limit. Min. allowed/Default value: 0x05 (5 Celsius degrees).</td></tr><tr><td>2</td><td>XX – upper temperature limit. Max. allowed/Default value: 0x1E (30 Celsius degrees).</td></tr></tbody></table>

Table 11

**Example command:** 0x081018 – Sets the lower temp. limit to 16 Celsius degrees and the upper temp. limit to 24 Celsius degrees.
{% endtab %}

{% tab title="GET" %}
### Get temperature ranges command explanation

&#x20;This command is used to get Vicki possible min. and max. target temperature values. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The sent command request and the received command response are described in Table 22. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="92.33333333333331">Byte index</th><th width="149">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>15 – Command code.</td><td>15 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – Lower temperature limit in Celsius degrees.</td></tr><tr><td>2</td><td></td><td>XX – Upper temperature limit in Celsius degrees.</td></tr></tbody></table>

Table 22

**Example command sent from server:** 0x15;

**Example command response:** 0x15051E – The lower temp. limit is 5°C and the upper temperature limit is 30°C.
{% endtab %}
{% endtabs %}

