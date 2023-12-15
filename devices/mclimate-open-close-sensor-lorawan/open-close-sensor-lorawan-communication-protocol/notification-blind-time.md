# Notification Blind Time

The Notification Blind Time is used to send the status (open / close) after a certain time. In this time interval, each detected status is counted by the status counter. When the time interval expires, the current status (open / close) and counter are sent to the keep-alive packet.

Notification Blind Time is useful when you are not interested in the events in real-time, but rather want to understand the "final" status of the sensor. E.g. if you install the sensor on a door, there might be a number of opens/closes in a single NBT. The sensor will not send an uplink for every event, but will send the final status of the sensor after NBT interval since the first event.

### **Set time interval command explanation.**

<table><thead><tr><th width="171">Byte index</th><th width="651.4285714285713">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>1E - The command code.</td></tr><tr><td>1</td><td><p>XX - Notification Blind Time in minutes. </p><p>Default value is 0 minutes.</p></td></tr></tbody></table>

_Table 14_

**Example command**, **\[Hex]:** 0x1E0A – the server sets NBT to 10 minutes.

### **Get time interval command explanation.**

<table><thead><tr><th width="175.4">Byte index</th><th width="150">Sent request, [hex]</th><th width="449.73543966501717">Received response, [hex]</th></tr></thead><tbody><tr><td>0</td><td>1F – Command code.</td><td>1F - The command code.</td></tr><tr><td>1</td><td></td><td>XX - NBT in minutes.</td></tr></tbody></table>

_Table 15_

**Example command sent from server**, **\[Hex]:** 1F;

**Example command response**, **\[Hex]:** 1F0A => NBT = 0A =  10 minutes.
