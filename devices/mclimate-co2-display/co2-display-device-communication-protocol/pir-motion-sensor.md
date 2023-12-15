---
description: >-
  In this page, you will learn how the PIR sensor works and what available
  settings you can change.
---

# PIR (Motion sensor)

Since the device is primarily solar-powered, the PIR sensor cannot be always ON, as the device will need a lot of light on average.

Therefore, we have implemented a duty-cycle on the PIR - turning it ON for certain period of time and turning it OFF for some period. This means that the device may not always report accurate movement detection.

{% hint style="success" %}
If you need to have the PIR constantly enabled and detecting movement, you have to insert 2 or 4 AA batteries and reconfigure the settings of the PIR sensor.

If you want to do this, we recommend sending the following downlink to the device:

0x3C014A0000
{% endhint %}

## PIR status

This commands allow you to set/get the PIR status - whether it's enabled or disabled at all. By default, the PIR is disabled.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>3C – The command code.</td></tr><tr><td>1</td><td><p>00 – Disable the PIR sensor;<br><strong>Default</strong> <strong>value of 0x00, disabled.</strong></p><p>01 – Enable the PIR sensor. </p></td></tr></tbody></table>

**Example downlink:** 0x3C01 – Turn on the PIR sensor.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>3D – Command code</td><td>3D – Command code</td></tr><tr><td>1</td><td> </td><td>00 - The PIR sensor is disabled.<br>01 - The PIR sensor is enabled</td></tr></tbody></table>

**Example downlink sent by the server:** 0x3D;

**Example command response:** 0x3D01 – The PIR sensor is on.
{% endtab %}
{% endtabs %}

## PIR blind period

After detecting a movement in the room, the PIR sensor is disabled for the specified blind period.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="140"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>4C – The command code.</td></tr><tr><td>1</td><td>00 –  PIR check period data, bits 15:8;</td></tr><tr><td>2</td><td><p>0A – PIR check period data, bits 7:0. </p><p>Minimum value = 15sec.<br><strong>Default</strong> <strong>value 0x000A=10min.</strong></p></td></tr></tbody></table>
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>4D – Command code</td><td>4D – Command code</td></tr><tr><td>1</td><td> </td><td>XX - PIR sensor blind period - bits 15:8</td></tr><tr><td>2</td><td></td><td>XX - PIR sensor blind period - bits 7:0</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

## PIR check period

This value instructs the sensor what's the period between measurements. Outside this time, the sensor is not powered.

When the value is 0, the PIR is constantly powered and checking for movements.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="161"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>4A – The command code.</td></tr><tr><td>1</td><td>00 –  PIR check period data, bits 15:8;</td></tr><tr><td>2</td><td><p>36 – PIR check period data, bits 7:0. </p><p>Minimum value = 0sec. <br><strong>Default value 0x0036=54sec.</strong></p></td></tr></tbody></table>

**Example downlink:** 0x4A0036 – Set the PIR check period to 54sec.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>4B – Command code</td><td>4B – Command code</td></tr><tr><td>1</td><td> </td><td>XX - PIR sensor check period - bits 15:8</td></tr><tr><td>2</td><td></td><td>XX - PIR sensor Check period - bits 7:0</td></tr></tbody></table>

**Example downlink sent by the server:** 0x4B;

**Example command response:** 0x4B0036 –  Measurement period of the PIR sensor = 54sec.
{% endtab %}
{% endtabs %}

## PIR measurement period

The PIR Measurement period is a value that instructs the sensor how long after turning on + initialization period it should be checking for movements before going back to sleep.

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="145"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>48 – The command code.</td></tr><tr><td>1</td><td><p>03 – PIR measurement time period. </p><p>Minimum value = 3sec. <br><strong>Default value 0x03=3sec.</strong></p></td></tr></tbody></table>

Example command: 0x4803 – Set the measurement period of the PIR sensor = 3sec.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>49 – Command code</td><td>49 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - PIR sensor measurement period [sec]</td></tr></tbody></table>

**Example downlink sent by the server:** 0x49;

**Example command response:** 0x4903 –  Measurement period of the PIR sensor = 3sec.
{% endtab %}
{% endtabs %}

## PIR sensitivity

The PIR sensitivity can be set from 12 to 255. The minimum value we advise setting is 12 or 0x0C - the sensor will be super sensitive to movements.

{% hint style="info" %}
The higher the value, the less sensitive the PIR sensor is to movement.&#x20;

Minimum = 12 - very sensitive

Maximum = 255 - less sensitive
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>3Е – The command code.</td></tr><tr><td>1</td><td>XX - PIR sensor sensitivity.<br><strong>Default value 0x14=20.</strong></td></tr></tbody></table>

**Example downlink:** 0x3E14 – Set PIR sensor sensitivity 0x14 = 20.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>3F – Command code</td><td>3F – Command code</td></tr><tr><td>1</td><td> </td><td>XX - The sensitivity of the PIR sensor</td></tr></tbody></table>

**Example downlink sent by the server:** 0x3F;

**Example command response:** 0x3F14 – The sensitivity of the PIR sensor = 0x14 => converted to decimal = 20.
{% endtab %}
{% endtabs %}

## PIR Initialization period

Every time the sensor turns on, it needs a little time to get used to the light conditions in the room.

{% hint style="danger" %}
We do not advise changing the default initialization period!
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="139"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>46 – The command code.</td></tr><tr><td>1</td><td><p>XX – PIR sensor initialization period in seconds. </p><p>Minimum value = 3sec.<br><strong>Default</strong> <strong>value 0x03=3sec.</strong></p></td></tr></tbody></table>

**Example downlink:** 0x4603 – Set the initialization period of the PIR sensor = 3sec.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>47 – Command code</td><td>47 – Command code</td></tr><tr><td>1</td><td> </td><td>03 - PIR initialisation period.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x47;

**Example command response:** 0x4703 –  Initialisation period of the PIR sensor = 3 sec.
{% endtab %}
{% endtabs %}

