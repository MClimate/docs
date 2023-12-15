# CO2 Measurement period

### S**et** CO2 Measurement period&#x20;

The command is described in Table 21.

| **Byte index** | **Hex Value** | **Meaning**                                                                        |
| -------------- | ------------- | ---------------------------------------------------------------------------------- |
| 0              | 24            | The command code.                                                                  |
| 1              | 0A            | 0x0A = 10 minutes. Used until the measured CO2 levels are inside the good zone.    |
| 2              | 0A            | 0x0A = 10 minutes. Used until the measured CO2 levels are inside the medium zone.  |
| 3              | 0A            | 0x0A = 10 minutes. Used until the measured CO2 levels are inside the bad zone.     |

_Table 21_

{% hint style="info" %}
Payload values in the example are default for the device.
{% endhint %}

**Example command:** 0x240A0A0A – The server sets CO2 measurement period.

### **Get** CO2 Measurement period&#x20;

| **Byte index** | **Sent request**   | **Received response**                                                              |
| -------------- | ------------------ | ---------------------------------------------------------------------------------- |
| 0              | 25 – Command code. | 25 – The command code.                                                             |
| 1              |                    | 0x0A = 10 minutes. Used until the measured CO2 levels are inside the good zone.    |
| 2              |                    | 0x0A = 10 minutes. Used until the measured CO2 levels are inside the medium zone.  |
| 3              |                    | 0x0A = 10 minutes. Used until the measured CO2 levels are inside the bad zone.     |

_Table 22_

**Example command sent from server:** 0x25;

**Example command response:** 0x250A0A0A =>  CO2 Measurement period is 10 minutes inside the good, medium and bad zone.
