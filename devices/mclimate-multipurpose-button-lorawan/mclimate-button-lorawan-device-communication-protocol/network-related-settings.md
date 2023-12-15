# Network-related settings

### **Set network join retry period command explanation.**

This command is used to set the period (T) of LoRaWAN join request sending from the end node device, in case it was unable to join the network from the first attempt. The command is described in Table 9.

<table data-header-hidden><thead><tr><th width="150">Byte index</th><th width="611.4285714285713">Hex value – Meaning</th><th data-hidden>Bit index</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td><td>Bit index</td></tr><tr><td>0</td><td>10 – The command code.</td><td>-</td></tr><tr><td>1</td><td><p>T, [s] = XX * 5. </p><p>Value 00 isn’t applicable. </p><p>Default value: 02 * 5 = 10 minutes.</p></td><td>-</td></tr></tbody></table>

_Table 9_

**Example command, \[HEX]:** 10F0 – the server sets device LoRaWAN join request send period to 20 minutes.

&#x20;Notes to this command:

* This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s;
* This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.

### **Get network join retry period command explanation**

This command is used to get the period (T) of LoRaWAN join request sending from the end-node device. Server sends the command code and the response is sent from the device together with the next keep-alive command. The sent command request and the received command response are described in Table 10. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="150">Byte index</th><th width="200.35661617297035">Sent request</th><th width="325.82375137102474">Sent request</th><th data-hidden>Bit index</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Sent request</strong></td><td><strong>Bit index</strong></td></tr><tr><td>0</td><td>19 – Command code.</td><td>19 – The command code.</td><td>-</td></tr><tr><td>1</td><td></td><td>XX – Network join retry period value. T, [s] = XX * 5.</td><td>-</td></tr></tbody></table>

_Table 10_

**Example command sent from server, \[HEX]:** 19;

**Example command response, \[HEX]:** 19C6 => T = C6\*5 = 198\*5 = 990s = 16.5 minutes.

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
