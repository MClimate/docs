# General, Display & Power recovery

## Operation after return of power supply

You can change the operation after return of power supply with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the operation after return of power supply with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>68 – The command code.</td></tr><tr><td>1</td><td>00: Last status. <strong>Default value.</strong><br>01: On - after return of power supply.<br>02: Off - after return of power supply.</td></tr></tbody></table>

**Example command**: 0x6802 – Sets the device to be off after return of power supply.
{% endtab %}

{% tab title="GET" %}
#### Get the operation after return to power status.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>69 – Command code</td><td>69 – Command code.</td></tr><tr><td>1</td><td> </td><td>00: Last status.<br>01: On - after return of power supply.<br>02: Off - after return of power supply.</td></tr></tbody></table>

**Example command:** 0x69;

**Example response:** 0x6902 – The device is set to be off after return of power supply.
{% endtab %}
{% endtabs %}

## Get Firmware & Hardware version

The LNS can send the command code to the device and with the next received message the response (Table 6) is received.

<table data-header-hidden><thead><tr><th width="138.66666666666669"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>04 – Read software and hardware version.</td></tr></tbody></table>

_Table 6._

<table data-header-hidden><thead><tr><th width="143.66666666666669"></th><th width="115"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>04 – The command byte shows that is packet with the device hardware and software version.</td></tr><tr><td>1</td><td>7:4</td><td>X – Device primary hardware version.</td></tr><tr><td>1</td><td>3:0</td><td>X – Device secondary hardware version.</td></tr><tr><td>2</td><td>7:4</td><td>X – Device primary software version.</td></tr><tr><td>2</td><td>3:0</td><td>X – Device secondary software version.</td></tr></tbody></table>

**Example command:** 0x04

**Example response:** 0x042511 (The keep-alive data is omitted for clarity).

Decoding:

\-       0x04 – Read software and hardware version response

\-       0x25 - Device hardware version – version 2.5

\-       0x11 – Device software version – version 1.1

**Note:** The HEX value is not converted to DEC to obtain the version, it is interpreted symbol by symbol.
