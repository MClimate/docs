---
description: >-
  Depending on the application you can choose different wiring schemes for the
  FCT (with respect to the Fan). This section will provide information on the
  seven possible schemes.
---

# ⚡ Wiring diagrams (applications) & Operational Modes

There is a total of 7 possible applications each with its specific wiring. They you can group them in 2 categories, depending whether you are utilizing a 3-speed or an ECM fan.

The two categories have very different wiring so it is advisable to examine the wiring diagram below in detail in order to choose the right application/wiring for your specific installation.

A summary can be found in the table below:

| Application code | Fan Type | Description                                                              |
| ---------------- | -------- | ------------------------------------------------------------------------ |
| 00               | 3-speed  | 2-pipe ON/OFF                                                            |
| 01               | 3-speed  | 2-pipe ON/OFF 3-wire  valve (220VAC); TiO2 / ESP                         |
| 02               | 3-speed  | 4-pipe ON/OFF 3-wire  valve (220VAC); TiO2 / ESP                         |
| 03               | ECM fan  | 4-pipe ON/OFF; optional TiO2 / ESP                                       |
| 04               | ECM fan  | 2-pipe ON/OFF; optional TiO2 / ESP                                       |
| 05               | ECM fan  | 2-pipe ON/OFF 3-wire  valve; optional TiO2 / ESP                         |
| 06               | ECM fan  | 2-pipe ON/OFF 3-wire  valve; optional TiO2 / ESP, optional floor heating |

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## Wiring Diagrams (applications)

You can change the applications with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the target applications with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>60 – The command code.</td></tr><tr><td>1</td><td><p>00: Application 0. <strong>Default value.</strong><br>01: Application 1.<br>02: Application 2.</p><p>...<br>05: Application 5.</p></td></tr></tbody></table>

**Example downlink**: 0x6001 – 0x01: Sets the application 1.
{% endtab %}

{% tab title="GET" %}
#### This command gets the application. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>61– Command code</td><td>61 – Command code</td></tr><tr><td>1</td><td> </td><td><p>00: Application 0.<br>01: Application 1.<br>02: Application 2.</p><p>...<br>05: Application 5.</p></td></tr></tbody></table>

**Example downlink sent by the server:** 0x61;

**Example command:** 0x6101 – 0x01: Application 1.
{% endtab %}
{% endtabs %}

## Allowed Operational Modes

You can change the allowed operational modes with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the allowed operational mode with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>54 – The command code.</td></tr><tr><td>1</td><td><p>00: Ventilation/Heating/Cooling. <strong>Default value.</strong></p><p>01: Ventilation/Heating. </p><p>02: Ventilation/Cooling.</p></td></tr></tbody></table>

**Example downlink**: 0x5401 – Sets the allowed operational mode to Ventilation/Heating.&#x20;
{% endtab %}

{% tab title="GET" %}
#### This command gets the allowed operating mode.&#x20;

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="192"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>55 – Command code</td><td>55 – Command code.</td></tr><tr><td>1</td><td> </td><td><p>00: Ventilation/Heating/Cooling.</p><p>01: Ventilation/Heating. </p><p>02: Ventilation/Cooling.</p></td></tr></tbody></table>

**Example downlink sent by the server:** 0x55;

**Example command:** 0x5501 – The allowed operating mode is Ventilation/Heating.

The keepalive data in the example above is omitted for clarity.
{% endtab %}
{% endtabs %}

## Change current operational mode

You can set/get the current operational mode with the following commands:

{% tabs %}
{% tab title="SET" %}
#### You can set the operational mode with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>52 – The command code.</td></tr><tr><td>1</td><td><p>00: Ventilation.</p><p>01: Heating.<br>02: Cooling.</p></td></tr></tbody></table>

**Example downlink**: 0x5201 –  Sets the operational mode heating.
{% endtab %}

{% tab title="GET" %}
#### This command gets the operational mode.&#x20;

<table data-header-hidden><thead><tr><th width="98.99999999999997"></th><th width="206"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>53 – Command code</td><td>53 – Command code.</td></tr><tr><td>1</td><td> </td><td><p>00: Ventilation.</p><p>01: Heating.<br>02: Cooling.</p></td></tr></tbody></table>

**Example downlink sent by the server:** 0x53;

**Example uplink sent by the device:** 0x5301 – The current operational mode is heating.

The keepalive data in the example above is omitted for clarity.
{% endtab %}
{% endtabs %}

## Valve open/close time

{% hint style="danger" %}
This is applicable only to applications: 01 and 05

**Feature for advanced users, use with care.**
{% endhint %}

You can change the valve open/close time with the following command set.

{% tabs %}
{% tab title="SET" %}
#### Set the valve open time.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>31 – The command code.</td></tr><tr><td>1</td><td>XX - Valve open/close time. <strong>Default value:</strong> 0xA0 (160 seconds). </td></tr></tbody></table>

**Example downlink:** 0x310F - Sets the valve open/close time to 15 seconds.
{% endtab %}

{% tab title="GET" %}
#### Get the valve open time.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>32 – Command code</td><td>32 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Valve open/close time.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x32;

**Example command response:** 0x320F – The valve open/close time time is 15 seconds.
{% endtab %}
{% endtabs %}

Acceptable values: 1...255 seconds (1sec. resolution).
