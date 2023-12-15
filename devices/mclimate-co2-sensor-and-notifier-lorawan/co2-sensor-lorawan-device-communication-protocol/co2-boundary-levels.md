# CO2 boundary levels

### S**et CO2** boundary levels

The command is described in Table 15.

| **Byte inde** | **Hex Velue** | **Meaning**                                                             |
| ------------- | ------------- | ----------------------------------------------------------------------- |
| 0             | 1E            | The command code.                                                       |
| 1             | 03            |                                                                         |
| 2             | 84            |  0x0384 = 900. This is the good-medium CO2 zone boundary value in ppm.  |
| 3             | 05            |                                                                         |
| 4             | DC            |  0x05DC = 1500. This is the medium-bad CO2 zone boundary value in ppm.  |

_Table 15_

{% hint style="info" %}
Payload values in the example are default for the device.
{% endhint %}

**Example command:** 0x1E038405DC – The server sets CO2 boundary levels to 900 ppm for good-medium zone and 1500 ppm for medium-bad zone.

### **Get CO2** boundary levels

| **Byte index** | **Bit index** | **Sent request**   | **Received response**                                       |
| -------------- | ------------- | ------------------ | ----------------------------------------------------------- |
| 0              | -             | 1F – Command code. | 1F – The command code.                                      |
| 1              | 15:8          |                    | 0x03                                                        |
| 2              | 7:0           |                    | 0x84 – bits \[15:0] = 0x0384 = 900 ppm for good-medium zone |
| 3              | 15:8          |                    | 0x05                                                        |
| 4              | 7:0           |                    | 0xDC – bits \[15:0] = 0x05DC = 1500 ppm for medium-bad zone |

_Table 16_

**Example command sent from server:** 0x1F;

**Example command response:** 0x1F038405DC =>  CO2 boundary levels to 900 ppm for good-medium zone and 1500 ppm for medium-bad zone.
