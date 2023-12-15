# Communication concepts

## Communication concepts related to the device's operation

{% hint style="info" %}
The device sends uplink on the following occasions:

1. Period uplink - Every keepalive period
2. Immediate uplink - on CO2 check via the button
3. Immediate uplink - when movement is detected
{% endhint %}

MClimate CO2 Display LoRaWAN  periodically sends messages (keep-alive commands) to the server. The server can then send command to the CO2 e-ink Display and the data will be received in the receiving windows, opened after each sent message, according to the LoRaWAN Class A devices protocol.&#x20;

The messages sent period is strict to the LoRaWAN duty cycle requirements. The CO2 e-ink Display can send both confirmed/unconfirmed uplink messages depending on its configuration.&#x20;

When a downlink is sent to the CO2 e-ink Display, it can be either confirmed or unconfirmed. For critical messages (e.g. initial parameters setup), we recommend using confirmed downlinks, so that the LNS can take care of repetition if required and successful delivery can be verified.&#x20;

One sent packet from the server may contain multiple commands for the CO2 e-ink Display to optimise the communication efficiency. These sent bytes can combine both multiple write or/and read commands. Response to the GET commands will be sent in the next uplinks.

When the server wants to read some data from the device, the corresponding command code or command codes are sent to the device and the response will be sent together with the next keep-alive message. If the length of the command responses and the keep-alive packet is longer than the allowed by LoRaWAN MAC layer application payload size, the keep-alive packet will be omitted and only the command responses are sent by the CO2 e-ink Display.

**When the server writes some device configuration with a command, the data is stored in the device non-volatile memory, so there isn’t need to send this command again on next network join.**

The aforementioned communication method is also described in Table 1.

<table data-header-hidden><thead><tr><th width="206">Payload byte index</th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Payload byte index</strong></td><td><strong>Meaning</strong></td></tr><tr><td>0</td><td>Command 0 meaning</td></tr><tr><td>1</td><td>Command 0 data - optional</td></tr><tr><td>i</td><td>Command 1 meaning - optional</td></tr><tr><td>i+1</td><td>Command 1 data - optional</td></tr><tr><td>j</td><td>Command 2 meaning- optional</td></tr><tr><td>j+1</td><td>Command 2 data - optional</td></tr><tr><td>...</td><td>...</td></tr><tr><td>k</td><td>Command x meaning- optional</td></tr><tr><td>k+1</td><td>Command x data - optional</td></tr></tbody></table>

Table 1

