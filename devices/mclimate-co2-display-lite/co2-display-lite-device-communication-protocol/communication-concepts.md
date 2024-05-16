# Communication concepts

## Communication concepts related to the device's operation

MClimate CO2 Display Lite periodically sends messages (keep-alive commands) to the server. The server can then send command to the CO2 Display Lite and the data will be received in the receiving windows, opened after each sent message, according to the LoRaWAN Class A devices protocol.&#x20;

The messages sent period is strict to the LoRaWAN duty cycle requirements. The CO2 Display Lite can send both confirmed/unconfirmed uplink messages depending on its configuration.&#x20;

When a downlink is sent to the CO2 Display Lite, it can be either confirmed or unconfirmed. For critical messages (e.g. initial parameters setup), we recommend using confirmed downlinks, so that the LNS can take care of repetition if required and successful delivery can be verified.&#x20;

One sent packet from the server may contain multiple commands for the CO2 Display Lite to optimize the communication efficiency. These sent bytes can combine both multiple write or/and read commands. Response to the GET commands will be sent in the next uplinks.

When the server wants to read some data from the device, the corresponding command code or command codes are sent to the device and the response will be sent together with the next keep-alive message. If the length of the command responses and the keep-alive packet is longer than the allowed by LoRaWAN MAC layer application payload size, the keep-alive packet will be omitted and only the command responses are sent by the CO2 Display Lite.

**When the server writes some device configuration with a command, the data is stored in the device non-volatile memory, so there isn’t need to send this command again on next network join.**

The aforementioned communication method is also described in table below

<table data-header-hidden><thead><tr><th width="206">Payload byte index</th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Payload byte index</strong></td><td><strong>Meaning</strong></td></tr><tr><td>0</td><td>Command 0 meaning</td></tr><tr><td>1</td><td>Command 0 data - optional</td></tr><tr><td>i</td><td>Command 1 meaning - optional</td></tr><tr><td>i+1</td><td>Command 1 data - optional</td></tr><tr><td>j</td><td>Command 2 meaning- optional</td></tr><tr><td>j+1</td><td>Command 2 data - optional</td></tr><tr><td>...</td><td>...</td></tr><tr><td>k</td><td>Command x meaning- optional</td></tr><tr><td>k+1</td><td>Command x data - optional</td></tr></tbody></table>
