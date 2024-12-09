# Algorithm 3 - Proportional Integral

This algorithm is an implementation of a typical PI algorithm.

$$
ValveOpening [\%]  = Kp * e + Ki*\sum_{}^{}e
$$

Both the proportional gain Kp and the integral gain Ki can be set with 5 decimal places after the comma.

The algorithm will run on 3 occasions:

&#x20;\- Periodic run (by default every 10 minutes)

&#x20;\- New target temperature is set

&#x20;\- T(measured) - T(target) > 2 degrees Celsius

$$
Integral = \sum_{}^{}e
$$

There's a [software hysteresis](algorithm-3-proportional-integral.md#temperature-hysteresis) in place, which prevents the movement of the motor unless the error is > Thys.

{% hint style="info" %}
The implementation does not have integral reset time - it integrates all previous errors. There's an integral anti wind-up and anti wind-down in place, which limits the integral to 0-50 degrees by default. You can change the maximum value via the command below, increasing the error limit.
{% endhint %}

## Maximum allowed Integral value

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="149">Byte Index</th><th>Byte value - meaning</th></tr></thead><tbody><tr><td><strong>Byte Index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>4C - The command code</td></tr><tr><td>1</td><td>XX - I[15:8]</td></tr><tr><td>2</td><td>XX -I[7:0] </td></tr></tbody></table>

**Example command:** 0x4C012C

I\[15:0] = 012C\[HEX] = 300

Integral = I\[DEC] / 10 = 300 / 10 = 30

The error is set to its maximum allowed value of 30°C

**Default:**\
**I\[15:0] = 01F4\[HEX] = 500\[DEC] = 50°C**
{% endtab %}

{% tab title="GET" %}
<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>4D – The command code.</td><td>4D – The command code.</td></tr><tr><td>1</td><td> </td><td>XX - I[15:8]</td></tr><tr><td>2</td><td></td><td>XX -I[7:0] </td></tr></tbody></table>

**Example command response:** 0x4D03E8

I\[15:0] = 03E8\[HEX] = 1000

Integral = I\[DEC] / 10 = 1000 / 10 = 100

The error is set to its maximum allowed value of 100°C

**Default:**\
**I\[15:0] = 01F4\[HEX] = 50\[DEC] = 50°C**
{% endtab %}
{% endtabs %}

## Proportional gain - Kp

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="149">Byte Index</th><th>Byte value - meaning</th></tr></thead><tbody><tr><td><strong>Byte Index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>37 - The command code</td></tr><tr><td>1</td><td>A[23:16]</td></tr><tr><td>2</td><td>A[15:8]</td></tr><tr><td>3</td><td>A[7:0]</td></tr><tr><td></td><td>A[23:0] = Kp * 131072 <strong>(default value Kp = 6)</strong></td></tr></tbody></table>

**Example downlink:** Setting Kp to 2.74688: 37 05 7E 67

2.74688\*131072 = 360039 = 0x05 7E 67
{% endtab %}

{% tab title="GET" %}
<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>36 – The command code.</td><td>36 – The command code.</td></tr><tr><td>1</td><td> </td><td>A[23:16]</td></tr><tr><td>2</td><td></td><td>A[15:8]</td></tr><tr><td>3</td><td></td><td>A[7:0]</td></tr><tr><td></td><td></td><td>Kp = A[23:0]/131072</td></tr></tbody></table>

**Uplink example:** 0x36123456

A\[23:0] = 0x123456 = 1193046

Kp = 1193046 / 131072 = 9.1
{% endtab %}
{% endtabs %}

## Integral gain - Ki

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="136"></th><th></th></tr></thead><tbody><tr><td><strong>Byte Index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>3E - The command code</td></tr><tr><td>1</td><td>B[23:16]</td></tr><tr><td>2</td><td>B[15:8]</td></tr><tr><td>3</td><td>B[7:0]</td></tr><tr><td></td><td>B[23:0] = Ki * 131072 <strong>(default value: Ki = 1)</strong></td></tr></tbody></table>

**Example downlink:** Setting Ki to 0.412678: 3E 00 D3 4A\
0.412678\*131072 = 54090 = 0x00D34A
{% endtab %}

{% tab title="GET" %}
<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>3D – The command code.</td><td>3D – The command code.</td></tr><tr><td>1</td><td> </td><td>B[23:16]</td></tr><tr><td>2</td><td></td><td>B[15:8]</td></tr><tr><td>3</td><td></td><td>B[7:0]</td></tr><tr><td></td><td></td><td>Ki = B[23:0]/131072</td></tr></tbody></table>

**Example uplink:** 0x3D112233

B\[23:0] = 0x112233 = 1122867

Ki = 1122867/131072 = 8.57
{% endtab %}
{% endtabs %}

## Get the value of the integral

<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>3F – The command code.</td><td>3F – The command code.</td></tr><tr><td>1</td><td> </td><td>Integral [15:8]</td></tr><tr><td>2</td><td> </td><td>Integral [7:0]</td></tr></tbody></table>

The value of the integral is pre-multiplied by 10 by the device, so it can use 0,1 resolution.

**Example uplink:**

If the integral is 2.5, the complete command response is going to be: 0x3F0019&#x20;

Integral \[15:0] = 0x0019 = 25

Integral = 25/10 = 2.5

## PI run period

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="136"></th><th></th></tr></thead><tbody><tr><td><strong>Byte Index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>41 - The command code</td></tr><tr><td>1</td><td>XX = Run period in minutes. <strong>(default value: 10 minutes)</strong></td></tr></tbody></table>

**Example downlink:**

0x410F - sets the run period to 15 minutes.
{% endtab %}

{% tab title="GET" %}
<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>40 – The command code.</td><td>40 – The command code.</td></tr><tr><td>1</td><td> </td><td>XX - Run period in minutes.</td></tr></tbody></table>

**Example uplink:**

0x400B - the run period is 11 minutes
{% endtab %}
{% endtabs %}

## Temperature hysteresis (Thys)

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="136"></th><th></th></tr></thead><tbody><tr><td><strong>Byte Index</strong></td><td><strong>Byte value - meaning</strong></td></tr><tr><td>0</td><td>43 - The command code</td></tr><tr><td>1</td><td>XX = Temperature hysteresis value (Thys), multiplied by 10. <strong>(default value: 0.2 deg. C)</strong></td></tr></tbody></table>

**Min. acceptable value of Thys is 0.2C**

**Example downlink:**

0x4303 - sets the temperature hysteresis to 0.3 degrees Celsius.
{% endtab %}

{% tab title="GET" %}
<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>42 – The command code.</td><td>42 – The command code.</td></tr><tr><td>1</td><td> </td><td>XX - Temperature hysteresis value, multiplied by 10.</td></tr></tbody></table>

**Example uplink:**

0x42FF - The temperature hysteresis is 1.6 degrees Celsius.
{% endtab %}
{% endtabs %}
