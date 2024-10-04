# Clear accumulated energy

{% hint style="warning" %}
This command is available for devices with firmware version ≥ 1.1
{% endhint %}

You can clear the accumulated energy in the long-term (EEPROM) memory.

{% hint style="info" %}
This is the only way to clear the accumulated energy, it will not be wiped if the device is reset or power cycled in any way. The only way to bring the measured energy to 0 is via the command.
{% endhint %}

<table><thead><tr><th width="134"></th><th width="111"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>26 – The command code.</td></tr><tr><td>1</td><td>-</td><td>01 - Clear the accumulated energy.</td></tr></tbody></table>

**Example downlink**: 0x2601 – Clear the accumulated energy.
