# Read device hardware and software version command explanation.

The server sends the command code to the device (Table 6) and with the next received message the response is received. The device response is described in Table 7.

<table data-header-hidden><thead><tr><th width="131">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>04 – Read software and hardware version</td></tr></tbody></table>

Table 6

**Example command**: 0x04

<table data-header-hidden><thead><tr><th width="139.33333333333331">Byte index</th><th width="103">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td><strong>-</strong></td><td>04 – The command byte shows that is packet with the device hardware and software version.</td></tr><tr><td>1</td><td>7:4</td><td>X – Device primary hardware version.</td></tr><tr><td>1</td><td>3:0</td><td>X – Device secondary hardware version.</td></tr><tr><td>2</td><td>7:4</td><td>X – Device primary software version.</td></tr><tr><td>2</td><td>3:0</td><td>X – Device secondary software version.</td></tr></tbody></table>

Table 7

**Example response**: 0x041211 (Here the received keep-alive command data is omitted for clarity).

**Decoding**:

* 0x04 – Read software and hardware version response
* 0x12 - Device hardware version – version 1.2
* 0x11 – Device software version – version 1.1

{% hint style="warning" %}
If you have used FUOTA or another way to update the firmware of the device, the hardware version will be changed as well. Please, do retain the initial hardware version in your system.
{% endhint %}
