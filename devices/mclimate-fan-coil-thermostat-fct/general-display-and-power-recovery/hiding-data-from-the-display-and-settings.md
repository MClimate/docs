---
description: >-
  In this page you will learn how to show/hide specific data from the display of
  the device. Even though the data is hidden from the display, you still receive
  it in the keepalive.
---

# Hiding data from the display & settings

### Show/Hide measured temperature

{% tabs %}
{% tab title="SET" %}
#### This command shows/hides the measured temperature on the display.

<table data-header-hidden><thead><tr><th width="146"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>40 – The command code.</td></tr><tr><td>1</td><td><p>00 – Hide the measured temperature;</p><p>01 – Show the measured temperature. <strong>Default state</strong>.</p></td></tr></tbody></table>

**Example command:** 0x4000 – Hide the measured temperature.
{% endtab %}

{% tab title="GET" %}
#### Check whether the measured temperature is shown/hidden.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>41 – Command code</td><td>41 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The measured temperature is hidden;<br>01 - The measured temperature is shown.</td></tr></tbody></table>

**Example command:** 0x41;

**Example response:** 0x4100 – The measured temperature is hidden.
{% endtab %}
{% endtabs %}

### Show/Hide measured humidity

{% tabs %}
{% tab title="SET" %}
#### This command shows/hides the measured humidity on the display.

<table data-header-hidden><thead><tr><th width="137"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>42 – The command code.</td></tr><tr><td>1</td><td><p>00 – Hide humidity;</p><p>01 – Show humidity. <strong>Default state.</strong></p></td></tr></tbody></table>

**Example command:** 0x4200 – Hide the measured humidity
{% endtab %}

{% tab title="GET" %}
#### Check whether the measured temperature is shown/hidden.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>43 – Command code</td><td>43 – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The measured humidity is hidden;<br>01 - The measured humidity is shown.</td></tr></tbody></table>

**Example command**: 0x43;

**Example response**: 0x4300 – The humidity is hidden.
{% endtab %}
{% endtabs %}

## Full display refresh

In order to protect the display of the device from the so-called "ghosting", where an image becomes permanently imprinted on the e-ink display, we have to refresh it fully every max. 24 hours. If you decide, you can lower the full-refresh period, which can remove some dim artefacts from the display's partial refreshes.

{% tabs %}
{% tab title="SET" %}
#### This command sets the full display refresh period.

<table data-header-hidden><thead><tr><th width="147.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>33 – The command code.</td></tr><tr><td>1</td><td>XX - Full display refresh in hours.  <strong>Default value:</strong> 0x0C (12 hours)</td></tr></tbody></table>

Example downlink: 0x330A - set the full display refresh period to 10 hours.
{% endtab %}

{% tab title="GET" %}
#### This command gets the full display refresh period.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>34 – Command code</td><td>34 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Display refresh period in hours.</td></tr></tbody></table>

**Example command:** 0x34;

**Example response:** 0x340F - The full display refresh period is set to 15 hours.
{% endtab %}
{% endtabs %}

**Note:** Acceptable values: 1...24 hours (1 hour resolution).
