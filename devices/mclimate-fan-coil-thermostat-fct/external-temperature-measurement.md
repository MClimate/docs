# External temperature measurement

## 1. A**utomatic temperature control mode with external temperature reading**

{% tabs %}
{% tab title="SET" %}
#### This command activates/deactivates the automatic temp. control mode with external temp. reading.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>35 – The command code.</td></tr><tr><td>1</td><td><p>00: Deactivate the automatic temp. control mode;  <strong>Default value.</strong></p><p>01: Activate the automatic temp. control mode. </p></td></tr></tbody></table>

**Example downlink:** 0x3501 – Activate the automatic temp. control mode with external temp. reading.
{% endtab %}

{% tab title="GET" %}
#### This command gets whether automatic temp. control mode with external temp. reading is enabled or disabled?

<table data-header-hidden><thead><tr><th width="91.99999999999997"></th><th width="160"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>36 – Command code</td><td>36 – Command code</td></tr><tr><td>1</td><td> </td><td>00: The automatic temp. control mode is deactivated.<br>01: The automatic temp. control mode is activated.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x36;

**Example command response:** 0x3601 – The automatic temp. control mode with external temp. reading is activated.
{% endtab %}
{% endtabs %}

## 2. External temperature sensor value

The server sends this command to Fan Coil Thermostat device when it has a new measured temperature by the external sensor. This external temperature will be used by Fan Coil Thermostat for the internal temperature control algorithm. The commands are detailed in the tables below.

### 2.1 Set еxternal temperature sensor value with resolution 1.0°C

<table data-header-hidden><thead><tr><th width="135">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>3B – The command code.</td></tr><tr><td>1</td><td>XX – The ext. temperature in degrees Celsius. The value must be greater than 0°C!</td></tr></tbody></table>

**Example downlink:** 0x3B14 – the server notifies Fan Coil Thermostat that the measured temperature by the external sensor is 0x14\[HEX] => 20\[DEC] = 20°C.

### 2.2 Set/Get еxternal temperature sensor value with resolution 0.1°C

{% tabs %}
{% tab title="SET" %}
#### You can set the external temperature with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>3C – The command code.</td></tr><tr><td>1</td><td>XX - T[15:8].</td></tr><tr><td>2</td><td>XX - T[7:0]. </td></tr></tbody></table>

T\[15:0] = Texternal\[°C] \* 10; The value of Texternal\[°C] must be greater than 0°C!

**Example command**: 0x3C0102 - the server notifies the Fan Coil Thermostat that the measured temperature by the external sensor is 25,8°C => 25,8 \* 10 = 258 \[DEC] => 0x0102 \[HEX];
{% endtab %}

{% tab title="GET" %}
#### When the Fan Coil Thermostat is in "Automatic temperature control mode with external temperature reading", the command is sent together with the keepalive of the device.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>3E – Command code</td><td>3E – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - T[15:8].</td></tr><tr><td>2</td><td></td><td>XX - T[7:0].</td></tr></tbody></table>

Texternal\[°C] = T\[15:0] / 10;

**Example command:** 0x3E;

**Example response:** 0x3E0102;

0x0102 \[HEX] = 258 \[DEC] => Texternal = 258 / 10 = 25,8°C.
{% endtab %}
{% endtabs %}
