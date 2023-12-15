# CO2 auto-zero value

{% hint style="info" %}
In practice, you are not supposed to change the auto-zero value, as this would directly affect the internal self-calibration algorithm.&#x20;

\
You can get the CO2 auto-zero value in order to check whether normal calibration has worked correctly - e.g. expected values are in the range 0-1500ppm. If you see value of e.g. 20000, please use the SET function to set it back to 400ppm and leave the sensor at fresh air for at least 1.2xMeasurement intervals (if you are using default settings, expose the sensor to fresh air for at least 15 minutes).
{% endhint %}

### S**et CO2 auto-zero value**

This command is used by the device for CO2 measurements compensation in order to get 400ppm in fresh air. The command is described in Table 17.

| **Byte index** | **Hex Value** | **Meaning**                                     |
| -------------- | ------------- | ----------------------------------------------- |
| 0              | 20            | The command code.                               |
| 1              | 02            |                                                 |
| 2              | 21            | 0x0221 = 545. This value is represented in ppm. |

_Table 17_

**Example command:** 0x200221 – The server sets CO2 auto-zero value to 545 ppm.

### **Get CO2 auto-zero value**

| **Byte index** | **Bit index** | **Sent request**   | **Received response**                |
| -------------- | ------------- | ------------------ | ------------------------------------ |
| 0              | -             | 21 – Command code. | 21 – The command code.               |
| 1              | 15:8          |                    | 02                                   |
| 2              | 7:0           |                    | 21 – bits \[15:0] = 0x0221 = 545 ppm |

_Table 18_

**Example command sent from server:** 0x21;

**Example command response:** 0x210221 =>  CO2 auto-zero value is 545 ppm.



