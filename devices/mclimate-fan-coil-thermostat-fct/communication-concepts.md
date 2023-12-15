# Communication concepts

## Communication concepts related to the device's operation

{% hint style="info" %}
The device sends uplink on the following occasions:

1. Periodic uplink - every keepalive period.
2. Immediate uplink - when target temperature, fan speed, operation mode or device ON/OFF status is changed.
{% endhint %}

MClimate Fan Coil Thermostat (FCT) periodically sends messages (keep-alive commands) to the LNS. This is a Class C device, according to the LoRaWAN 1.0.3 specification, meaning it sends regular uplinks and you can send a downlink at any time, as the device constantly listens for LoRaWAN messages.

The messages are restricted by the LoRaWAN duty cycle requirements. The FCT can send both confirmed/unconfirmed uplink messages depending on its configuration.&#x20;

When a downlink is sent to the Fan Coil Thermostat, it can be either confirmed or unconfirmed. For critical messages (e.g. initial parameters setup), we recommend using confirmed downlinks, so that the LNS can take care of repetition if required and successful delivery can be verified.&#x20;

{% hint style="success" %}
**Downlink fports:** 1, 2, 4-224
{% endhint %}

One downlink packet from the LNS may contain multiple commands for the FCT to optimise the communication efficiency. These downlinks can combine both multiple write and/or read commands. Response to the GET commands will be sent in the next uplink.

When the LNS wants to read data from the device, the corresponding command code or command codes are sent to the device and the response will be sent together with the next keep-alive message. If the combined length of the command responses and the keep-alive packet is longer than the allowed by the LoRaWAN MAC layer application payload size, the keep-alive packet will be omitted and only the command responses will be sent by the FCT.

**When the LNS writes device configuration data with a command, the data is stored in the device non-volatile memory, so there is no need to send this command again on the next network join.**

The aforementioned communication method and the payload structure is described in Table 1.

| **Payload byte index** | **Meaning**                  |
| ---------------------- | ---------------------------- |
| 0                      | Command 0 meaning            |
| 1                      | Command 0 data - optional    |
| i                      | Command 1 meaning - optional |
| i+1                    | Command 1 data - optional    |
| j                      | Command 2 meaning- optional  |
| j+1                    | Command 2 data - optional    |
| ...                    | ...                          |
| k                      | Command x meaning- optional  |
| k+1                    | Command x data - optional    |

_Table 1._
