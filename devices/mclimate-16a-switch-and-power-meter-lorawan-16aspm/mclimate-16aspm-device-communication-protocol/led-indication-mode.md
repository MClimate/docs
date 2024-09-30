# LED indication mode

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="146"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>5B – The command code.</td></tr><tr><td>1</td><td><p>00 - Turn off the continuous LED indication of the radio joining status;</p><p>01 - Turn on the continuous LED indication of the radio joining status.  <strong>Default value.</strong></p></td></tr></tbody></table>

**Example downlink:** 0x5B00 – Turn off the continuous LED indication of the radio joining status.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="127.99999999999997"></th><th width="150"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5C – Command code</td><td>5C – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The continuous LED indication of the radio joining status is turned off;<br>01 - The continuous LED indication of the radio joining status is turned on.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x5C;

**Example command response:** 0x5C00 – The continuous LED indication of the radio joining status is turned off.
{% endtab %}
{% endtabs %}
