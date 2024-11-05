# 🥳 Release notes

### Firmware version 1.3

**Release date:** \
04 November 2024

* NEW - the device now can initiate a new join procedure either via the [Watch Dog](mclimate-16aspm-device-communication-protocol/network-related-settings.md#communication-watch-dog) timer expiring, or manually by **holding the button for 10s**. This is new in the sense that it does not power cycle the device, thus not causing the connected appliance to be turned OFF and ON.
* NEW - command to remotely power cycle the device - [A5](mclimate-16aspm-device-communication-protocol/reset-device.md).
* Bug fix - negative temperatures (Celsius) were not interpreted correctly.
* NEW - A flag for negative temperature has been added to the [keep-alive](mclimate-16aspm-device-communication-protocol/keep-alive.md) packet and to events for recovering [overcurrent](mclimate-16aspm-device-communication-protocol/protections.md#overcurrent-recovery-event) and [overpower](mclimate-16aspm-device-communication-protocol/protections.md#overpower-recovery-event) protection.
* Added functionality to calculate current sensor error and used in overcurrent and overpower protection.
* [Overvoltage protection](mclimate-16aspm-device-communication-protocol/protections.md#overvoltage-thresholds) parameters have been changed: trigger threshold from 275V to 245V; recovery threshold from 250V to 240V; threshold maximum range from 300V to 250V.
* Bug fix - LED indication incorrect behavior.

### Firmware version 1.2

**Release date:** \
24 September 2024

* Fixed a bug related to writing the accumulated energy in the EEPROM memory.

### Firmware version 1.1

**Release date:** \
23 September 2024

* Fixed a bug where the device restarts continuously if you press the button for 10s+. It now resets only one time unless you release and press it again.
* NEW - Mechanism to store the energy in long-term (EEPROM) memory.
* NEW - Added functionality to detect the type (DC or AC) of the voltage and respond accordingly. The device now accurately measures both AC and DC voltage, current and accumulated energy.
* NEW - when a protection event occurs the the event uplink is sent as a confirmed message and it will be periodically sent until an acknowledgement that it has been received by the server is received by the device.
* NEW - when the device recovers from a protection even it sends the corresponding uplink message now.
* Changed default overheating protection limits from 90 - 60°C to 95 - 70°C.
* If holding the button for 10s to reset the device
* Added functionality and radio commands "SET"/"GET" the state of the relay after overheating recovery (choose whether to retain previous state or start in a closed state every time).
* Added radio command to reset the energy count to zero.

### Firmware version 1.0

**Release date:** \
11 September 2024&#x20;

* Initial firmware release
