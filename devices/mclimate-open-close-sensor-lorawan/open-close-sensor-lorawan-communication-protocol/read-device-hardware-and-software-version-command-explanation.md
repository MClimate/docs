# Read device hardware and software version command explanation

The server sends the command code to the device (Table 6) and with the next received message the response is received. The device response is described in Table 7.

| Byte index | Bit index | Hex value – Meaning                     |
| ---------- | --------- | --------------------------------------- |
| 0          | -         | 04 – Read software and hardware version |

_Table 6_

**Example command, \[Hex]**: 04

| Byte index | Bit index | Hex value - Meaning                                                                       |
| ---------- | --------- | ----------------------------------------------------------------------------------------- |
| 0          | -         | 04 – The command byte shows that is packet with the device hardware and software version. |
| 1          | 7:4       | X – Device primary hardware version.                                                      |
|            | 3:0       | X – Device secondary hardware version.                                                    |
| 2          | 7:4       | X – Device primary software version.                                                      |
|            | 3:0       | X – Device secondary software version.                                                    |

_Table 7_

**Example response, \[Hex]**: 041311 (Here the received keep-alive command data is omitted for clarity).

**Decoding, \[Hex]**:

04 – Read software and hardware version response_._

13 - Device hardware version – version 1.3

11 – Device software version – version 1.1
