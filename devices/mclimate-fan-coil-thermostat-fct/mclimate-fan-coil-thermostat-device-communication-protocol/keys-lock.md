# 🔓 Keys lock

You can decide that you want to lock some of the keys of the FCT and disable their use. Example - you may want to disable changing the fan speed.

{% tabs %}
{% tab title="SET" %}
#### You can disable one or a combination of keys with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>07 – The command code.</td></tr><tr><td>1</td><td><p>00: No keys locked.  <strong>Default value.</strong></p><p>01: Lock all keys. </p><p>02: Lock ON/OFF and mode change. </p><p>03: Lock ON/OFF. </p><p>04: Lock all keys except ON/OFF key. </p><p>05: Lock mode change.</p></td></tr></tbody></table>

**Example command**: 0x0705 – disables changing the mode through the button.
{% endtab %}

{% tab title="GET" %}
#### This command gets which keys have been disabled.

<table data-header-hidden><thead><tr><th width="131.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>14 – Command code</td><td>14 – Command code.</td></tr><tr><td>1</td><td> </td><td><p>00: No keys are locked.</p><p>01: All keys are locked.</p><p>02: ON/OFF and mode change are locked. </p><p>03: ON/OFF is locked. </p><p>04: All keys except ON/OFF key are locked. </p><p>05: Mode change is locked.</p></td></tr></tbody></table>

**Example command:** 0x14.

**Example response:** 0x1405 – The mode change key is locked.
{% endtab %}
{% endtabs %}

##
