# Get Firmware & Hardware version

The server can send the command code to the device (Table 6) and with the next received message the response is received.

<table data-header-hidden><thead><tr><th width="138.66666666666669"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>04 – Read software and hardware version</td></tr></tbody></table>

Table 6

<table data-header-hidden><thead><tr><th width="143.66666666666669"></th><th width="115"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>04 – The command byte shows that is packet with the device hardware and software version.</td></tr><tr><td>1</td><td>7:4</td><td>X – Device primary hardware version.</td></tr><tr><td>1</td><td>3:0</td><td>X – Device secondary hardware version.</td></tr><tr><td>2</td><td>7:4</td><td>X – Device primary software version.</td></tr><tr><td>2</td><td>3:0</td><td>X – Device secondary software version.</td></tr></tbody></table>

**Example response:** 0x042511 (The keep-alive data is omitted for clarity).

Decoding:

\-       0x04 – Read software and hardware version response

\-       0x25 - Device hardware version – version 2.5

\-       0x11 – Device software version – version 1.1
