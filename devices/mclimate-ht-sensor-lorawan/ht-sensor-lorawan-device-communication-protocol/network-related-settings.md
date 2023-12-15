# Network-related settings

### **Set network join retry period command explanation.**

This command is used to set the period (T) of LoRaWAN join request sending from the end node device, in case it was unable to join the network from the first attempt. The command is described in Table 9.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                                   |
| -------------- | ------------- | ------------------------------------------------------------------------- |
| 0              | -             | 10 – The command code.                                                    |
| 1              | -             | T, \[s] = XX \* 5. Value 0x00 isn’t applicable. Default value: 3 minutes. |

_Table 9_

**Example command:** 0x10F0 – the server sets device LoRaWAN join request send period to 20 minutes.

&#x20;Notes to this command:

* This join retry period (T) must comply to LoRaWAN messages duty cycle. Otherwise the join request will be sent on the next attempt. In most of cases, min. acceptable value for T is 240s. Recommended are higher values, for less battery discharge, e.g. 480s;
* This join retry period (T) is for the first 15 sent messages. After, the used LoRaWAN stack automatically changes the possibility to send join request to \~20 minutes for 20 network join attempts. If the device is still not joined to the network after these 20 attempts, next join request can be sent after \~3 hours and 15 minutes.

### **Get network join retry period command explanation**

This command is used to get the period (T) of LoRaWAN join request sending from the end-node device. Server sends the command code and the response is sent from the device together with the next keep-alive command. The sent command request and the received command response are described in Table 10. The keep-alive in the response is omitted for clarity.

| **Byte index** | **Bit index** | **Sent request**   | **Sent request**                                         |
| -------------- | ------------- | ------------------ | -------------------------------------------------------- |
| 0              | -             | 19 – Command code. | 19 – The command code.                                   |
| 1              | -             |                    | XX – Network join retry period value. T, \[s] = XX \* 5. |

_Table 10_

**Example command sent from server:** 0x19;

**Example command response:** 0x19C6 => T = 0xC6\*5 = 198\*5 = 990s = 16.5 minutes.

### **Set device radio communication watch-dog parameters command  explanation**

This command is used to set independent radio watch-dog configurations for confirmed and unconfirmed uplink messages sent from the device. It other words, the radio watch-dog configuration for confirmed uplinks no matter when the device works with unconfirmed uplinks, and vice versa. When no downlink is received for the defined Watch-Dog Period (WDP), the device resets itself. The command is described in Table 13. The keep-alive in the response is omitted for clarity.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                                                                                                                                                                                                                                                       |
| -------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0              | -             | 1C – The command code.                                                                                                                                                                                                                                                                        |
| 1              | -             | <p>XX – Watch-dog period (WDP) when confirmed uplinks are used by the device.</p><p>WDP <em>confirmed</em>, [min] = XX *(Keep-alive period, [min]) + 7</p><p>Default value for XX: 0x02.</p><p>Note that value 0x00 disables the watch-dog functionality when confirmed uplinks are used.</p> |
| 2              | -             | <p>XX – Watch-dog period (WDP) when unconfirmed uplinks are used by the device. </p><p>WDP <em>unconfirmed</em>, [min] = XX *60</p><p>Default value for XX: 0x18.</p><p>Note that value 0x00 disables the watch-dog functionality when unconfirmed uplinks are used.</p>                      |

_Table 13_

**Example command, \[Hex]:** 1C0300 – Assuming that the send Keep-alive period is 5 minutes, **WDP** _confirmed_ = 22 minutes, but the watch-dog functionality for unconfirmed messages is totally disabled.

### **Get device radio communication watch-dog parameters command  explanation**

This command is used to get the radio watch-dog configurations. The command is described in Table 14. The keep-alive in the response is omitted for clarity.\


| **Byte index** | **Bit index** | **Sent request**   | **Received response**                                  |
| -------------- | ------------- | ------------------ | ------------------------------------------------------ |
| 0              | -             | 1D – Command code. | 1D – The command code.                                 |
| 1              | -             |                    | **WDP** _confirmed_ value, as described in Table 13.   |
| 2              | -             |                    | **WDP** un_confirmed_ value, as described in Table 13. |

_Table 14_
