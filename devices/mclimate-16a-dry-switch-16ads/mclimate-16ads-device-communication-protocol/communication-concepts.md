# Communication concepts

## Communication concepts related to the device's operation

MClimate 16ADS periodically sends messages (keep-alive) to the LNS. This is a Class C device, according to the LoRaWAN 1.0.3 specification, meaning it sends regular uplinks and you can send a downlink at any time, as the device constantly listens for LoRaWAN messages.

The messages are restricted by the LoRaWAN duty cycle requirements. The 16ADS can send both confirmed/unconfirmed uplink messages depending on its configuration.

When a downlink is sent to the 16ADS, it can be either confirmed or unconfirmed. For critical messages (e.g. initial parameters setup), we recommend using confirmed downlinks, so that the LNS can take care of repetition if required and successful delivery can be verified.

{% hint style="success" %}
**Downlink fports:** 1, 2, 4-224
{% endhint %}

One downlink packet from the LNS may contain multiple commands for the 16ADS to optimize the communication efficiency. These downlinks can combine both multiple write and/or read commands. Response to the GET commands will be sent in the next uplink.

When the LNS wants to read data from the device, the corresponding command code or command codes are sent to the device and the response will be sent together with the next keep-alive message. If the combined length of the command responses and the keep-alive packet is longer than the allowed by the LoRaWAN MAC layer application payload size, the keep-alive packet will be omitted and only the command responses will be sent by the 16ADS.

{% hint style="info" %}
**When the LNS writes device configuration data with a command, the data is stored in the device non-volatile memory, so there is no need to send this command again on the next network join.**
{% endhint %}

The aforementioned communication method is also described in table below

<table data-header-hidden><thead><tr><th width="206">Payload byte index</th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Payload byte index</strong></td><td><strong>Meaning</strong></td></tr><tr><td>0</td><td>Command 0 meaning</td></tr><tr><td>1</td><td>Command 0 data - optional</td></tr><tr><td>i</td><td>Command 1 meaning - optional</td></tr><tr><td>i+1</td><td>Command 1 data - optional</td></tr><tr><td>j</td><td>Command 2 meaning- optional</td></tr><tr><td>j+1</td><td>Command 2 data - optional</td></tr><tr><td>...</td><td>...</td></tr><tr><td>k</td><td>Command x meaning- optional</td></tr><tr><td>k+1</td><td>Command x data - optional</td></tr></tbody></table>
