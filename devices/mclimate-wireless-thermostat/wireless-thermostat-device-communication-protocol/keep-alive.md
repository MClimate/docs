---
description: >-
  The keep-alive is a periodic message sent by the Wireless Thermostat with
  sensor data and more. In this page you will learn how to decode keepalive
  messages and how to set the keepalive interval.
---

# Keep-alive

## Keep-alive decoding

Periodically sent message which contains the most important device data.

The data is described in Table 3. In Table 4 example packet is given.

{% tabs %}
{% tab title="f.w. ≥ 1.4" %}
<table><thead><tr><th width="94.66666666666669">Byte</th><th width="88">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>81</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>XX</td><td><strong>Internal temperature sensor data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>XX</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0]-400)/10</p></td></tr><tr><td>3</td><td>XX</td><td><strong>Relative Humidity data;</strong> RH [%] = (XX*100)/256</td></tr><tr><td>4</td><td>XX</td><td><strong>Supply voltage of the device data</strong>, bits 15:8.</td></tr><tr><td>5</td><td>XX</td><td><p>Supply voltage of the device data, bits 7:0. </p><p>Battery voltage, [mV].</p></td></tr><tr><td>6</td><td>XX</td><td><strong>Target temperature data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>7</td><td>XX</td><td><p>Target temperature data, bits 7:0 - T[7:0].</p><p>t [°C] = T[15:0] / 10.</p></td></tr><tr><td>8</td><td>XX</td><td><p><strong>Power source status.</strong></p><p>Тhe device is powered by:</p><p>00 - Built-in photovoltaic panel;</p><p>01 - АА batteries;<br>02 - USB power supply.</p></td></tr><tr><td>9</td><td>XX</td><td><strong>Device light intensity data</strong>, bits 15:8.</td></tr><tr><td>10</td><td>XX</td><td>Device light intensity data, bits 7:0. Light intensity [Lux].</td></tr><tr><td>11</td><td>XX</td><td><p><strong>PIR sensor status:</strong><br>00 - No motion detected;</p><p>01 - Motion detected.</p></td></tr></tbody></table>

_Table 3_.

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>81</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>02</td><td><strong>Internal temperature sensor data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>88</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0]-400)/10<br>t [°C] = (<strong>0x0288</strong>-400)/10 = (648-400)/10 = 24.8°C.</p></td></tr><tr><td>3</td><td>80</td><td><strong>Relative Humidity data</strong>; RH [%] = (XX*100)/256<br>(0x80 * 100)/256 = (128*100)/256 = 50% RH</td></tr><tr><td>4</td><td>0A</td><td><strong>Supply voltage of the device data</strong>, bits 15:8.</td></tr><tr><td>5</td><td>45</td><td><p>Supply voltage of the device data, bits 7:0. </p><p>Battery voltage, [mV].<br><strong>0x0A45</strong> = 2629mV.</p></td></tr><tr><td>6</td><td>01</td><td><strong>Target temperature data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>7</td><td>09</td><td><p>Target temperature data, bits 7:0 - T[7:0].</p><p>t [°C] = T[15:0] / 10.<br>t [°C] = 0x0109 / 10 =  265 / 10 = 26.5°C.</p></td></tr><tr><td>8</td><td>00</td><td><p><strong>Power source status</strong>.</p><p>Тhe device is powered by:</p><p>00 - Built-in photovoltaic panel;</p></td></tr><tr><td>9</td><td><strong>02</strong></td><td><strong>Device light intensity data</strong>, bits 15:8.</td></tr><tr><td>10</td><td>7A</td><td>Device light intensity data, bits 7:0. Light intensity [LUX].<br><strong>0x027A</strong> = 634 LUX.</td></tr><tr><td>11</td><td>00</td><td><strong>PIR sensor status:</strong><br>00 - No motion detected;</td></tr></tbody></table>

_Table 4_.
{% endtab %}

{% tab title="f.w. ≤ 1.3" %}
<table><thead><tr><th width="94.66666666666669">Byte</th><th width="103">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>01</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>XX</td><td><strong>Internal temperature sensor data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>XX</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0]-400)/10</p></td></tr><tr><td>3</td><td>XX</td><td><strong>Relative Humidity data;</strong> RH [%] = (XX*100)/256</td></tr><tr><td>4</td><td>XX</td><td><strong>Supply voltage of the device data</strong>, bits 15:8.</td></tr><tr><td>5</td><td>XX</td><td><p>Supply voltage of the device data, bits 7:0. </p><p>Battery voltage, [mV].</p></td></tr><tr><td>6</td><td>XX</td><td><strong>Target temperature in Celsius.</strong></td></tr><tr><td>7</td><td>XX</td><td><p><strong>Power source status.</strong></p><p>Тhe device is powered by:</p><p>00 - Built-in photovoltaic panel;</p><p>01 - АА batteries;<br>02 - USB power supply.</p></td></tr><tr><td>8</td><td>XX</td><td><strong>Device light intensity data</strong>, bits 15:8.</td></tr><tr><td>9</td><td>XX</td><td>Device light intensity data, bits 7:0. Light intensity [Lux].</td></tr><tr><td>10</td><td>XX</td><td><p><strong>PIR sensor status:</strong><br>00 - No motion detected;</p><p>01 - Motion detected.</p></td></tr></tbody></table>

Table 3.

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>01</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>02</td><td><strong>Internal temperature sensor data</strong>, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>88</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0]-400)/10<br>t [°C] = (<strong>0x0288</strong>-400)/10 = (648-400)/10 = 24.8°C.</p></td></tr><tr><td>3</td><td>80</td><td><strong>Relative Humidity data;</strong> RH [%] = (XX*100)/256<br>(0x80 * 100)/256 = (128*100)/256 = 50% RH</td></tr><tr><td>4</td><td>0A</td><td><strong>Supply voltage of the device data</strong>, bits 15:8.</td></tr><tr><td>5</td><td>45</td><td><p>Supply voltage of the device data, bits 7:0. </p><p>Battery voltage, [mV].<br><strong>0x0A45</strong> = 2629mV</p></td></tr><tr><td>6</td><td>17</td><td><strong>Target temperature in Celsius:</strong><br>0x17 = 23°C.</td></tr><tr><td>7</td><td>00</td><td><p><strong>Power source status.</strong></p><p>Тhe device is powered by:</p><p>00 - Built-in photovoltaic panel;</p></td></tr><tr><td>8</td><td>02</td><td><strong>Device light intensity data</strong>, bits 15:8.</td></tr><tr><td>9</td><td>7A</td><td>Device light intensity data, bits 7:0. Light intensity [LUX].<br><strong>0x027A</strong> = 634 LUX.</td></tr><tr><td>10</td><td>00</td><td><strong>PIR sensor status:</strong><br>00 - No motion detected;</td></tr></tbody></table>

Table 4.
{% endtab %}
{% endtabs %}

### Keepalive period

{% tabs %}
{% tab title="SET keep-alive period" %}
<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – Command code to set keepalive period</td></tr><tr><td>1</td><td>XX – keep-alive period in minutes. Value 0x00 isn’t applicable. Default value: 0x0A.</td></tr></tbody></table>

**Example command:** 0x0209

The example sets the keep-alive period to 9 minutes.

Note that the period value must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger period value, the less battery discharge. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.
{% endtab %}

{% tab title="GET keep-alive period" %}
This command is used to get Wireless Thermostat's period of the keep-alive command messages. Server sends the command code and the response is sent from the device together with the next keep-alive command.&#x20;

The keep-alive in the example is omitted for clarity.

<table data-header-hidden><thead><tr><th width="137.66666666666666">Byte index</th><th width="225">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – device keep-alive period in minutes.</td></tr></tbody></table>

**Example command sent from server:** 0x12;

**Example command response:** 0x1209 – Wireless Thermostat's keep-alive is 9 minutes.
{% endtab %}
{% endtabs %}

**Note:** Acceptable values: 1...255 minutes (1min. resolution).
