# Network-related settings & Others

## Join-retry period

{% tabs %}
{% tab title="SET" %}
This command is used to set the period (T) of LoRaWAN join request sending from the device, in case it was unable to join the network from the first attempt.

<table data-header-hidden><thead><tr><th width="138.66666666666669"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>10 – The command code.</td></tr><tr><td>1</td><td>T, [s] = XX * 5. Value 0x00 isn’t applicable.<br><strong>Default</strong> <strong>value 0x78=10min</strong></td></tr></tbody></table>

**Example downlink:** 0x10F0 – the server sets the join request period to 20 minutes.
{% endtab %}

{% tab title="GET" %}
This command is used to get the period (T) of LoRaWAN join request sending from the device, in case it was unable to join the network from the first attempt. Server sends the command code and the response is sent together with the next keep-alive command.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>19 – Command code</td><td>19 – Command code</td></tr><tr><td>1</td><td> </td><td>XX – Network join retry period value. T, [s] = XX * 5.</td></tr></tbody></table>

**Example command sent from server:** 0x19;

**Example command response:** 0x19C6 => T = 0xC6\*5 = 198\*5 = 990s = 16.5 minutes.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s.
{% endhint %}

{% hint style="info" %}
This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.
{% endhint %}

## Communication Watch Dog&#x20;

There is a Watch Dog functionality that forces the device to reset, so it can rejoin the network in case a certain threshold has been reached where no downlinks have been received. There are 2 independent threshold values, one for confirmed mode and one for unconfirmed mode.

When working in confirmed mode if no downlink is received for the period defined by the  Watch Dog Period (_WDPconfirmed)_  parameter (see table below), the device resets itself.

When working in unconfirmed mode if no downlink is received for the period defined by the Watch Dog Period (_WDPunconfirmed)_ parameter (see table below), the device resets itself.

The command is described in the table below. The keep-alive in the response is omitted for clarity.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="147.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>1C – The command code.</td></tr><tr><td>1</td><td><p>XX – Watch Dog Period (WDP) when <strong>confirmed uplinks</strong> are used by the device.</p><p>XX defines how many uplinks should be received without ACK so that the device restarts. On top of that XX uplinks, another 7 minutes should pass before the device restarts.</p><p>D<strong>efault value for XX: 0x02.</strong><br><em>Note that value 0x00 disables the functionality when confirmed uplinks are used.</em></p></td></tr><tr><td>2</td><td><p>XX – Watch Dog Period (WDP) when <strong>unconfirmed uplinks</strong> are used by the device. Value is represented in hours.</p><p><strong>Default value for XX: 0x18. (24 hours)</strong></p><p><em>Note that value 0x00 disables the functionality when unconfirmed uplinks are used.</em></p></td></tr></tbody></table>

**Example command, \[Hex]:** 1C0300 – Assuming that the Keep-alive period is 5 minutes, the device will wait for 3x5+7 = 22 minutes before resetting if confirmed uplinks are used. If unconfirmed uplinks are used the functionality is disabled (0x00).
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1D – Command code</td><td>1D – Command code</td></tr><tr><td>1</td><td> </td><td><span class="math">WDP _{confirmed}</span> value.</td></tr><tr><td>2</td><td></td><td><span class="math">WDP _{unconfirmed}</span> value.</td></tr></tbody></table>

**Example command, \[Hex]:** 1C020C – Assuming that the Keep-alive period is 5 minutes, the device will wait for 2x5+7 = 17 minutes before resetting if confirmed uplinks are used. If unconfirmed uplinks are used it will wait for 0C\[HEX]=12\[DEC] hours and reset.
{% endtab %}
{% endtabs %}

## LoRaWAN Region

This command reports the LoRaWAN Region your device is setup to work in. Make sure it matches you network as LoRaWAN regions/bands are country dependent. This region is hardcoded in the FW and the user can not change it, only report on it. The keep-alive in the command response is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="147"></th><th width="194"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>A4 – Command code</td><td>A4 – Command code</td></tr><tr><td>1</td><td> </td><td><p>Radio region:<br>00 => EU868</p><p>01 => AS923</p><p>02 => AU915</p><p>03 => US915</p></td></tr></tbody></table>

**Example command, \[Hex]:** A400 – extracting the 1st byte value we get 00\[HEX], thus the device operates in the EU868 LoRaWAN band.
{% endtab %}
{% endtabs %}

## Deep-sleep activation

If you plan to store the device and you want it to conserve maximum power, you can put it to sleep with the following command:

<table data-header-hidden><thead><tr><th width="141"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>3B – The command code.</td></tr><tr><td>1</td><td>01 – Enter deep sleep mode. </td></tr></tbody></table>

**Example downlink: 0x3B01**

{% hint style="danger" %}
If you put the device to sleep, you then need to follow the commissioning procedure described in the user manual to wake-up the device.
{% endhint %}

## Full display refresh

In order to protect the display of the device from the so-called "ghosting", where an image becomes permanently imprinted on the e-ink display, we have to refresh it fully every max. 24 hours. If you decide, you can lower the full-refresh period, which can remove some dim artefacts from the display's partial refreshes.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="147.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>33 – The command code.</td></tr><tr><td>1</td><td><p>XX - Full display refresh in hours. </p><p>Acceptable values: 1 - 24 hours (0x01 - 0x18).<br><strong>Default</strong> <strong>value 0x0C=12hrs.</strong></p></td></tr></tbody></table>

Example downlink: 0x330E - set the full display refresh period to 10 hours.
{% endtab %}

{% tab title="GET" %}


<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>34 – Command code</td><td>34 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Display refresh period in hours</td></tr></tbody></table>

**Example downlink sent by the server:** 0x34;

**Example command response:** 0x340F - The full display refresh period is set to 15hours.
{% endtab %}
{% endtabs %}
