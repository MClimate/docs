# Uplink types

{% tabs %}
{% tab title="SET" %}
### Set uplink messages type command explanation.

This command is used to set the uplink message type.&#x20;



| **Byte index** | **Hex value – Meaning**                                                                                              |
| -------------- | -------------------------------------------------------------------------------------------------------------------- |
| 0              | 17 – The command code.                                                                                               |
| 1              | <p>00 – sends unconfirmed uplink messages; <strong>Default</strong></p><p>01 – sends confirmed uplink messages. </p> |

**Example command:** 0x1701 – Sets the message type to be confirmed
{% endtab %}

{% tab title="GET" %}
### Get uplink messages type command explanation

This command is used to get the uplink messages type.



| **Byte index** | **Sent request**   | **Received response**                                                            |
| -------------- | ------------------ | -------------------------------------------------------------------------------- |
| 0              | 18 – Command code. | 18 – The command code.                                                           |
| 1              |                    | <p>00 – unconfirmed uplinks are used;</p><p>01 – confirmed uplinks are used.</p> |

**Example command sent from server:** 0x18;

**Example command response:** 0x1800 => The device uses unconfirmed messages
{% endtab %}
{% endtabs %}
