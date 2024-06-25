# Network-related settings

## Join-retry period

{% tabs %}
{% tab title="SET" %}
This command is used to set the period (T) of LoRaWAN join request sending from the device, in case it was unable to join the network from the first attempt.

<table data-header-hidden><thead><tr><th width="131">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>10 – The command code.</td></tr><tr><td>1</td><td><p><span class="math">T, [s] = XX * 5.</span> Value 0x00 isn’t applicable. </p><p><strong>Default value:</strong> 0x78 * 5 = 600 sec = 10 minutes.</p></td></tr></tbody></table>

**Example command:** 0x10F0 – the server sets join request send period to 20 minutes.
{% endtab %}

{% tab title="GET" %}
This command is used to get the period (T) of LoRaWAN join request sending from the device, in case it was unable to join the network from the first attempt. Server sends the command code and the response is sent together with the next keep-alive command.

<table data-header-hidden><thead><tr><th width="134.33333333333331">Byte index</th><th width="148">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>19 – Command code.</td><td>19 – The command code.</td></tr><tr><td>1</td><td></td><td>XX – Network join retry period value. <span class="math">T, [s] = XX*5</span></td></tr></tbody></table>

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

### Set Send event button later when it is **allowed**

{% hint style="info" %}
The device may not always be able to send the command right now. The reason for this is the duty-cycle of LoRaWAN devices, which limits the amount of time a device transmits on the radio spectrum in order to be compliant with the EU regulations.

The duty-cycle depends on the Spreading factor. E.g. on SF12, the device can send one command every approx 2m30s and on SF7, it can send a command approx every 15 seconds.
{% endhint %}

This command is used to define the device behaviour when it is not allowed to send the signal right now due to duty-cycle restrictions. You can choose to not send the signal at all or to send it at earliest convenience. The command is described in Table 9.

<table data-header-hidden><thead><tr><th width="150">Byte index</th><th width="593.4285714285713">Hex value – Meaning</th><th data-hidden>Bit index</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td><td><strong>Bit index</strong></td></tr><tr><td>0</td><td>1E – The command code.</td><td>-</td></tr><tr><td>1</td><td><p>00 - Do not send the button event later when allowed. <strong>Default value: 00</strong></p><p>01 - Send the button event later when allowed. </p></td><td>-</td></tr></tbody></table>

_Table 9_

**Example command, \[HEX]:** 1E01 – the server sets device send the button event later when the LoRaWAN duty-cycle allows it.

### **Get** Send event button later when it is **allowed**

This command is used to retrieve the device behaviour on sending an uplink when the duty-cycle restrictions do not allow it to do it in real-time. The sent command request and the received command response are described in Table 10.&#x20;

<table data-header-hidden><thead><tr><th width="150">Byte index</th><th width="189.63302752293578">Sent request</th><th width="431.22543352601156">Sent request</th><th data-hidden>Bit index</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Sent request</strong></td><td><strong>Bit index</strong></td></tr><tr><td>0</td><td>1F – Command code.</td><td>1F – The command code.</td><td>-</td></tr><tr><td>1</td><td></td><td><p>00 - Do not send the button event later when allowed.</p><p>01 - Send the button event later when allowed. </p></td><td>-</td></tr></tbody></table>

_Table 10_

**Example command sent from server, \[HEX]:** 1F;

**Example command response, \[HEX]:** 1F01 - the device send the button event later when the LoRaWAN duty cycle allows it.
