---
description: >-
  The keep-alive is a periodic message sent by the CO2 Display Lite with sensor
  data and more. In this page you will learn how to decode keepalive messages
  and how to set the keepalive interval.
---

# Keep-alive

## Keep-alive decoding

Periodically sent message which contains the most important device data.

The data is described in the table below, where an example is also given in a second table.

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="108">Bit Index</th><th width="77">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td>01</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>-</td><td>XX</td><td>Internal temperature sensor data, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>-</td><td>XX</td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0] - 400) / 10</p></td></tr><tr><td>3</td><td>-</td><td>XX</td><td>Relative Humidity data; RH [%] = (XX * 100) / 256</td></tr><tr><td>4</td><td>-</td><td>XX</td><td>Device battery voltage data, bits 15:8.</td></tr><tr><td>5</td><td>-</td><td>XX</td><td>Device battery voltage data, bits 7:0. Battery voltage, [mV].</td></tr><tr><td>6</td><td>-</td><td>XX</td><td>CO2 value in ppm, bits 7:0.</td></tr><tr><td>7</td><td>7:3</td><td>-</td><td>CO2 value in ppm, bits 12:8.</td></tr><tr><td></td><td>2:0</td><td>-</td><td><p>Power source status.</p><p>Тhe device is powered by:</p><p>000 - Built-in photovoltaic panel;</p><p>001 - Reserved;<br>002 - USB power supply.</p></td></tr><tr><td>8</td><td></td><td>XX</td><td>Device light intensity data, bits 15:8.</td></tr><tr><td>9</td><td></td><td>XX</td><td>Device light intensity data, bits 7:0. Light intensity [Lux].</td></tr></tbody></table>

### Keepalive example

<table><thead><tr><th width="87.66666666666669">Byte</th><th width="89">Bit index</th><th width="79">Value</th><th>Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td>01</td><td>Command byte for this packet.</td></tr><tr><td>1</td><td>-</td><td><strong>02</strong></td><td>Internal temperature sensor data, bits 15:8 – T[15:8].</td></tr><tr><td>2</td><td>-</td><td><strong>88</strong></td><td><p>Internal temperature sensor data, bits 7:0 - T[7:0].  </p><p>t [°C] = (T[15:0]-400)/10<br>t [°C] = (<strong>0x0288</strong>-400)/10 = (648-400)/10 = 24.8 deg C.</p></td></tr><tr><td>3</td><td>-</td><td>80</td><td>Relative Humidity data; RH [%] = (XX*100)/256<br>(0x80 * 100)/256 = (128*100)/256 = 50% RH</td></tr><tr><td>4</td><td>-</td><td><strong>0A</strong></td><td>Device battery voltage data, bits 15:8.</td></tr><tr><td>5</td><td>-</td><td><strong>45</strong></td><td><p>Device battery voltage data, bits 7:0. </p><p>Battery voltage, [mV].<br><strong>0x0A45</strong> = 2629mV</p></td></tr><tr><td>6</td><td>-</td><td>1B</td><td>CO2 value in ppm, bits 7:0.</td></tr><tr><td>7</td><td>7:3</td><td>00</td><td>CO2 value in ppm, bits 12:8.<br>CO2, [ppm]=CO2[12:0]<br><strong>0x1B00</strong>=0001101100000000<br>CO2, [ppm]=CO2[12:0]=0001101100000=864 ppm</td></tr><tr><td></td><td>2:0</td><td>00</td><td><p>Power source status.</p><p>Тhe device is powered by:</p><p><strong>0x00</strong>=0001101100000000</p><p>[3:0]=000</p><p>000 - Built-in photovoltaic panel;</p></td></tr><tr><td>8</td><td></td><td><strong>02</strong></td><td>Device light intensity data, bits 15:8.</td></tr><tr><td>9</td><td></td><td><strong>7A</strong></td><td>Device light intensity data, bits 7:0. Light intensity [LUX].<br><strong>0x027A</strong> = 634 LUX</td></tr></tbody></table>

### Keepalive period

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – Command code to set keepalive period</td></tr><tr><td>1</td><td>XX – keep-alive period in minutes. Value 0x00 isn’t applicable.<br><strong>Default value 0A=10min.</strong></td></tr></tbody></table>

**Example command:** 0x020A

The example sets the keep-alive period to 10 minutes.

Note that the period value must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger period value, the less battery discharge. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.
{% endtab %}

{% tab title="GET" %}
This command is used to get CO2 Display's period of the keep-alive command messages. Server sends the command code and the response is sent from the device together with the next keep-alive command.&#x20;

The keep-alive in the example is omitted for clarity.

<table data-header-hidden><thead><tr><th width="131.66666666666666">Byte index</th><th width="136">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – device keep-alive period in minutes.</td></tr></tbody></table>

**Example command sent from server:** 0x12;

**Example command response:** 0x1209 – Wireless Thermostat's keep-alive is 9 minutes.
{% endtab %}
{% endtabs %}
