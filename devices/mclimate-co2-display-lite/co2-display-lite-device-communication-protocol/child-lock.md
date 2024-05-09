# Child lock

When the child lock function is on, all buttons on the front panel of the device are locked for manual control.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="140"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>07 – The command code.</td></tr><tr><td>1</td><td><p>00 – Turn off the child lock function;<br><strong>Default value of 0x00, disabled</strong></p><p>01 – Turn on the child lock function. </p></td></tr></tbody></table>

Example downlink: 0x0701 – Turn on the child lock function.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>14 – Command code</td><td>14 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - Child-lock is disabled;<br>01 - Child lock is enabled</td></tr></tbody></table>

Example downlink sent from server: 0x14;

Example uplink response: 0x1401 – The child-lock is enabled
{% endtab %}
{% endtabs %}
