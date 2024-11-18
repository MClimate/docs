# Reset device

{% hint style="info" %}
This command is available for devices with firmware version ≥ 1.3.
{% endhint %}

{% hint style="danger" %}
Performing a Reset IS NOT equal to factory reset.
{% endhint %}

Reset the device, causing it to power cycle, and initiate a new join procedure.

{% hint style="danger" %}
Using this command will effectively disconnect the connected appliance for a brief period.
{% endhint %}

<table><thead><tr><th width="153"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>A5 – The command code.</td></tr></tbody></table>

**Example downlink**: 0xA5
