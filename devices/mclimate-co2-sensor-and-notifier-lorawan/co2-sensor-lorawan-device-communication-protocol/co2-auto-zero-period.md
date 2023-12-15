# CO2 auto-zero period

### S**et CO2 auto-zero period**

Default auto-zero period, after the factory auto-zeroing, is 192 hours (8 days). During this period the lowest measured CO2 value is accepted as 400ppm and the auto-zero value is obtained automatically. If The period is 0, automatic auto-zero function is disabled, but the obtained or set with command auto-zero value is still used internally.

The command is described in Table 19.

| **Byte inde** | **Hex Velue** | **Meaning**                                 |
| ------------- | ------------- | ------------------------------------------- |
| 0             | 2A            | The command code.                           |
| 1             | 48            | Auto-zero period in hours. 0x48 = 72 hours. |

_Table 19_

**Example command:** 0x2A48 – The server sets CO2 auto-zero period to 72 hours.

### **Get CO2 auto-zero period**

| **Byte index** | **Sent request**   | **Received response**                             |
| -------------- | ------------------ | ------------------------------------------------- |
| 0              | 2B – Command code. | 2B – The command code.                            |
| 1              |                    | 48 –  Auto-zero period in hours. 0x48 = 72 hours. |

_Table 20_

**Example command sent from server:** 0x2B;

**Example command response:** 0x2B48 =>  CO2 auto-zero period is 72 hours.
