# Protections

## Overvoltage threshold

This command sets the threshold temperature in Celsius at which the overheating protection activates.

{% hint style="warning" %}
As long as the measured temperature is above the threshold the relay will be OFF and you will not be able to turn it ON.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="131"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>1E – The command code.</td></tr><tr><td>1</td><td>-</td><td>Threshold temperature in Celsius.<br><strong>Default</strong> <strong>value 0x5A=90</strong>°C<strong>.</strong></td></tr></tbody></table>

**Example downlink**: 0x1E3C – Set the threshold temperature to 0x3C=60°C.
{% endtab %}

{% tab title="GET" %}
This command gets the threshold temperature in Celsius.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="104"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>1F – The command code</td></tr><tr><td>1</td><td>-</td><td>Threshold temperature in Celsius.</td></tr></tbody></table>

**Example command: 0x1F**

**Example response:** 0x**1**F3C – when we separate the value of the threshold temperature from the command code we get 0x3C**,** which is 60°C.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold temperature range is 30...100°C (1.0°C resolution).
{% endhint %}

## Overvoltage threshold

Set the threshold voltage, which when exceeded will turn OFF the relay.

{% hint style="warning" %}
As long as the measured voltage is above the threshold the relay will be OFF and you will not be able to turn it ON.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="144"></th><th width="72"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>20 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Voltage data, bits - [15:8]. </td></tr><tr><td>2</td><td>-</td><td><p>Voltage data, bits - [7:0]. </p><p><strong>Default</strong> <strong>value 0x113=275V.</strong></p></td></tr></tbody></table>

**Example command**: 0x200118 – Set the threshold voltage to 0x0118=280V.
{% endtab %}

{% tab title="GET" %}
Get the threshold voltage.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>21 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Voltage data, bits - [15:8]. </td></tr><tr><td>2</td><td>-</td><td>Voltage data, bits - [7:0].</td></tr></tbody></table>

**Example command: 0x21**

**Example command**: 0x**21**0180 – when we separate the command code value we get the threshold voltage of 0x0118=280V.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold voltage range is 80...300V (1V resolution).
{% endhint %}

## Overcurrent threshold

Set the threshold current, which when exceeded will turn OFF the relay.

{% hint style="warning" %}
As the measured current is above the threshold the relay will be OFF.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="144"></th><th width="126"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>22 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Threshold current in amperes.<br><strong>Default</strong> <strong>value 0x10=16A.</strong></td></tr></tbody></table>

**Example command**: 0x220B – Set the threshold current the 0x0B=11A.
{% endtab %}

{% tab title="GET" %}
Get the threshold current in amperes.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>23 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Threshold current in amperes.</td></tr></tbody></table>

**Example command: 0x23**

**Example command**: 0x**23**0B – when we separate the command code value we get the threshold current of 0x0B=11A.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold current range is 1...16A (1A resolution).
{% endhint %}

## Overpower threshold

Set the threshold power, which when exceeded will turn OFF the relay.

{% hint style="warning" %}
As the measured power is above the threshold the relay will be OFF.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="128"></th><th width="112"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>24 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Power data, bits - [15:8]. </td></tr><tr><td>2</td><td>-</td><td><p>Power data, bits - [7:0]. </p><p><strong>Default</strong> <strong>value 0x0E10=3680W.</strong></p></td></tr></tbody></table>

**Example command**: 0x2407D0 – Set the threshold power to 0x07D0=2000W.
{% endtab %}

{% tab title="GET" %}
Get the threshold voltage.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>25 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Power data, bits - [15:8]. </td></tr><tr><td>2</td><td>-</td><td>Power data, bits - [7:0].</td></tr></tbody></table>

**Example command: 0x25**

**Example command**: 0x2507D0 – when we separate the command code value we get the threshold power of 0x07D0=2000W.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The allowed threshold power range is 100...3680W (1W resolution).
{% endhint %}

## Overheating event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>60 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Number of overheating events.</td></tr><tr><td>2</td><td>-</td><td>Temperature in Celsius.</td></tr></tbody></table>

**Example command: 0x60**

**Example command**: 0x6053C – when we extract the value of the command code, we get the number of overheating events 0x05=5 and a temperature of 0x3C=60°C.
{% endtab %}
{% endtabs %}

## Overvoltage event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>61 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Number of overcurrent events.</td></tr><tr><td>2</td><td>-</td><td>Voltage data, bits - [15:8]. </td></tr><tr><td>3</td><td>-</td><td>Voltage data, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x61**

**Example command**: 0x61030180 – when we extract the value of the command code, we get the number of overvoltage events 0x03=3 and a voltage of 0x0180=280V.
{% endtab %}
{% endtabs %}

## Overcurrent event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>62 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Number of overcurrent events.</td></tr><tr><td>2</td><td>-</td><td>Current data, bits - [15:8]. </td></tr><tr><td>3</td><td>-</td><td>Current data, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x62**

**Example command**: 0x62031952 – when we extract the value of the command code, we get the number of overcurrent events 0x03=3 and a current of 0x1952=6482mA.
{% endtab %}
{% endtabs %}

## Overpower event

The command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

{% tabs %}
{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>63 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Number of overcurrent events.</td></tr><tr><td>2</td><td>-</td><td>Power data, bits - [15:8]. </td></tr><tr><td>3</td><td>-</td><td>Power data, bits - [7:0]. </td></tr></tbody></table>

**Example command: 0x63**

**Example command**: 0x630307D0 – when we extract the value of the command code, we get the number of overpower events 0x03=3 and a power of 0x07D0=2000W.
{% endtab %}
{% endtabs %}
