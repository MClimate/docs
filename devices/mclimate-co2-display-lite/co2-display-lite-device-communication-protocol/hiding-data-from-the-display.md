---
description: >-
  In this page you will learn how to show/hide specific data from the display of
  the device. Even though the data is hidden from the display, you still receive
  it in the keepalive.
---

# Hiding data from the display

## **Hiding/showing specific readings on the display**

### Measured temperature

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="146"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>40 – The command code.</td></tr><tr><td>1</td><td><p>00 – Hide the measured temperature;</p><p>01 – Show the measured temperature. <strong>Default state</strong>.</p></td></tr></tbody></table>

**Example downlink:** 0x4000 – Hide the measured temperature.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>41 – Command code</td><td>41 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The measured temperature is hidden;<br>01 - The measured temperature is shown.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x41;

**Example command response:** 0x4100 – The measured temperature is hidden.
{% endtab %}
{% endtabs %}

### Measured humidity

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="137"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>42 – The command code.</td></tr><tr><td>1</td><td><p>00 – Hide humidity;</p><p>01 – Show humidity. <strong>Default state.</strong></p></td></tr></tbody></table>

**Example downlink:** 0x4200 – Hide the measured humidity
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>43 – Command code</td><td>43 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The measured humidity is hidden;<br>01 - The measured humidity is shown.</td></tr></tbody></table>

**Example downlink sent by the server**: 0x43;

**Example command response**: 0x4300 – The humidity is hidden.
{% endtab %}
{% endtabs %}

### Measured light intensity

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>44 – The command code.</td></tr><tr><td>1</td><td><p>00 – Hide light intensity;</p><p>01 – Show light intensity. <strong>Default state.</strong></p></td></tr></tbody></table>

**Example downlink:** 0x4400 – Hide the light intensity.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>45 – Command code</td><td>45 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The light intensity is hidden;<br>01 - The light intensity is shown.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x45;

**Example command response:** 0x4500 – The light intensity is hidden.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
By **Default** all 3 metrics are displayed at the same time (temperature, humidity, and light intensity).
{% endhint %}

### CO2 related images to be shown on the display

You can set how the CO2 measurement is represented on the display. You can select to either a value and/or an emoji.

{% tabs %}
{% tab title="SET" %}
Select one of the 2 options for displaying the CO2 level.

<table data-header-hidden><thead><tr><th width="97"></th><th width="85"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>82 – The command code.</td></tr><tr><td>1</td><td>7:3</td><td>Reserved.</td></tr><tr><td></td><td>1</td><td>1 to show the CO2 value on the display with digits. 0 to hide it.</td></tr><tr><td></td><td>0</td><td>1 to show the CO2 emoji and level on the display. 0 to hide it.</td></tr></tbody></table>

**Example command:** 0x8303 – when we separate the command code value we get 0x**03.** Converting it to binary we get 00000011. Utilizing the last 2 bits we have 11, thus the value will be displayed in digits together with an emoji.
{% endtab %}

{% tab title="GET" %}
Obtain the currently selected option for displaying the CO2 level.

By default, all 2 options are shown.

<table data-header-hidden><thead><tr><th width="95"></th><th width="77"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>83 – The command code.</td></tr><tr><td>1</td><td>7:3</td><td>Reserved.</td></tr><tr><td></td><td>1</td><td>1 if the CO2 digital value is shown on the display. 0 if hidden.</td></tr><tr><td></td><td>0</td><td>1 if the CO2 emoji is shown on the display. 0 if hidden.</td></tr></tbody></table>

**Example command:** 0x8302 – when we separate the command code value we get 0x**02.** Converting it to binary we get 00000010. Utilizing the last 2 bits we have 10, thus only the CO2 value will be shown on the display.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The **Default** all 2 metrics are displayed at the same time (CO2 value and CO2 emoji).
{% endhint %}
