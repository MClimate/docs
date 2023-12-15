# Force-close & Force-attach

### Valve close until over-voltage is detected command explanation, also called “Force close”.

Usage of this command must be avoided. Sending the command from the server causes the valve to be closed until over-voltage is detected from the device. In Table 12 is described the data the server sends.

<table data-header-hidden><thead><tr><th width="134">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0B – The command code.</td></tr></tbody></table>

Table 12

**Example command:** 0x0B

## Force-attach a Vicki

{% hint style="info" %}
Command for advanced users. Use with care.

Available in firmware >= 4.2
{% endhint %}

When you mount Vicki on a backplate, a small hidden button indicates that Vicki is mounted and it will start calibrating.

If the device that has been working fine previously and starts reporting it's not attached to a backplate and motorRange = 0, then you **might** want to force-attach it.

In it's essence, the force-attach command makes Vicki ignore the status of the aforementioned hidden button and starts the normal operation of the device.

If Vicki e.g. has been fiddled with by the customer and they did not attach it correctly afterwards, this command might be helpful.

If Vicki is not attached to a backplate and a valve at all, calibration will not be successful, as it wouldn't be able to determine the maximum closed position of the valve.

{% tabs %}
{% tab title="SET" %}


<table data-header-hidden><thead><tr><th width="133.5">Byte index</th><th>Byte value - meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>47 – the command code</td></tr><tr><td>1</td><td><p>Bits 7:1 – Reserved.</p><p>Bit 0 – 1 to force device attaching to valve disregarding the button which sense that. 0 to force device detaching from the valve.</p></td></tr></tbody></table>

**Example downlink:**&#x20;

0x4701 - Activate force-attach

0x4700 - Deactivate force-attach
{% endtab %}

{% tab title="GET" %}


<table><thead><tr><th width="129">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>48 – The command code.</td><td>48 – The command code.</td></tr><tr><td>1</td><td> </td><td><p>Bits 7:1 – Reserved.</p><p>Bit 0 – 1 the force-attach is activated, 0 otherwise.</p></td></tr></tbody></table>

**Example downlink:** 0x48

**Example uplink:** 0x4801 - the force-attach is activated
{% endtab %}
{% endtabs %}

