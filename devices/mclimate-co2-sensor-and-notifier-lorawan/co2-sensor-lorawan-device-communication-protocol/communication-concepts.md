# Communication concepts

## Communication concepts related to device operation.

MClimate CO2 sensor & notifier device periodically sends messages (keep-alive commands) to the server. The server can then send command to the device and the data will be received in the receiving windows, opened after each sent message, according to the LoRaWAN Class A devices protocol. The messages sent period is strict to the LoRaWAN duty cycle requirements. This device  can send both confirmed/unconfirmed uplink messages depending on its configuration. We recommend configure it for confirmed uplinks, since they provide message retransmission in case of not acknowledge of the sent message.

&#x20;When a command is sent to this device, the LoRaWAN message type can be with confirmation (recommended). In this way the server is sure the command is received by the device, by checking the ACK bit from the MAC header of the next received packet. If the server doesn’t get a message confirmation, that command must be retransmitted by the server. One sent packet from the server may contain multiple commands for the end device to optimize communication time. The only restriction is the total number of bytes sent to be less or equal to the allowed application payload size. These sent bytes can combine both multiple write or/and read commands.

&#x20;If this device receives valid command from the server, next uplink sending will be done as soon as possible. In this way the server can check faster the ACK bit, in case of confirmed downlink was received by the device, or the requested data or the keep-alive command data.

&#x20;When the server wants to read some data from the device, the corresponding command code or command codes are sent to the device and the response will be sent together with the next keep-alive message. If the length of the command responses and the keep-alive packet is longer than the allowed by LoRaWAN MAC layer application payload size, the keep-alive packet will be omitted and only the command responses are sent by the device.&#x20;

The aforementioned communication method is also described in Table 1.

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

_Table 1_

When the server writes some device configuration with a command, the data is stored in the device non-volatile memory, so there isn’t need to send this command again on next network join.
