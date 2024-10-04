# Protections

This section defines the protection mechanic of the 16ASPM. It explains how protection limits are set, how protections are triggered and the corresponding events that generate uplink packets.

{% hint style="info" %}
The device works in such a way that when any of the protection thresholds is crossed an uplink is triggered (specific code depending on the protection activated).

This is a one-time uplink to signal that a threshold has been crossed and the protection is active.

Upon recovering from the protection event (crossing the recovery threshold), another uplink is sent (code, specific to the protection type), that is also a one-time event.

Thus, the user is notified when the device has turned off the relay due to a protection being activated and also when the relay has returned to its previous state after recovering from the protection event.
{% endhint %}

## Overheating thresholds

{% hint style="warning" %}
1. **Overheating trigger threshold** - This is the temperature at which the overheating protection is triggered and turns off the relay.
2. **Overheating recovery threshold** - This is the temperature at which the overheating protection will be turned off and allow the relay to go to its previous state.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>1E – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Overheating trigger temperature;<br><strong>Default</strong> <strong>value 0x5F = 95</strong>°C<strong>.</strong></td></tr><tr><td>2</td><td>-</td><td><p>XX - Overheat recovery temperature.</p><p><strong>Default</strong> <strong>value 0x46 = 70</strong>°C<strong>.</strong></p></td></tr></tbody></table>

**Example downlink**: 0x1E5A3C – Set the trigger temperature to 0x5A = 90°C and the recovery temperature to 0x3C = 60°C.
{% endtab %}

{% tab title="GET" %}
This command gets the threshold temperature in Celsius.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="104"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>1F – The command code</td></tr><tr><td>1</td><td>-</td><td>XX - Overheat trigger threshold temperature;</td></tr><tr><td>2</td><td>-</td><td>XX - Overheat recovery threshold temperature.</td></tr></tbody></table>

**Example command: 0x1F**

**Example response:** 0x1F5A3C – When we separate the value of the trigger temperature to 0x5A = 90°C and recovery temperature 0x3C = 60°C.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold temperature range is 30...100°C (1.0°C resolution).
{% endhint %}

## Overvoltage thresholds

{% hint style="warning" %}
1. **Overvoltage trigger threshold** - This is the threshold at which the overvoltage protection is triggered and turns off the relay.
2. **Overvoltage recovery threshold** - This is the threshold at which the overvoltage protection will be turned off and allow the relay to go to previous state, after 1min.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="144"></th><th width="112"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>20 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Overvoltage trigger threshold, bits  - [15:8]. </td></tr><tr><td>2</td><td>-</td><td><p>XX - Overvoltage trigger threshold, bits - [7:0]. </p><p><strong>Default</strong> <strong>value 0x0113 = 275V.</strong></p></td></tr><tr><td>3</td><td>-</td><td><p>XX - Overvoltage recovery threshold. </p><p><strong>Default</strong> <strong>value 0xFA = 250V.</strong></p></td></tr></tbody></table>

**Example command**: 0x20010EF5 – Set the trigger voltage to 0x010E = 270V and recovery voltage 0xF5 = 245V.&#x20;
{% endtab %}

{% tab title="GET" %}
Get the threshold voltage.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>21 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Overvoltage trigger threshold, bits  - [15:8]. </td></tr><tr><td>2</td><td>-</td><td>XX - Overvoltage trigger threshold, bits - [7:0].</td></tr><tr><td>3</td><td>-</td><td>XX - Overvoltage recovery threshold. </td></tr></tbody></table>

**Example command: 0x21**

**Example command**: 0x**21**0180 – when we separate the command code value we get the threshold voltage of 0x0118 = 280V.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold voltage range is 1...300V (1V resolution).
{% endhint %}

## Overcurrent threshold

Set the current threshold, which when exceeded will turn OFF the relay.

{% hint style="warning" %}
As long as the measured current is above the threshold the relay will be OFF.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="144"></th><th width="126"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>22 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Threshold current in amperes.<br><strong>Default</strong> <strong>value 0x10 = 16A.</strong></td></tr></tbody></table>

**Example command**: 0x220B – Set the threshold current to 0x0B = 11A.
{% endtab %}

{% tab title="GET" %}
Get the threshold current in amperes.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>23 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Threshold current in amperes.</td></tr></tbody></table>

**Example command: 0x23**

**Example command**: 0x**23**0B – When we separate the command code value we get the threshold current of 0x0B = 11A.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold current range is 1...16A (1A resolution).
{% endhint %}

## Overpower threshold

Set the power threshold, which when exceeded will turn OFF the relay.

{% hint style="warning" %}
As long as the measured power is above the threshold the relay will be OFF.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="128"></th><th width="112"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>24 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Power data, bits - [15:8]. </td></tr><tr><td>2</td><td>-</td><td><p>XX - Power data, bits - [7:0]. </p><p><strong>Default</strong> <strong>value 0x0E60 = 3680W.</strong></p></td></tr></tbody></table>

**Example command**: 0x2407D0 – Set the power threshold to 0x07D0 = 2000W.
{% endtab %}

{% tab title="GET" %}
Get the threshold voltage.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>25 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Power data, bits - [15:8]. </td></tr><tr><td>2</td><td>-</td><td>XX - Power data, bits - [7:0].</td></tr></tbody></table>

**Example command: 0x25**

**Example command**: 0x2507D0 – When we separate the command code value we get the threshold power of 0x07D0 = 2000W.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold power range is 100...3680W (1W resolution).
{% endhint %}

## Overheating event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>60 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Number of overheating events.</td></tr><tr><td>2</td><td>-</td><td>XX - Temperature in Celsius.</td></tr></tbody></table>

**Example command: 0x60**

**Example command**: 0x60053C – When we extract the value of the command code, we get the number of overheating events 0x05 = 5 and a temperature of 0x3C = 60°C.
{% endtab %}
{% endtabs %}

## Overheating recovery event

{% hint style="warning" %}
This command is available for devices with firmware version ≥ 1.1
{% endhint %}

{% hint style="info" %}
When the overheating protection activates the device starts a timer that runs until the temperature drops below the threshold and the device resumes normal operation. At this point an uplink is transmitted that reports the measured time, giving insights in how much time the device was off due to overheating.
{% endhint %}

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>70 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Overheating protection running time, bits - [15:8];</td></tr><tr><td>2</td><td>-</td><td>XX - Overheating protection running time, bits - [7:0].</td></tr></tbody></table>

**Example command: 0x70**

**Example command**: 0x70002A – When we extract the value of the command code, we get the overheating protection running time 0x002A = 42 seconds.
{% endtab %}
{% endtabs %}

## Overvoltage event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>61 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Number of overcurrent events.</td></tr><tr><td>2</td><td>-</td><td>XX - Voltage data, bits - [15:8]. </td></tr><tr><td>3</td><td>-</td><td>XX - Voltage data, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x61**

**Example command**: 0x61030180 – When we extract the value of the command code, we get the number of overvoltage events 0x03 = 3 and a voltage of 0x0180 = 280V.
{% endtab %}
{% endtabs %}

## Overvoltage recovery event

{% hint style="warning" %}
This command is available for devices with firmware version ≥ 1.1
{% endhint %}

{% hint style="info" %}
When the overvoltage protection activates the device starts a timer that runs until the voltage drops below the threshold value and the device resumes normal operation. At this point an uplink is transmitted that reports the measured time, giving insights in how much time the device was off due to overvoltage.
{% endhint %}

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>71 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Overvoltage protection running time, bits - [15:8];</td></tr><tr><td>2</td><td>-</td><td>Overvoltage protection running time, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x71**

**Example command**: 0x71001A – When we extract the value of the command code, we get the overvoltage protection running time 0x001A = 26 seconds.
{% endtab %}
{% endtabs %}

## Overcurrent event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>62 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Number of overcurrent events.</td></tr><tr><td>2</td><td>-</td><td>XX - Current data, bits - [15:8]. </td></tr><tr><td>3</td><td>-</td><td>XX - Current data, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x62**

**Example command**: 0x62031952 – When we extract the value of the command code, we get the number of overcurrent events 0x03 = 3 and a current of 0x1952 = 6482mA.
{% endtab %}
{% endtabs %}

## Overcurrent recovery event

{% hint style="warning" %}
This command is available for devices with firmware version ≥ 1.1
{% endhint %}

{% hint style="info" %}
Because of the way the device operates, it recovers almost instantaneously from an Overcurrent event, thus no outage time as with the Overheating and Overvoltage protections is measured. Instead the internal temperature of the device at the time of event/recovery event is measured and reported.
{% endhint %}

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>72 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Temperature when overcurrent protection is triggered.</td></tr></tbody></table>

**Example command: 0x72**

**Example command**: 0x723E – When we extract the value of the command code, we get the  temperature  when overcurrent protection is triggered - 0x3E = 62°C.
{% endtab %}
{% endtabs %}

## Overpower event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>63 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Number of overcurrent events.</td></tr><tr><td>2</td><td>-</td><td>XX - Power data, bits - [15:8]. </td></tr><tr><td>3</td><td>-</td><td>XX - Power data, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x63**

**Example command**: 0x630307D0 – When we extract the value of the command code, we get the number of overpower events 0x03 = 3 and a power of 0x07D0 = 2000W.
{% endtab %}
{% endtabs %}

## Overpower recovery event

{% hint style="warning" %}
This command is available for devices with firmware version ≥ 1.1
{% endhint %}

{% hint style="info" %}
Because of the way the device operates, it recovers almost instantaneously from an Overpower event, thus no outage time as with the Overheating and Overvoltage protections is measured. Instead the internal temperature of the device at the time of event/recovery event is measured and reported.
{% endhint %}

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>73 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX -Temperature when overpower protection is triggered.</td></tr></tbody></table>

**Example command: 0x73**

**Example command**: 0x732C – When we extract the value of the command code, we get the  temperature when overpower protection is triggered - 0x2C = 44°C.
{% endtab %}
{% endtabs %}
