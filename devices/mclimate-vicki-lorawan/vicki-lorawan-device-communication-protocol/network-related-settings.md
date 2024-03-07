# Network-related settings

## Get LoRaWAN Region

This command gets the&#x20;

<table data-header-hidden><thead><tr><th width="125">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>A4 – The command code.</td></tr><tr><td>1</td><td><p><span class="math">T, [s] = XX * 5.</span> Value 0x00 isn’t applicable. </p><p>Default value for f.w. &#x3C; 4.1: 3 minutes.<br>Default value for f.w. >= 4.1: 10 minutes</p></td></tr></tbody></table>

## Set network join retry period command explanation.

This command is used to set the period (T) of LoRaWAN join request sending from Vicki, in case it was unable to join the network from the first attempt. The command is described in Table 17.

<table data-header-hidden><thead><tr><th width="125">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>10 – The command code.</td></tr><tr><td>1</td><td>XX - LoRaWAN region<br>00: EU868<br>01:  AS923<br>02: AU915<br>03: US915<br>FF: Other</td></tr></tbody></table>

Table 17

**Example command:** 0x10F0 – the server sets Vicki LoRaWAN join request send period to 20 minutes.

&#x20;Notes to this command:

* This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s;
* This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.

## Get network join retry period command explanation

This command is used to get the period (T) of LoRaWAN join request sending from Vicki, in case it was unable to join the network from the first attempt. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The sent command request and the received command response are described in Table 26. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="134.33333333333331">Byte index</th><th width="148">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>19 – Command code.</td><td>19 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – Network join retry period value. <span class="math">T, [s] = XX*5</span></td></tr></tbody></table>

Table 26

**Example command sent from server:** 0x19;

**Example command response:** 0x19C6 => T = 0xC6\*5 = 198\*5 = 990s = 16.5 minutes.



## Set device radio communication watch-dog parameters command explanation

&#x20;This command is used to set independent Vicki radio watch-dog configurations for confirmed and unconfirmed uplink messages sent from the device. It other words, the radio watch-dog configuration for confirmed uplinks no matter when the device works with unconfirmed uplinks, and vice versa. When no downlink is received for the defined Watch-Dog Period (WDP), the device resets itself. The command is described in Table 28. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="124">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>1C – The command code.</td></tr><tr><td>1</td><td><p>XX – Watch-dog period (WDP) when confirmed uplinks are used by the device.</p><p>XX defines how many uplinks should be received without ack so that the device restarts. On top of that XX uplinks, another 7 minutes should pass before the device restarts.</p><p>Default value for XX: 0x02.</p><p>Note that value 0x00 disables the watch-dog functionality when confirmed uplinks are used.</p></td></tr><tr><td>2</td><td><p>XX – Watch-dog period (WDP) when unconfirmed uplinks are used by the device. Value is represented in hours.</p><p>Default value for XX: 0x18. (24 hours)</p><p>Note that value 0x00 disables the watch-dog functionality when unconfirmed uplinks are used.</p></td></tr></tbody></table>

Table 28

**Example command, \[Hex]:** 1C0300 – Assuming that the send Keep-alive period is 5 minutes, = 22 minutes, but the watch-dog functionality for unconfirmed messages is totally disabled.

## Get device radio communication watch-dog parameters command explanation

&#x20;This command is used to get the radio watch-dog configurations. The command is described in Table 29. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="137.33333333333331">Byte index</th><th width="196">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1D – Command code.</td><td>1D – The command code.</td></tr><tr><td>1</td><td></td><td><span class="math">WDP _{confirmed}</span> value, as described in Table 28.</td></tr><tr><td>2</td><td></td><td><span class="math">WDP _{unconfirmed}</span> value, as described in Table 28.</td></tr></tbody></table>

Table 29

## Change AppEUI and AppKey

{% hint style="danger" %}
Use with increased caution!&#x20;
{% endhint %}

{% hint style="info" %}
This feature is available in firmware >= 4.1
{% endhint %}

{% tabs %}
{% tab title="SET" %}
You can now change the AppEUI and AppKey of a device. Once the device has received this command, it restarts and re-join the network using the new keys.

<table data-header-hidden><thead><tr><th width="124">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>33 – The command code.</td></tr><tr><td>1</td><td>AppEUI byte 0 (most significant).</td></tr><tr><td>2</td><td>AppEUI byte 1.</td></tr><tr><td>...</td><td>...</td></tr><tr><td>8</td><td>AppEUI byte 7 (least significant)</td></tr><tr><td>9</td><td>AppKey byte 0 (most significant).</td></tr><tr><td>10</td><td>AppKey byte 1.</td></tr><tr><td>...</td><td>...</td></tr><tr><td>24</td><td>AppKey byte 15.</td></tr></tbody></table>

Example command to change the AppEUI to AABBCCDD11223344 and the AppKey to AABBCCDDEEFF00010203040506070809 is:

33AABBCCDD11223344AABBCCDDEEFF00010203040506070809
{% endtab %}
{% endtabs %}

## Remote reset the device

{% hint style="info" %}
This feature is available in firmware >= 4.0
{% endhint %}

{% hint style="danger" %}
When sending this command, **always use unconfirmed downlink**.
{% endhint %}

The command forces the device to fully reset (not reverting to factory settings), triggering recalibration as well as joining the network.

<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Sent request</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td></tr><tr><td>0</td><td>30 – Command code.</td></tr></tbody></table>
