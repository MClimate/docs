# Child lock

{% tabs %}
{% tab title="SET" %}
## Set child lock parameters command explanation.

&#x20;When child lock is enabled, manual target temperature change with the device rotary encoder is forbidden. If the user rotates the rotary encoder, in case Child lock is enabled, on the device LED display “Ch” is shown.

&#x20;In Table 10 is described the data which the server sends to control this functionality.

<table data-header-hidden><thead><tr><th width="139">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>07 – The command code.</td></tr><tr><td>1</td><td>XX – 01 to enable and 00 to disable child lock functionality.</td></tr></tbody></table>

Table 10

**Example command:** 0x0701 – Enable child lock.
{% endtab %}

{% tab title="GET" %}
## Get child lock parameters command explanation

&#x20;This command is used to get Vicki child lock functional state. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The sent command request and the received command response are described in Table 21. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="96.33333333333331">Byte index</th><th width="198">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>14 – Command code.</td><td>14 – The command code.</td></tr><tr><td>1</td><td></td><td><p>01 – child lock functionality is enabled;</p><p>00 – child lock functionality is disabled;</p></td></tr></tbody></table>

Table 21

**Example command sent from server:** 0x14;

**Example command response:** 0x1400 – Child lock functionality is disabled.
{% endtab %}
{% endtabs %}

## Child lock behavior when device goes offline

You can choose what happens with the Child lock setting if a device goes offline for some reason (e.g. gateway is offline). Once the device comes back online, it'll revert to the previously set settings.

{% hint style="danger" %}
Available in f.w. 4.1 and above
{% endhint %}

{% hint style="info" %}
E.g. If child lock is activated on a device and it goes offline, you can decide whether the child lock is disabled.

Once the device comes back online, it'll revert to the settings that were active prior to going offline.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="135">Byte index</th><th>Hex Value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex Value - Meaning</strong></td></tr><tr><td>0</td><td>35 - Command code</td></tr><tr><td>1</td><td><p>00 – Child lock is automatically disabled when the device goes offline.</p><p>01 – Child lock remains unchanged when the device goes offline.</p></td></tr></tbody></table>
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="93.33333333333331">Byte index</th><th width="149">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>34 – Command code.</td><td>34 – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – When child lock is enabled and the device goes offline, child lock will be automatically disabled. <strong>Default for the device.</strong></p><p>01 – Child lock remains unchanged when the device goes offline.</p></td></tr></tbody></table>
{% endtab %}
{% endtabs %}

##
