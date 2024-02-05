# Network-related settings & Others

## Join-retry period

See below how to set/get the join-retry period of the device. If the devices is not connected to a gateway, this value basically instructs it how frequent it should try to re-join the network.

{% tabs %}
{% tab title="SET" %}


<table data-header-hidden><thead><tr><th width="138.66666666666669"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>10 – The command code.</td></tr><tr><td>1</td><td>T, [s] = XX * 5. Value 0x00 isn’t applicable.<br><strong>Default</strong> <strong>value 0x78=10min</strong></td></tr></tbody></table>

**Example downlink:** 0x10F0 – the server sets the join request period to 20 minutes.

&#x20;Notes to this command:

* This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s;
* This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.
{% endtab %}

{% tab title="GET" %}
This command is used to get the period (T) of LoRaWAN join request sending from the end-node device. Server sends the command code and the response is sent from the device together with the next keep-alive command. The sent command request and the received command response are described in Table 10. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>19 – Command code</td><td>19 – Command code</td></tr><tr><td>1</td><td> </td><td>XX – Network join retry period value. T, [s] = XX * 5.</td></tr></tbody></table>

**Example downlink:** 0x19

**Example command response:** 0x19C6 => T = 0xC6\*5 _= 198\*5_ = 990s = 16.5 minutes.
{% endtab %}
{% endtabs %}

## Communication watch-dog

{% tabs %}
{% tab title="SET" %}
This command is used to set independent radio watch-dog configurations for confirmed and unconfirmed uplink messages sent from the device. In other words, the radio watch-dog configuration for confirmed uplinks no matter whether the device works with unconfirmed uplinks, and vice versa. When no downlink (regular or MAC command) is received for the defined Watch-Dog Period (WDP), the device resets itself.&#x20;

<table data-header-hidden><thead><tr><th width="147.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>1C – The command code.</td></tr><tr><td>1</td><td><p>XX – Watch-dog period (WDP) when <strong>confirmed uplinks</strong> are used by the device.</p><p>WDP_confirmed [min] = (XX * Keepalive period) + 7</p><p><strong>Default value 0x02=27min.</strong></p><p></p><p><strong>Note:</strong> The value 0x00 disables the watch-dog functionality when confirmed uplinks are used.</p></td></tr><tr><td>2</td><td><p>XX – Watch-dog period (WDP) when <strong>unconfirmed uplinks</strong> are used by the device.</p><p>WDP_unconfirmed [min] = XX * 60</p><p><strong>Default value 0x18=24hrs.</strong></p><p></p><p><strong>Note:</strong> The value 0x00 disables the watch-dog functionality when unconfirmed uplinks are used.</p></td></tr></tbody></table>

**Example downlink:** 0x1C0300 – Assuming that the send Keepalive period is 5 minutes,  WDP\_confirmed = (0x03 \* 5)+7 = (3\*5)+7 = 22 minutes.&#x20;

The watch-dog functionality for unconfirmed messages is totally disabled - 0x00.
{% endtab %}

{% tab title="GET" %}
This command is used to get the radio watch-dog configurations.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1D – Command code</td><td>1D – Command code</td></tr><tr><td>1</td><td> </td><td>WDP_confirmed, as described in the SET command</td></tr><tr><td>2</td><td></td><td>WDP_unconfirmed, as described in the SET command</td></tr></tbody></table>
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

c
