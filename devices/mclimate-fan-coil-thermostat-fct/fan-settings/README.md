# Fan Settings

## 1. **Changing the fan speed**

{% hint style="info" %}
If the fan speed is set to auto, the actual speed is determined by an algorithm explained [here](auto-fan-d-settings.md). It's also reported in the [keepalive](../keep-alive.md) of the device.
{% endhint %}

### 1.1 Fan type: 3-speed fan

{% tabs %}
{% tab title="SET" %}
#### You can set the fan speed with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>44 – The command code.</td></tr><tr><td>1</td><td>00: Automatic. <strong>Default</strong><br>01, 02: Low.<br>03, 04: Medium.<br>05, 06: High.</td></tr></tbody></table>

**Example command**: 0x4402 – Sets fan speed to Low.
{% endtab %}

{% tab title="GET" %}
You can get the fan speed with the command. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>45 – Command code</td><td>45 – Command code.</td></tr><tr><td>1</td><td> </td><td>00: Fan speed is automatic. <br>02: Fan speed is Low.<br>04: Fan speed is Medium.<br>06: Fan speed is High.</td></tr></tbody></table>

**Example command:** 0x45;

**Example response:** 0x4502 – Fan speed is set to Low.
{% endtab %}
{% endtabs %}

### 1.2 Fan type: ECM fan

You can change the fan speed with the following command set.

{% tabs %}
{% tab title="SET" %}
You can set the fan speed with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>44 – The command code.</td></tr><tr><td>1</td><td><p>00: Automatic. <strong>Default</strong><br>01: Fan speed 1.<br>02: Fan speed 2.</p><p>...<br>06: Fan speed 6.</p></td></tr></tbody></table>

**Example downlink**: 0x4404 – Sets the fan speed 4.
{% endtab %}

{% tab title="GET" %}
#### This command gets the ECM fan speed. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>45 – Command code</td><td>45 – Command code.</td></tr><tr><td>1</td><td> </td><td><p>00: Automatic.<br>01: Fan speed 1.<br>02: Fan speed 2.</p><p>...<br>06: Fan speed 6.</p></td></tr></tbody></table>

**Example downlink sent by the server:** 0x45;

**Example command:** 0x4504 – The fan speed is 4.
{% endtab %}
{% endtabs %}

## **2. Limiting the selectable fan speed**

{% hint style="danger" %}
This only reflects what's selectable through the device's buttons.
{% endhint %}

### 2.1. Fan type: 3-speed fan

You can change the fan speed limit with the following set of commands.

{% tabs %}
{% tab title="SET" %}
#### You can set the fan speed limit with the command:

<table data-header-hidden><thead><tr><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>46 – The command code.</td></tr><tr><td>1</td><td>00: Low / Medium / High. <strong>Default value.</strong><br>01: Low / Medium.<br>02: Low.<br>03: Fan control deactivated.</td></tr></tbody></table>

**Example downlink**: 0x4601 – Sets the fan speed limit to Low / Medium.
{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>47 – Command code</td><td>47 – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - Fan speed limit value.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x47;

**Example command:** 0x4701 – The fan speed limit is Low / Medium.
{% endtab %}
{% endtabs %}

### **2.2 Fan type: ECM fan**

{% hint style="warning" %}
**Description pending**
{% endhint %}

## **3. ECM Fan Settings**

{% hint style="danger" %}
The following commands are for advanced users only.&#x20;

**Use with great caution.**
{% endhint %}

### 3.1. ECM Fan min/max control voltage settings.

You can change the minimum and maximum voltage of the ECM fan with the following set of commands.

{% tabs %}
{% tab title="SET" %}
#### The command adjusts the voltage range of the ECM fan.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>48 – The command code.</td></tr><tr><td>1</td><td>XX - Vmin[V] * 10.   <strong>Default value:</strong> 0x1E (3V).</td></tr><tr><td>2</td><td>XX - Vmax[V] * 10.  <strong>Default value:</strong> 0x64 (10V).</td></tr></tbody></table>

**Example downlink**: 0x481947;

Sets the Vmin = 2,5V => 2,5 \* 10 = 25 convert to HEX 0x19.&#x20;

Sets the Vmax = 7,1V =>  7,1 \* 10 = 71 convert to HEX 0x47.
{% endtab %}

{% tab title="GET" %}
#### The command extracts the voltage range of the ECM fan.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>49 – Command code</td><td>49 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Vmin[V] * 10.</td></tr><tr><td>2</td><td></td><td>XX - Vmax[V] * 10.</td></tr></tbody></table>

Vmin/max\[V] = XX / 10;

**Example downlink sent by the server:** 0x49;

**Example command:** 0x491947;

0x19 convert to DEC 25 => Vmin = 25 / 10 = 2,5V.

0x47 convert to DEC 71 => Vmax = 71 / 10 = 7,1V.
{% endtab %}
{% endtabs %}

Adjustable range is 0…10V (0,1V resolution).

### 3.2. ECM Relay (F-ON)

This commands allow you to set/get the ECM relay (F-ON) - whether it's activated or deactivated at all.

{% tabs %}
{% tab title="SET" %}
#### Set the ECM relay to activated/deactivated.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>4C – The command code.</td></tr><tr><td>1</td><td><p>00: Deactivated the ECM relay (F-ON);  </p><p>01: Activated the ECM relay (F-ON). <strong>Default state.</strong></p></td></tr></tbody></table>

**Example downlink:** 0x4C01 – Activated the ECM relay (F-ON).
{% endtab %}

{% tab title="GET" %}
#### Get the status of the ECM relay.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>4D – Command code</td><td>4D – Command code</td></tr><tr><td>1</td><td> </td><td>00: The ECM relay (F-ON) is deactivated.<br>01: The ECM relay (F-ON) is activated.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x4D;

**Example command response:** 0x4D01 – The ECM relay (F-ON) is activated.
{% endtab %}
{% endtabs %}

### 3.3. ECM start up time

The ECM fan starts at maximum speed for a specified start up time.

{% tabs %}
{% tab title="SET" %}
#### Set up the start up time.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>4A – The command code.</td></tr><tr><td>1</td><td>XX - ECM start up time.  <strong>Default value:</strong> 0x00 (The function is deactivated). </td></tr></tbody></table>

**Example downlink:** 0x4A03 - Sets the ECM start up time to 3 seconds.
{% endtab %}

{% tab title="GET" %}
#### Get up the the start up time.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>4B – Command code</td><td>4B – Command code</td></tr><tr><td>1</td><td> </td><td>XX - ECM start up time.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x4B;

**Example command response:** 0x4B03 – The ECM start up time is 3 seconds.
{% endtab %}
{% endtabs %}

Acceptable values: 0...20 seconds (1sec. resolution).

### 3.4.  Additional fan modes

{% hint style="info" %}
These commands are available for devices with firmware version ≥ 1.6
{% endhint %}

{% tabs %}
{% tab title="SET" %}
#### Set аdditional fan modes.

<table data-header-hidden><thead><tr><th width="134"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>7A – The command code.</td></tr><tr><td>1</td><td>00: Turn off the fan when the target temperature is reached. <strong>Default.</strong><br>01: Keep the fan running for some time after reaching the target temp.<br>02: The fan runs continuously.</td></tr></tbody></table>

**Example downlink:** 0x7A02 - Sets the fan runs continuously.
{% endtab %}

{% tab title="GET" %}
#### Get аdditional fan modes.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>7B – Command code</td><td>7B – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Additional fan mode.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x7B;

**Example command response:** 0x7B02 – The fan runs continuously.
{% endtab %}
{% endtabs %}

### 3.5. Fan off delay time

{% hint style="info" %}
These commands are available for devices with firmware version ≥ 1.6
{% endhint %}

Continue running for X minutes on LOW speed fan to cool off the heating element.

{% tabs %}
{% tab title="SET" %}
#### Set up the start up time.

<table data-header-hidden><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>78 – The command code.</td></tr><tr><td>1</td><td>XX - Fan off delay time. <strong>Default value:</strong> 0x01 (1min).</td></tr></tbody></table>

**Example downlink:** 0x7803 - Sets the fan off delay time to 3 minutes.
{% endtab %}

{% tab title="GET" %}
#### Get up the the start up time.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="193"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>79 – Command code</td><td>79 – Command code</td></tr><tr><td>1</td><td> </td><td>XX - Fan off delay time.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x79;

**Example command response:** 0x7903 – The fan off delay time is 3 minutes.
{% endtab %}
{% endtabs %}

Acceptable values: 1...255 minutes (1min. resolution).
