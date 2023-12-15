# Network-related settings

### **Set network join retry period command explanation.** <a href="#set-network-join-retry-period-command-explanation" id="set-network-join-retry-period-command-explanation"></a>

This command is used to set the period (T) of LoRaWAN join request sending from the end node device, in case it was unable to join the network from the first attempt. The command is described in table 10.

<table><thead><tr><th width="150">Byte index</th><th width="632.4285714285713">Hex value – Meaning</th></tr></thead><tbody><tr><td><strong>0</strong></td><td>10 – The command code.</td></tr><tr><td>1</td><td><p>T, [s] = XX * 5. </p><p>Value 00 isn’t applicable. </p><p>Default value: 3 minutes.</p></td></tr></tbody></table>

_Table 10_

**Example command**, **\[Hex]:** 10F0 – the server sets device LoRaWAN join request send period to 20 minutes.

Notes to this command:

* This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s;
* This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.

### **Get network join retry period command explanation** <a href="#get-network-join-retry-period-command-explanation" id="get-network-join-retry-period-command-explanation"></a>

This command is used to get the period (T) of LoRaWAN join request sending from the end-node device. Server sends the command code and the response is sent from the device together with the next keep-alive command. The sent command request and the received command response are described in Table 11. The keep-alive in the response is omitted for clarity.

<table><thead><tr><th width="150">Byte index</th><th width="198">Sent request, [hex]</th><th width="374.992700729927">Received response, [hex]</th></tr></thead><tbody><tr><td>0</td><td>19 – Command code.</td><td>19 – The command code.</td></tr><tr><td>1</td><td></td><td><p>XX – Network join retry period value. </p><p>T, [s] = XX * 5.</p></td></tr></tbody></table>

_Table 11_

**Example command sent from server**, **\[Hex]:** 19;

**Example command response**, **\[Hex]:** 19C6 => T = C6\*5 = 198\*5 = 990s = 16.5 minutes.

### **Set device radio communication watch-dog parameters command explanation** <a href="#set-device-radio-communication-watch-dog-parameters-command-explanation" id="set-device-radio-communication-watch-dog-parameters-command-explanation"></a>

This command is used to set independent radio watch-dog configurations for confirmed and unconfirmed uplink messages sent from the device. It other words, the radio watch-dog configuration for confirmed uplinks no matter when the device works with unconfirmed uplinks, and vice versa. When no downlink is received for the defined Watch-Dog Period (WDP), the device resets itself. The command is described in table 1_2_. The keep-alive in the response is omitted for clarity.

<table><thead><tr><th width="150">Byte index</th><th width="637.4285714285713">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>1C – The command code.</td></tr><tr><td>1</td><td><p>XX – Watch-dog period (WDP) when confirmed uplinks are used by </p><p>the device.</p><p>WDP <em>unconfirmed</em>, [min] = XX *(Keep-alive period, [min]) + 7</p><p>Default value for XX: 02.</p><p>Note that value 00 disables the watch-dog functionality when</p><p>confirmed uplinks are used.</p></td></tr><tr><td>2</td><td><p>XX – Watch-dog period (WDP) when unconfirmed uplinks are used by the device. Value is represented in hours.</p><p>Default value for XX: 0x18. (24 hours)</p><p>Note that value 0x00 disables the watch-dog functionality when </p><p>unconfirmed uplinks are used.</p></td></tr></tbody></table>

_Table 12_

**Example command, \[Hex]:** 1C0300 – Assuming that the send Keep-alive period is 5 minutes, **WDP** _confirmed_ = 22 minutes, but the watch-dog functionality for unconfirmed messages is totally disabled.

### **Get device radio communication watch-dog parameters command explanation** <a href="#get-device-radio-communication-watch-dog-parameters-command-explanation" id="get-device-radio-communication-watch-dog-parameters-command-explanation"></a>

This command is used to get the radio watch-dog configurations. The command is described in table 13. The keep-alive in the response is omitted for clarity.

<table><thead><tr><th width="161.04501358168415">Byte index</th><th width="150">Sent request, [hex]</th><th width="490.7335088381374">Received response, [hex]</th></tr></thead><tbody><tr><td>0</td><td>1D – Command code.</td><td>1D – The command code.</td></tr><tr><td>1</td><td></td><td><strong>WDP</strong> <em>confirmed</em> value, as described in Table 8.</td></tr><tr><td>2</td><td></td><td><strong>WDP</strong> un<em>confirmed</em> value, as described in Table 8.</td></tr></tbody></table>

_Table 13_
