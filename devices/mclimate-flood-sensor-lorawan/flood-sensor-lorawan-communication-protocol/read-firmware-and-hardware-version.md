# Read Firmware & Hardware version

{% hint style="info" %}
NOTE: Available for firmware version 1.5 or later.
{% endhint %}

The server can send the command code to the device (Table 10) and with the next received message the response is received. The device response is described in Table 11.

<table data-header-hidden><thead><tr><th width="138.66666666666669"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>07 – Read software and hardware version</td></tr></tbody></table>

_Table 10._

<table data-header-hidden><thead><tr><th width="143.66666666666669"></th><th width="115"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>07 – The command byte shows that is packet with the device hardware and firmware version.</td></tr><tr><td>1</td><td>7:4</td><td>X – Device primary hardware version.</td></tr><tr><td></td><td>3:0</td><td>X – Device secondary hardware version.</td></tr><tr><td>2</td><td>7:4</td><td>X – Device primary firmware version.</td></tr><tr><td></td><td>3:0</td><td>X – Device secondary firmware version.</td></tr></tbody></table>

_Table 11._

**Example response, \[Hex]:** 071115 (The keep-alive data is omitted for clarity).

Decoding:

\-       0x07 – Read firmware and hardware version response;

\-       0x11 - Device hardware version – version 1.1;

\-       0x15 – Device firmware version – version 1.5.
