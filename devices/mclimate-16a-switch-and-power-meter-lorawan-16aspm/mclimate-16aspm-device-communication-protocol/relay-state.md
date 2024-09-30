# Relay state

## Relay state change

This command sets/gets the state of the relay, effectively powering/depowering the appliance it is controlling.

{% hint style="info" %}
By default, the last state of the relay is saved in the device's memory.

For more details, see the command described below.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="146"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>C1 – The command code.</td></tr><tr><td>1</td><td><p>00 – OFF;</p><p>01 – ON. </p></td></tr></tbody></table>

**Example downlink:** 0xC101 – Turn on the relay.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>B1 – Command code</td><td>B1 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The relay is off;<br>01 - The relay is on;</td></tr></tbody></table>

**Example downlink sent by the server:** 0xB1;

**Example command response:** 0xB101 – The relay is ON.
{% endtab %}
{% endtabs %}

## Relay state after return of power supply

You can set/get the relay state after return of power supply with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the relay state after return of power supply with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>5E – The command code.</td></tr><tr><td>1</td><td>00: Last state. <strong>Default value.</strong><br>01: ON - after return of power supply.<br>02: OFF - after return of power supply.</td></tr></tbody></table>

**Example command**: 0x5E02 – Sets the relay state to be off after return of power supply.
{% endtab %}

{% tab title="GET" %}
#### Get the relay state after return of power supply.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5F – Command code.</td><td>5F – Command code.</td></tr><tr><td>1</td><td> </td><td>00: Last state.<br>01: ON - after return of power supply.<br>02: OFF - after return of power supply.</td></tr></tbody></table>

**Example command:** 0x5F;

**Example response:** 0x5F02 – The relay state is set to be off after return of power supply.
{% endtab %}
{% endtabs %}

## Relay state after overheating protection recovery

{% hint style="info" %}
These commands are available for devices with firmware version ≥ 1.1
{% endhint %}

You can set/get the relay state after overheating protection recovery with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the relay state after overheating protection recovery with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>59 – The command code.</td></tr><tr><td>1</td><td>00: Last state. <strong>Default value.</strong><br>01: OFF - after overheating protection recovery.</td></tr></tbody></table>

**Example command**: 0x5901 – Sets the relay state to be off after overheating protection recovery.
{% endtab %}

{% tab title="GET" %}
#### Get the relay state after overheating protection recovery.

<table data-header-hidden><thead><tr><th width="130.99999999999997"></th><th width="192"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5A – Command code.</td><td>5A – Command code.</td></tr><tr><td>1</td><td> </td><td>00: Last state.<br>01: OFF - after overheating protection recovery.</td></tr></tbody></table>

**Example command:** 0x5A;

**Example response:** 0x5A01 – The relay state is set to be off after overheating protection recovery.
{% endtab %}
{% endtabs %}

## Manual relay state change

This command lets the Application Server know that the relay state has been manually (physically - via a button on the device) changed.

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table><thead><tr><th width="153"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5D – Command code</td></tr><tr><td>1</td><td>XX - Relay state.</td></tr></tbody></table>

**Example uplink**: 0x5D01;

The relay state has been manually changed to 01 (Relay state is ON).
