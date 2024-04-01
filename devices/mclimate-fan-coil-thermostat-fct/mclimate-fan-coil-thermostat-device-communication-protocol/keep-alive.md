---
description: >-
  The keep-alive is a periodic message sent by the FCT with sensor data and
  more. In this page you will learn how to decode keepalive messages and how to
  set the keepalive interval.
---

# Keep-alive

## Keep-alive decoding

Periodically sent message which contains the most important device data.

The data is described in Table 1. In Table 2, an example packet is given.

<table><thead><tr><th width="96.66666666666669">Byte</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>01</td><td><strong>Command byte for this packet</strong>.</td></tr><tr><td>1</td><td>XX</td><td><strong>Internal temperature sensor</strong> data, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>XX</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0] - 400) / 10.</p></td></tr><tr><td>3</td><td>XX</td><td><strong>Relative Humidity data</strong>; RH [%] = (XX * 100) / 256.</td></tr><tr><td>4</td><td>XX</td><td><strong>Target temperature data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>5</td><td>XX</td><td><p>Target temperature data, bits 7:0 - T[7:0].</p><p>t [°C] = T[15:0] / 10.</p></td></tr><tr><td>6</td><td>XX</td><td><p><strong>Operational mode:</strong></p><p>00: Ventilation;</p><p>01: Heating;<br>02: Cooling.</p></td></tr><tr><td>7</td><td>XX</td><td><p><strong>Displayed fan speed:</strong><br>ECM fan                                      3-speed fan<br><strong>00: Auto                                             Auto</strong></p><p>01: Speed 1                                 NA</p><p><strong>02: Speed 2                                      Low</strong><br>03: Speed 3                                NA<br><strong>04: Speed 4                                      Medium</strong><br>05: Speed 5                                NA<br><strong>06: Speed 6                                      High</strong></p></td></tr><tr><td>8</td><td>XX</td><td><p><strong>Actual fan speed:</strong><br>ECM fan                                      3-speed fan</p><p>01: Speed 1                                 NA</p><p><strong>02: Speed 2</strong> <strong>Low</strong></p><p>03: Speed 3                                NA<br><strong>04: Speed 4                                      Medium</strong></p><p>05: Speed 5                                NA<br><strong>06: Speed 6                                      High</strong> </p><p>07 : Fan off <strong>Fan off</strong></p></td></tr><tr><td>9</td><td>XX</td><td><p><strong>Valve status:</strong> </p><p>00: Valve is closed; </p><p>01: Valve is open.</p></td></tr><tr><td>10</td><td>XX</td><td><p><strong>Device status:</strong> </p><p>00: The device is off;</p><p>01: The device is on.</p></td></tr></tbody></table>

_Table 1._

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>01</td><td><strong>Command byte for this packet.</strong></td></tr><tr><td>1</td><td>02</td><td><strong>Internal temperature sensor data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>88</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0] - 400) / 10<br>t [°C] = (0 x 0288 - 400) / 10 = (648 - 400) / 10 = 24.8°C.</p></td></tr><tr><td>3</td><td>80</td><td><strong>Relative Humidity data</strong>; RH [%] = (XX * 100) / 256<br>(0 x 80 * 100) / 256 = (128 * 100) / 256 = 50% RH</td></tr><tr><td>4</td><td>01</td><td><strong>Target temperature data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>5</td><td>09</td><td><p>Target temperature data, bits 7:0 - T[7:0].</p><p>t [°C] = T[15:0] / 10.<br>t [°C] = 0x0109 / 10 =  265 / 10 = 26.5°C.</p></td></tr><tr><td>6</td><td>01</td><td><strong>Operational mode:</strong><br>01: Heating.</td></tr><tr><td>7</td><td>02</td><td><strong>Displayed fan speed:</strong><br>02: Speed 2 (for ECM) / Low (for 3-speed)</td></tr><tr><td>8</td><td>02</td><td><p><strong>Actual fan speed:</strong> </p><p>02: Speed 2 (for ECM) / Low (for 3-speed)</p></td></tr><tr><td>9</td><td>01</td><td><strong>Valve status:</strong><br>01: Valve is open. </td></tr><tr><td>10</td><td>01</td><td><strong>Device status:</strong> <br>01: The device is on.</td></tr></tbody></table>

_Table 2._

### Keepalive period

{% tabs %}
{% tab title="SET" %}
#### This command is used to set the FCT's keep-alive message period The keep-alive data in the example is omitted for clarity.

<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – Command code to set keepalive period</td></tr><tr><td>1</td><td>XX – keep-alive period in minutes. <strong>Default value:</strong> 0x0A (10 minutes). Value 0x00 isn’t applicable. </td></tr></tbody></table>

**Example command:** 0x0203

The example sets the keep-alive period to 3 minutes.

**Note:** The period value must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger period value, the less battery discharge. In most cases, the minimum allowed period is 3 minutes and recommended values are 10 minutes or greater.
{% endtab %}

{% tab title="Get" %}
#### This command is used to get the FCT's keep-alive message period The keep-alive data in the example is omitted for clarity.

<table data-header-hidden><thead><tr><th width="137.66666666666666">Byte index</th><th width="225">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – device keep-alive period in minutes.</td></tr></tbody></table>

**Example command:** 0x12;

**Example response:** 0x1203 – The Fan Coil Thermostat's keep-alive is 3 minutes.
{% endtab %}
{% endtabs %}
