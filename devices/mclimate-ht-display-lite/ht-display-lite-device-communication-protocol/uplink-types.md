# Uplink types

### **Set uplink messages type command explanation.**

This command is used to set the device sent uplink message type. The command is described in the table below.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                                                                                                                               |
| -------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0              | -             | 11 – The command code.                                                                                                                                                |
| 1              | -             | <p>00 – The device sends unconfirmed uplink messages;</p><p>01 – The device sends confirmed uplink messages. <strong>Default</strong> message type for the device</p> |

**Example command:** 0x1101 – The server sets device uplink message type to confirmed.

### **Get uplink messages type command explanation**

| **Byte index** | **Bit index** | **Sent request**   | **Received response**                                                                                            |
| -------------- | ------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------- |
| 0              | -             | 1B – Command code. | 1B – The command code.                                                                                           |
| 1              | -             |                    | <p>00 – The device operates with unconfirmed uplinks;</p><p>01 – The device operates with confirmed uplinks.</p> |

**Example command sent from server:** 0x1B;

**Example command response:** 0x1B00 => Device uplinks are unconfirmed.
