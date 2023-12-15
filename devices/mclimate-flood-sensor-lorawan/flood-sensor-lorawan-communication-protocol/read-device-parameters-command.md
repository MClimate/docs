# Read device parameters command

{% hint style="info" %}
This command is useful only for f.w. < 1.5

In f.w. >= 1.5, you can use the "[Read Firmware & Hardware version](read-firmware-and-hardware-version.md)" command.
{% endhint %}

<table data-header-hidden><thead><tr><th width="138.66666666666669"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>01 – Read device parameters</td></tr></tbody></table>

**Example command**, **\[Hex]:** 01

**Example response from the device**, **\[Hex]**: 42C21A15

The data is described in Table 8. In Table 9 example packet is given.

<table><thead><tr><th width="150">Byte index</th><th width="150">Bit index</th><th width="449.2">Meaning</th></tr></thead><tbody><tr><td>0</td><td>7:5</td><td><p>000: Keep-alive; </p><p>001: Reserved;</p><p>010: Flood detected by device sensor; </p><p>100: Box tamper switch detected.</p></td></tr><tr><td></td><td>4</td><td>Reserved.</td></tr><tr><td></td><td>3</td><td><p>0: No box tamper detected; </p><p>1: Box tamper detected.</p></td></tr><tr><td></td><td>2</td><td>Reserved.</td></tr><tr><td></td><td>1</td><td><p>0: No flood detected; </p><p>1: Flood detected.</p></td></tr><tr><td></td><td>0</td><td>Reserved.</td></tr><tr><td>1</td><td>7:0</td><td>Battery voltage, [mV] = (bits7:0)*16</td></tr><tr><td>2</td><td>7</td><td><p>0: The temperature is positive; </p><p>1: The temperature is negative. </p><p><strong>NOTE:</strong> This bit is used in firmware version 1.5 or later.</p></td></tr><tr><td></td><td>6:0</td><td>Temperature sensor value in Celsius degrees.</td></tr><tr><td>3</td><td>7:4</td><td>X – Device primary firmware version.</td></tr><tr><td></td><td>3:0</td><td>X – Device secondary firmware version.</td></tr></tbody></table>

_Table 8._



<table><thead><tr><th width="114">Payload index</th><th width="81">Value, [hex]</th><th width="98">Bit index</th><th width="436.71428571428567"></th></tr></thead><tbody><tr><td>0</td><td>42</td><td>7:5</td><td><p>010: Flood detected</p><p> by device sensor.</p></td></tr><tr><td></td><td></td><td>4</td><td>Reserved.</td></tr><tr><td></td><td></td><td>3</td><td>0: No box tamper detected.</td></tr><tr><td></td><td></td><td>2</td><td>Reserved.</td></tr><tr><td></td><td></td><td>1</td><td>1: Flood detected.</td></tr><tr><td></td><td></td><td>0</td><td>Reserved.</td></tr><tr><td>1</td><td>C2</td><td>7:0</td><td><p>Battery voltage</p><p>[mV] = (194)*16 = 3104.</p></td></tr><tr><td>2</td><td>1A</td><td>7</td><td><p>0: The temperature is positive. </p><p><strong>NOTE:</strong> This bit is used in firmware version 1.5 or later.</p></td></tr><tr><td></td><td></td><td>6:0</td><td>The temperature is 26 Celsius degrees.</td></tr><tr><td>3</td><td>15</td><td>7:3</td><td>1 – Device primary firmware version.</td></tr><tr><td></td><td></td><td>4:0</td><td>5 – Device secondary firmware version.<br>Device firmware version – version 1.5</td></tr></tbody></table>

_Table 9._
