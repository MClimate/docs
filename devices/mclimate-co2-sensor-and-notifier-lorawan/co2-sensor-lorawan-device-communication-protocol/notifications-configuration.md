# Notifications configuration

{% hint style="danger" %}
Please mind that notifications can require a lot of energy depending on your configuration. E.g. if you power on the LED for more than the default parameters, batteries will be depleted faster.\
\
The default values are what we recommend. We give you the flexibility to adjust them, but deviating the default values might shorten the battery life of your devices!
{% endhint %}

### S**et notify period**&#x20;

The command is described in Table 23.

| **Byte inde** | **Hex Velue** | **Meaning**                                                                                       |
| ------------- | ------------- | ------------------------------------------------------------------------------------------------- |
| 0             | 22            | The command code.                                                                                 |
| 1             | 00            | Notification period, in minutes, when measured CO2 is inside the good zone. 0 means notify once.  |
| 2             | 0A            | Notification period, in minutes, when measured CO2 is inside the medium zone. 0x0A = 10 minutes.  |
| 3             | 0A            | Notification period, in minutes, when measured CO2 is inside the bad zone. 0x0A = 10 minutes.     |

_Table 23_

{% hint style="info" %}
Payload values in the example are default for the device.
{% endhint %}

**Example command:** 0x22000A0A – The server sets CO2 measurement period.

### **Get notify period**&#x20;

| **Byte index** | **Sent request**   | **Received response**                                                                                      |
| -------------- | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| 0              | 23 – Command code. | 23 – The command code.                                                                                     |
| 1              |                    | 0x00 = 0. Notification period, in minutes, when measured CO2 is inside the good zone. 0 means notify once. |
| 2              |                    | 0x0A = 10. Notification period, in minutes, when measured CO2 is inside the medium zone.                   |
| 3              |                    | 0x0A = 10. Notification period, in minutes, when measured CO2 is inside the bad zone.                      |

_Table 24_

**Example command sent from server:** 0x23;

**Example command response:** 0x23000A0A =>  CO2 Notification period is once inside the good zone and 10 minutes inside the medium and bad zone.

### S**et buzzer notification configuration**&#x20;

The command is described in Table 25.

| **Byte inde** | **Hex Velue** | **Meaning**                                                                                                                                                           |
| ------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0             | 26            | The command code.                                                                                                                                                     |
| 1             | 00            | Duration of the buzzer beeping, in seconds, when must notify for good CO2 levels. A value of 0 means don’t notify. Default value for the device: 0ms.                 |
| 2             | 00            | Duration of the buzzer loud periods, when must notify for good CO2 levels. Duration, \[ms] = 0x00 \* 10 = 0. Default value for the device: 510ms.                     |
| 3             | 00            | Duration of the buzzer silent periods, when must notify for good CO2 levels. Duration, \[ms] = 0x00 \* 10 = 0. Default value for the device: 500ms.                   |
| 4             | 02            | Duration of the buzzer beeping, in seconds, when must notify for medium CO2 levels. 0x02 = 2s. Default value for the device: 500ms (Can’t be set with command).       |
| 5             | 65            | Duration of the buzzer loud periods, when must notify for medium CO2 levels. Duration, \[ms] = 0x65  \* _10 = 101 \*_ 10 = 1010. Default value for the device: 510ms. |
| 6             | 50            | Duration of the buzzer silent periods, when must notify for medium CO2 levels. Duration, \[ms] = 0x50 _\* 10 = 80 \*_ 10 = 800. Default value for the device: 500ms.  |
| 7             | 04            | Duration of the buzzer beeping, in seconds, when must notify for bad CO2 levels. 0x04 = 4s. Default value for the device: 2s.                                         |
| 8             | 65            | Duration of the buzzer loud periods, when must notify for bad CO2 levels. Duration, \[ms] = 0x65 \* _10 = 101 \*_ 10 = 1010. Default value for the device: 510ms.     |
| 9             | 50            | Duration of the buzzer silent periods, when must notify for bad CO2 levels. Duration, \[ms] = 0x50 \* _10 = 80 \*_ 10 = 800. Default value for the device: 500ms.     |

_Table 25_

**Example command:** 0x26 00 00 00 02 65 50 04 65 50 – The server sets CO2 buzzer notification.

### **Get buzzer notification configuration**&#x20;

| **Byte inde** | **Sent request** | **Received response**                                                                                                                                                        |
| ------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0             | 27               | 27 - The command code.                                                                                                                                                       |
| 1             |                  | 0x00 = Duration of the buzzer beeping, in seconds, when must notify for good CO2 levels. A value of 0 means don’t notify. Default value for the device: 0ms.                 |
| 2             |                  | 0x00 = Duration of the buzzer loud periods, when must notify for good CO2 levels. Duration, \[ms] = 0x00 \* 10 = 0. Default value for the device: 510ms.                     |
| 3             |                  | 0x00 = Duration of the buzzer silent periods, when must notify for good CO2 levels. Duration, \[ms] = 0x00 \* 10 = 0. Default value for the device: 500ms.                   |
| 4             |                  | 0x02 = Duration of the buzzer beeping, in seconds, when must notify for medium CO2 levels. 0x02 = 2s. Default value for the device: 500ms (Can’t be set with command).       |
| 5             |                  | 0x65 = Duration of the buzzer loud periods, when must notify for medium CO2 levels. Duration, \[ms] = 0x65  \* _10 = 101 \*_ 10 = 1010. Default value for the device: 510ms. |
| 6             |                  | 0x50 = Duration of the buzzer silent periods, when must notify for medium CO2 levels. Duration, \[ms] = 0x50 _\* 10 = 80 \*_ 10 = 800. Default value for the device: 500ms.  |
| 7             |                  | 0x04 = Duration of the buzzer beeping, in seconds, when must notify for bad CO2 levels. 0x04 = 4s. Default value for the device: 2s.                                         |
| 8             |                  | 0x65 = Duration of the buzzer loud periods, when must notify for bad CO2 levels. Duration, \[ms] = 0x65 \* _10 = 101 \*_ 10 = 1010. Default value for the device: 510ms.     |
| 9             |                  | 0x50 = Duration of the buzzer silent periods, when must notify for bad CO2 levels. Duration, \[ms] = 0x50 \* _10 = 80 \*_ 10 = 800. Default value for the device: 500ms.     |

_Table 26_

**Example command sent from server:** 0x27;

**Example command response:** 0x27 00 00 00 02 65 50 04 65 50  => CO2 buzzer notification settings.&#x20;

### S**et LED notification configuration**&#x20;

The command is described in Table 27.

| **Byte inde** | **Hex Velue** | **Meaning**                                                                                                         |
| ------------- | ------------- | ------------------------------------------------------------------------------------------------------------------- |
| 0             | 28            | The command code.                                                                                                   |
| 1             | 00            | Red LED command used to notify for good CO2 level.                                                                  |
| 2             | 02            | Green LED command used to notify for good CO2 level.                                                                |
| 3             | 00            | Blue LED command used to notify for good CO2 level.                                                                 |
| 4             | 00            |                                                                                                                     |
| 5             | 15            | Duration of the LED notification for good CO2 level = 0x0015 \* _10ms = 21 \*_ 10ms = 210ms.                        |
| 6             | 03            | Red LED command  used to notify for medium CO2 level.                                                               |
| 7             | 03            | Green LED command used to notify for medium CO2 level. Note that red and green color combination results in yellow. |
| 8             | 00            | Blue LED command used to notify for medium CO2 level.                                                               |
| 9             | 01            |                                                                                                                     |
| 10            | 92            | Duration of the LED notification for medium CO2 level = 0x0192 _10ms = 402_ 10ms = 4020ms.                          |
| 11            | 03            | Red LED command used to notify for bad CO2 level.                                                                   |
| 12            | 00            | Green LED command  used to notify for bad CO2 level.                                                                |
| 13            | 00            | Blue LED command used to notify for medium CO2 level.                                                               |
| 14            | 01            |                                                                                                                     |
| 15            | 92            | Duration of the LED notification for bad CO2 level = 0x0192 \* _10ms = 402 \*_ 10ms = 4020ms.                       |

_Table 27_

#### **Available LED commands values and meaning:**&#x20;

* 0x00: None;&#x20;
* 0x01: LED is constantly on for the given time duration;&#x20;
* 0x02: Blink fast for the given time duration;&#x20;
* 0x03: Blink slow for the given time duration. &#x20;

{% hint style="info" %}
Payload values in the example are default for the device.
{% endhint %}

**Example command:** 0x28 00 02 00 00 15 03 03 00 01 92 03 00 00 01 92 – The server sets CO2 LED notification.

### **Get LED notification configuration**&#x20;

| **Byte inde** | **Bit index** | **Sent request** | **Received response**                                                                                                      |
| ------------- | ------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------- |
| 0             |               | 29               | 29 - The command code.                                                                                                     |
| 1             |               |                  | 0x00 = Red LED command used to notify for good CO2 level.                                                                  |
| 2             |               |                  | 0x02 = Green LED command used to notify for good CO2 level.                                                                |
| 3             |               |                  | 0x00 = Blue LED command used to notify for good CO2 level.                                                                 |
| 4             | 15:8          |                  | 0x00                                                                                                                       |
| 5             | 7:0           |                  | 0x15 = Duration of the LED notification for good CO2 level = bits\[15:0] =  0x0015 \* _10ms = 21 \*_ 10ms = 210ms.         |
| 6             |               |                  | 0x03 = Red LED command used to notify for medium CO2 level.                                                                |
| 7             |               |                  | 0x03 = Green LED command used to notify for medium CO2 level. Note that red and green color combination results in yellow. |
| 8             |               |                  | 0x00 = Blue LED command used to notify for medium CO2 level.                                                               |
| 9             | 15:8          |                  | 0x01                                                                                                                       |
| 10            | 7:0           |                  | 0x92 = Duration of the LED notification for medium CO2 level =bits\[15:0] = 0x0192 _\* 10ms = 402 \*_ 10ms = 4020ms.       |
| 11            |               |                  | 0x03 = Red LED command used to notify for bad CO2 level.                                                                   |
| 12            |               |                  | 0x00 = Green LED command used to notify for bad CO2 level.                                                                 |
| 13            |               |                  | 0x00 = Blue LED command used to notify for bad CO2 level.                                                                  |
| 14            | 15:8          |                  | 0x01                                                                                                                       |
| 15            | 7:0           |                  | 0x92 = Duration of the LED notification for bad CO2 level =bits\[15:0] = 0x0192 _\* 10ms = 402 \*_ 10ms = 4020ms.          |

_Table 28_

**Example command sent from server:** 0x29;

**Example command response:** 0x28 00 02 00 00 15 03 03 00 01 92 03 00 00 01 92  => CO2 LED notification settings.&#x20;
