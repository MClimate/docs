# Device LED’s control

### **Device LED’s control command  explanation**

This command is used to control the device LED’s. It’s described in Table 16.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                 |
| -------------- | ------------- | ------------------------------------------------------- |
| 0              | -             | 05 – The command code.                                  |
| 1              | 7:5           | **Red** LED behavior_1_.                                |
|                | 4:0           | **Red** LED duration of the specified behavior_2_.      |
| 2              | 7:5           | **Green** LED behavior_1_.                              |
|                | 4:0           | **Green** LED duration of the specified behavior_2_.    |
| 3              | 7:5           | **Blue** LED behavior_1_.                               |
|                | 4:0           | **Blue** LED duration of the specified behavior _2_ .   |

_Table 16_

_1_ Bits 7:5 values:

* Turn the LED ON.
* Blink fast (10ms on, 200ms off).
* Blink slow (10ms on, 2000ms off).
* Turn the LED OFF.

_2_  The LED behavior duration can be zero. In this case, the specified LED behavior will be available until it’s changed from new radio command or the device button is pressed. If bits\[4:0] are non-zero, the specified LED duration is calculated by the expression: $$Duration, [s] = bits[4:0] * 10$$. The duration matters in case the LED behavior isn’t turned off.

**Example command, \[Hex]:** 05460046 – commands the device LED’s as follows:

* Red LED: Blink fast for 1 minute.
* Green LED: Turn off.
* Blue LED: Blink fast for 1 minute.
