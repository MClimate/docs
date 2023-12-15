# Uplink types

### **Set uplink messages type command explanation.**

This command is used to set the device sent uplink message type. The command is described in table 8.

<table><thead><tr><th width="150">Byte index</th><th width="621.961489088575">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>11 – The command code.</td></tr><tr><td>1</td><td><p>00 – The device sends unconfirmed uplink messages;</p><p>01 – The device sends confirmed uplink messages. </p><p>Default message type for the device is unconfirmed.</p></td></tr></tbody></table>

_Table 8_

**Example command**, **\[Hex]:** 1101 – The server sets device uplink message type to confirmed.

### **Get uplink messages type command explanation**

<table><thead><tr><th width="150">Byte index</th><th width="150">Sent request, [hex]</th><th width="448.2">Received response, [hex]</th></tr></thead><tbody><tr><td>0</td><td>1B – Command code.</td><td>1B – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – The device operates with unconfirmed uplinks;</p><p>01 – The device operates with confirmed uplinks.</p></td></tr></tbody></table>

_Table 9_

**Example command sent from server**, **\[Hex]:** 1B;

**Example command response**, **\[Hex]:** 1B00 => Device uplinks are unconfirmed.
