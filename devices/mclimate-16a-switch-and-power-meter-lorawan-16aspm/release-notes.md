# 🥳 Release notes

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
