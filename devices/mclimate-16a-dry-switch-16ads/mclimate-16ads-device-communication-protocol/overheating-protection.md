# Overheating protection

This section defines the protection mechanic of the 16ADS. It explains how protection limits are set, how protection is triggered and the corresponding events that generate uplink packets.

{% hint style="info" %}
This section defines the protection mechanic of the 16ADS. It explains how protection limits are set, how the protection is triggered and the corresponding events that generate uplink packets.

The device works in such a way that when the protection threshold is crossed an uplink is triggered.

This is a one-time uplink to signal that the threshold has been crossed and the protection is active.

Upon recovering from the protection event (crossing the recovery threshold), another uplink is sent, that is also a one-time event.

Thus, the user is notified when the device has turned off the relay due to the protection being activated and also when the relay has returned to its previous state after recovering from the protection event.
{% endhint %}

## Overheating thresholds

{% hint style="info" %}
1. **Overheating trigger threshold** - This is the temperature at which the overheating protection is triggered and turns off the relay.
2. **Overheating recovery threshold** - This is the temperature at which the overheating protection will be turned off and allow the relay to go to its previous state.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
\


<table data-header-hidden><thead><tr><th width="129"></th><th width="106"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>1E – The command code.</td></tr><tr><td>1</td><td>-</td><td><p>XX - Overheating trigger temperature; </p><p><strong>Default</strong> <strong>value 0x5F = 95</strong>°C<strong>.</strong></p></td></tr><tr><td>2</td><td>-</td><td><p>XX - Overheat recovery temperature.</p><p><strong>Default</strong> <strong>value 0x46 = 70</strong>°C<strong>.</strong></p></td></tr></tbody></table>

**Example downlink**: 0x1E5A3C – Set the trigger temperature to 0x5A = 90°C and the recovery temperature to 0x3C = 60°C.
{% endtab %}

{% tab title="GET" %}
This command gets the threshold temperature in Celsius.

<table data-header-hidden><thead><tr><th width="139"></th><th width="102"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>1F – The command code</td></tr><tr><td>1</td><td>-</td><td>XX - Overheat trigger threshold temperature;</td></tr><tr><td>2</td><td>-</td><td>XX - Overheat recovery threshold temperature.</td></tr></tbody></table>

**Example command: 0x1F**

**Example response:** 0x1F5A3C – When we separate the value of the trigger temperature to 0x5A = 90°C and recovery temperature 0x3C = 60°C.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold temperature range is 30...100°C (1.0°C resolution).
{% endhint %}

## Overheating event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
Get the overheating event parameters.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>60 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Number of overheating events.</td></tr><tr><td>2</td><td>-</td><td>Temperature in Celsius.</td></tr></tbody></table>

**Example command: 0x60**

**Example command**: 0x60053C – when we extract the value of the command code, we get the number of overheating events 0x05 = 5 and a temperature of 0x3C = 60°C.
{% endtab %}
{% endtabs %}

## Overheating recovery event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="147"></th><th width="113"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>70 – The command code.</td></tr><tr><td>1</td><td>-</td><td>XX - Overheating protection running time, bits - [15:8];</td></tr><tr><td>2</td><td>-</td><td>XX - Overheating protection running time, bits - [7:0].</td></tr></tbody></table>

**Example command: 0x70**

**Example command**: 0x70002A – When we extract the value of the command code, we get the overheating protection running time 0x002A = 42 seconds.
{% endtab %}
{% endtabs %}

