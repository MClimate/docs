# Get Firmware & Hardware version

The server sends the command code to the device and with the next received message the response is received.&#x20;

| **Byte index** | **Bit index** | **Hex value – Meaning**                 |
| -------------- | ------------- | --------------------------------------- |
| 0              | -             | 04 – Read software and hardware version |

An example of a response is given in the table below.

**Example command**: 0x04

| **Byte index** | **Bit index** | **Hex value - Meaning**                                                                   |
| -------------- | ------------- | ----------------------------------------------------------------------------------------- |
| 0              | -             | 04 – The command byte shows that is packet with the device hardware and software version. |
| 1              | 7:4           | X – Device primary hardware version.                                                      |
| 1              | 3:0           | X – Device secondary hardware version.                                                    |
| 2              | 7:4           | X – Device primary software version.                                                      |
| 2              | 3:0           | X – Device secondary software version.                                                    |

**Example response, \[Hex]**: 041210 (Here the received keep-alive command data is omitted for clarity).

**Decoding**:&#x20;

* 0x04 – Read software and hardware version response
* 0x12 - Device hardware version – version 1.2
* 0x10 – Device software version – version 1.0
