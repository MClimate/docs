# Uplink types



{% tabs %}
{% tab title="SET" %}
### Set uplink messages type command explanation.

This command is used to set Vicki sent uplink message type.&#x20;



| **Byte index** | **Hex value – Meaning**                                                                                                                                    |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0              | 11 – The command code.                                                                                                                                     |
| 1              | <p>00 – Vicki sends unconfirmed uplink messages; Default for f.w. >=3.5</p><p>01 – Vicki sends confirmed uplink messages. Default for f.w. &#x3C;= 3.4</p> |

**Example command:** 0x1101 – The server sets Vicki uplink message type to confirmed.
{% endtab %}

{% tab title="GET" %}
### Get uplink messages type command explanation

This command is used to get Vicki sent uplink messages type. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The keep-alive in the response is omitted for clarity.



| **Byte index** | **Sent request**   | **Received response**                                                              |
| -------------- | ------------------ | ---------------------------------------------------------------------------------- |
| 0              | 1B – Command code. | 1B – The command code.                                                             |
| 1              |                    | <p>00 – Vicki uplinks are unconfirmed;</p><p>01 – Vicki uplinks are confirmed.</p> |

**Example command sent from server:** 0x1B;

**Example command response:** 0x1B00 => Vicki sent uplinks are unconfirmed.
{% endtab %}
{% endtabs %}



