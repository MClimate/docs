---
description: >-
  In this page you will learn how to show/hide specific data from the display of
  the device. Even though the data is hidden from the display, you still receive
  it in the keepalive.
---

# Sensor mode & hiding data from the display

## Sensor mode

In some cases you may want to hide the target temperature from the device and show only the current temperature. See image below how the interface looks when the sensor mode is turned on. Clicking the buttons on the device does not do anything in this mode.

<figure><img src="../../../.gitbook/assets/image (33).png" alt="" width="360"><figcaption><p>The Wireless Thermostat in sensor mode</p></figcaption></figure>

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="140"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>39 – The command code.</td></tr><tr><td>1</td><td><p>00 – Turn off the sensor mode; <strong>The default state is off.</strong></p><p>01 – Turn on the sensor mode. </p></td></tr></tbody></table>

**Example downlink:** 0x3901 – Turn on the sensor mode
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>3A – Command code</td><td>3A – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The sensor mode is off;<br>01 - The sensor mode is on.</td></tr></tbody></table>

**Example downlink sent from server**: 0x3А;

**Example response:** 0x3A01 – The sensor mode is on
{% endtab %}
{% endtabs %}

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
