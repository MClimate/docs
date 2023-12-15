# Device buzzer control command

### **Device buzzer control command  explanation**

This command is used to control the device buzzer. It’s described in Table 15.

| **Byte index** | **Bit index** | **Hex value – Meaning**                                                                                                                                                                                                                                            |
| -------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0              | -             | 03 – The command code.                                                                                                                                                                                                                                             |
| 1              | 7:4           | <p>Buzzer volume:<br>0x0: Buzzer volume set to minimum available;<br>0x1: …<br>0x2: …</p><p>…</p><p>0xE: Buzzer volume set to maximum available;<br>0xF: Buzzer is off<strong>.</strong></p>                                                                       |
|                | 3:0           | <p>Buzzer frequency:<br>0x0: Buzzer frequency is 1kHz;<br>0x1: Buzzer frequency is 1.5kHz;<br>0x2: Buzzer frequency is 2kHz;<br>…</p><p>0xA: Buzzer frequency is 6kHz;<br>0xB: Reserved;<br>0xC: Reserved;<br>…<br>0xF: Reserved.</p>                              |
| 2              | -             | Time the buzzer to be active. Resolution – 1s. If zero, the buzzer will stay active until buzzer command with volume 0xF is received (buzzer turn-off) or the device button is pressed. During this time the buzzer continuously alternate loud and silent states. |
| 3              | -             | On time from the buzz loud-silent period. Resolution – 10ms.                                                                                                                                                                                                       |
| 4              | -             | Off time from the buzz loud-silent period. Resolution – 10ms.                                                                                                                                                                                                      |

_Table 15_

**Example command, \[Hex]:** 03E60A3264 – commands the buzzer as follows:

* Volume: max. available;
* Frequency: 4kHz;
* Time the buzzer to be active: 10s;
* On time from the buzz loud-silent period: 500ms.
* Off time from the buzz loud-silent period: 1000ms.
