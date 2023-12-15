# Network-related settings

{% hint style="info" %}
Available for firmware version 1.5 or later.
{% endhint %}

## Join-retry period

See below how to set/get the join-retry period of the device. If the devices is not connected to a gateway, this value basically instructs it how frequent it should try to re-join the network.

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="131">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>10 – The command code.</td></tr><tr><td>1</td><td>T, [s] = XX * 5. Value 0x00 isn’t applicable. Default value: 0x78 * 5 = 600 sec = 10 minutes.</td></tr></tbody></table>

**Example downlink, \[Hex]:** 10F0 – the server sets the join request period to 20 minutes.

Notes to this command:

* This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s;       &#x20;
* This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.
{% endtab %}

{% tab title="GET" %}
This command is used to get the period (T) of LoRaWAN join request sending from the end-node device. Server sends the command code and the response is sent from the device together with the next keep-alive command. The keep-alive in the response is omitted for clarity.

<table><thead><tr><th width="131.66666666666666">Byte index</th><th width="191">Received response</th><th>Received response</th></tr></thead><tbody><tr><td>0</td><td>19 – Command code</td><td>19 – Command code</td></tr><tr><td>1</td><td></td><td>XX – Network join retry period value. T, [s] = XX * 5.</td></tr></tbody></table>

**Example downlink, \[Hex]:** 19

**Example command response, \[Hex]:** 19C6 - T = 0xC6 \* _5 = 198 \*_ 5 = 990s = 16.5 minutes.
{% endtab %}
{% endtabs %}

## Communication watch-dog

{% tabs %}
{% tab title="SET" %}
This command is used to set independent radio watch-dog configurations for confirmed and unconfirmed uplink messages sent from the device. In other words, the radio watch-dog configuration for confirmed uplinks no matter when the device works with unconfirmed uplinks, and vice versa. When no downlink (regular or MAC command) is received for the defined Watch-Dog Period (WDP), the device resets itself.

<table><thead><tr><th width="129">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>1C – The command code.</td></tr><tr><td>1</td><td><p>XX – Watch-dog period (WDP) when <strong>confirmed uplinks</strong> are used by the device.</p><p>WDP_confirmed [min] = (XX * Keepalive period) + 7</p><p></p><p><strong>Default value for XX: 0x02.</strong></p><p>Note that value 0x00 disables the watch-dog functionality when confirmed uplinks are used.</p></td></tr><tr><td>2</td><td><p>XX – Watch-dog period (WDP) when <strong>unconfirmed uplinks</strong> are used by the device.</p><p>WDP_unconfirmed [min] = XX * 60 </p><p></p><p><strong>Default value for XX: 0x18.</strong></p><p>Note that value 0x00 disables the watch-dog functionality when unconfirmed uplinks are used.</p></td></tr></tbody></table>

**Example downlink, \[Hex]:** 1C0300 – Assuming that the send Keepalive period is 5 minutes,  WDP\_confirmed = (0x03 \* 5) + 7 = (3 \* 5) + 7 = 22 minutes.&#x20;

The watch-dog functionality for unconfirmed messages is totally disabled - 0x00.
{% endtab %}

{% tab title="GET" %}
This command is used to get the radio watch-dog configurations.

<table><thead><tr><th width="134.66666666666666">Byte index</th><th width="200">Sent request</th><th></th></tr></thead><tbody><tr><td>0</td><td>1D – Command code</td><td>1D – Command code</td></tr><tr><td>1</td><td></td><td>WDP_confirmed, as described in the SET command.</td></tr><tr><td>2</td><td></td><td>WDP_unconfirmed, as described in the SET command.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}
