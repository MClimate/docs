# Heating status flag

The heating status flag is a small icon that appears on the display of the Wireless Thermostat when the target temperature is higher than the measured temperature.

You can select two options - it can show automatically or it can show only when you instruct it.

## Automatic heating status flag

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="140"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>37 – The command code.</td></tr><tr><td>1</td><td><p>00 – Turn off the automatic mode;</p><p>01 – Turn on the automatic mode. <strong>Default.</strong></p></td></tr></tbody></table>

Example downlink: 0x3701 – Turn on the automatic mode.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>38 – Command code</td><td>38 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The automatic heating status flag is turned OFF<br>01 - The automatic heating status flag is turned ON</td></tr></tbody></table>

**Example downlink sent from server:** 0x38;

**Example command response:** 0x3801 – The heating flag appears automatically when the target temperature is above the measured temperature.
{% endtab %}
{% endtabs %}

## Manual heating status flag

{% tabs %}
{% tab title="SET" %}


<table data-header-hidden><thead><tr><th width="140"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>31 – The command code.</td></tr><tr><td>1</td><td><p>00 – Hide the heating flag;</p><p>01 – Show the heating flag;</p></td></tr></tbody></table>

**Example downlink:** 0x3101 – Show the heating flag heating.
{% endtab %}

{% tab title="GET" %}


<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>32 – Command code</td><td>32 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The heating flag is hidden.<br>01 - The heating flag is shown.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x32;

**Example uplink response:** 0x3201 – The heating flag is shown.
{% endtab %}
{% endtabs %}
