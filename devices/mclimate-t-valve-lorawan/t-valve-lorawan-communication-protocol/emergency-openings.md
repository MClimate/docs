# Emergency openings

{% hint style="warning" %}
When T-Valve has been configured to work in either a [short cycle](valve-state-control.md#set-open-close-state-short-cycle) or [long cycle](valve-state-control.md#set-open-close-state-long-cycle) mode it will not accept a state change via the buttons the usual way.

In order to open/close the valve via a button you need to hold it for 5 seconds. Each state change exhausts 1 emergency opening, when down to 0 you will no longer be able to change the state.

You will need to set a new nonzero value with the command below every time it reaches 0 if you want to still be able to open/close the valve when it is in cyclical mode.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
This command sets the allowed emergency openings of the valve.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>04 – The command code</td></tr><tr><td>1</td><td>XX - Number of allowed emergency openings.<br><strong>Maximum: 15 times</strong></td></tr></tbody></table>

**Example command:** 0x040A

0A\[HEX] = 10\[DEC] -> Set the allowed emergency openings to 10 times
{% endtab %}

{% tab title="GET" %}
This command gets the remaining emergency openings of the valve.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0F – The command code</td></tr><tr><td>1</td><td>XX - Number of allowed emergency openings left.</td></tr></tbody></table>

**Example response:** 0x0F05

05\[HEX] = 5\[DEC] -> There are 5 emergency openings left
{% endtab %}
{% endtabs %}
