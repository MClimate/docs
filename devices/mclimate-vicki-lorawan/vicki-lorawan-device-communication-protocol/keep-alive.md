---
description: How to decode the keep-alive packet and how to set new keep-alive period
---

# Keep-alive

## Keep-alive command explanation

Periodically sent message which contains the most important device data.

The data is described in Table 3.

<table data-header-hidden><thead><tr><th width="134">Byte index</th><th width="126.00000000000003">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>01 – Keep-alive command for firmware &#x3C;= 3.4<br>81 - Keep-alive command for firmware >= 3.5</td></tr><tr><td>1</td><td>-</td><td>XX – Target Temperature set by the rotary encoder. Currently 0x05 &#x3C;= XX &#x3C;= 0x1E</td></tr><tr><td>2</td><td>-</td><td><p>XX – Temperature measured by the device sensor.  </p><p></p><p><strong>For firmware &#x3C;= 3.4</strong><span class="math">t,[°C]= (XX*165)/256-40</span></p><p> <br><strong>For firmware >= 3.5</strong><br><span class="math">t,[°C]= (XX-28.33333)/5.66666</span></p></td></tr><tr><td>3</td><td>-</td><td><p>XX – Relative Humidity measured by the device sensor. </p><p><span class="math">RH, [\%] = (XX * 100) / 256</span> </p></td></tr><tr><td>4</td><td>-</td><td>XX – Motor position in steps, bits 7:0</td></tr><tr><td>5</td><td>-</td><td>XX – Motor range in steps, bits 7:0</td></tr><tr><td>6</td><td>7:4</td><td>X – Motor position in steps, bits 11:8</td></tr><tr><td>6</td><td>3:0</td><td>X – Motor range in steps, bits 11:8</td></tr><tr><td>7</td><td>7:4</td><td>X – Battery voltage. Voltage = 2 + X * 0.1, [V]</td></tr><tr><td>7</td><td>3</td><td>Set to 1 if open window functionality is enabled and such condition is met. Cleared otherwise.</td></tr><tr><td>7</td><td>2</td><td>Set to 1 if too high motor current consumption was measured. Cleared otherwise.</td></tr><tr><td>7</td><td>1</td><td>Set to 1 if too low motor current consumption was measured. Cleared otherwise.</td></tr><tr><td>7</td><td>0</td><td>Set to 1 if device temperature sensor is broken, cleared if it works properly.</td></tr><tr><td>8</td><td>7</td><td>Set to 1 if manual temperature set through the rotary encoder is disabled. Set to 0 otherwise.</td></tr><tr><td>8</td><td>6:0</td><td>!!! Reserved for future use in f.w. version less than 4.1</td></tr><tr><td>8</td><td>6</td><td>Set to 1 if device motor calibration fails due to impossibility to detect end of valve position. Cleared otherwise.</td></tr><tr><td>8</td><td>5</td><td>Set to 1 when the device is attached to the backplate. </td></tr><tr><td>8</td><td>4</td><td>Set to 1 when the device is online – joined the network and/or server packets are regularly received. Set to 0 if the device thinks it's offline.</td></tr><tr><td>8</td><td>3</td><td>Anti-free functionality status. <br>0 - it has not been activated<br>1 - it has been activated and the internal algorithm is working to reach the threshold temperature</td></tr><tr><td>8</td><td>2:0</td><td>Reserved for future use.</td></tr></tbody></table>

Table 3

**Example keep-alive:** 0x011D5A78FA2C01F080

**Decoding:**

* 0x01 – Command code (according to Table 2). Shows that keep-alive data follows
* 0x1D – Target temperature is 29
* 0x5A – Sensor temperature; 0x5A = 90; 90\*165/256-40 = 18,0078125 deg. Celsius
* 0x78 – Sensor humidity; 0x78 = 120; (120\*100)/256 = 46,875 % relative humidity
* 0xFA2C01 – Byte indexes 4, 5 and 6; Motor position = 0x0FA = 250; Motor range = 0x12C = 300;
* 0xF0 – Battery voltage and status; 0xF = Battery voltage = 2+ 15\*0,1 = 3,5VDC; 0x0 = All status flags are cleared.
* 0x80 – Rotary encoder is disabled (Child Lock is enabled).

**Example keep-alive 2:** 0x01185C5CDFDF118000

* 0x01 – Command code (according to Table 2). Shows that keep-alive data follows
* 0x18 = Target temperature is 24
* 0x5C = Sensor temperature; 0x5c = 92; 92 \*165/256-40 = 19,296875 deg. Celsius
* 0x5C= Sensor humidity; 0x5c = 92; 92\*100/256 = 35,9375 % relative humidity
* 0xDFDF11 = Byte indexes 4, 5 and 6; Motor position = 0x1DF = 479; Motor range = 0x1DF = 479
* 0x80 = Battery voltage and status; 0x8 = Battery voltage = 2 + 8\*0,1 = 2,8 VDC; 0x0 = All status flags are cleared.
* 0x00 = Rotary encoder is enabled (Child lock is disabled).

{% hint style="info" %}
Devices with firmware version 3.5 and above:\
&#x20;\- The byte at index 0 is changed to 0x81

&#x20;\- New formula is used for measured temperature calculation: (XX-28.33333)/5.66666
{% endhint %}

{% tabs %}
{% tab title="SET keep-alive period" %}
### Set Keep-alive period command explanation

&#x20;Sets the period for the Vicki keep-alive command messages. See table 4 for details.



<table data-header-hidden><thead><tr><th width="176">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>02 – The command will set Vicki keep-alive period.</td></tr><tr><td>1</td><td>XX – keep-alive period in minutes. Value 0x00 isn’t applicable.<br><strong>Default value: 0x0A.</strong></td></tr></tbody></table>

**Example command:** 0x020A

The example sets the keep-alive period to 10 minutes.

Note that the period value must respect the LoRaWAN messages duty cycle limitations. Otherwise the message will be sent when this is allowed. Also, the bigger period value, the less battery discharge. In most of cases, min. allowed period is 3 minutes and recommended values are 10 minutes or greater.
{% endtab %}

{% tab title="GET keep-alive period" %}
### Get keep-alive period command explanation

This command is used to get Vicki period of the keep-alive command messages. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The keep-alive in the response is omitted for clarity.



<table data-header-hidden><thead><tr><th width="124.66666666666666">Byte index</th><th width="225">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>12 – The command code.</td><td>12 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – device keep-alive period in minutes.</td></tr></tbody></table>

**Example command sent from server:** 0x12;

**Example command response:** 0x1209 – Vicki keep-alive is 9 minutes.
{% endtab %}
{% endtabs %}
