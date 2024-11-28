# CO2 measurement settings

## CO2 measurement blind time

When CO2 measurement is started by button press, for the given blind time next start by button press will be forbidden.

{% tabs %}
{% tab title="SET" %}
This command sets the the measuring blind time in minutes.

<table data-header-hidden><thead><tr><th width="131"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>81 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Measuring blind time in minutes.<br><strong>Default</strong> <strong>value 0x01=1min.</strong></td></tr></tbody></table>

**Example downlink**: 0x810E – when we separate the value of the time from the command code we get 0x**0E,** which is 14 min.
{% endtab %}

{% tab title="GET" %}
This command gets the currently set value in minutes.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="104"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>80 – The command code</td></tr><tr><td>1</td><td>-</td><td>Measuring blind time in minutes.</td></tr></tbody></table>

**Example command: 0x80**

**Example response:** 0x**80**0F – when we separate the value of the time from the command code we get 0x0&#x46;**,** which is 15 min.
{% endtab %}
{% endtabs %}

## CO2 boundary levels

Configure the boundary levels of the CO2 zones.

{% tabs %}
{% tab title="SET" %}
Set the boundary levels.

<table data-header-hidden><thead><tr><th width="133"></th><th width="106"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>1E – The command code.</td></tr><tr><td>1</td><td>15:8</td><td>Good-medium CO2 zone boundary value in ppm [high byte].</td></tr><tr><td>2</td><td>7:0</td><td>Good-medium CO2 zone boundary value in ppm [low byte].<br><strong>Default value 0x0384=900ppm.</strong></td></tr><tr><td>3</td><td>15:8</td><td>Medium-bad CO2 zone boundary value in ppm [high byte].</td></tr><tr><td>4</td><td>7:0</td><td>Medium-bad CO2 zone boundary value in ppm [low byte].<br><strong>Default value 0x05DC=1500ppm.</strong></td></tr></tbody></table>

**Example command**: 0x1E038405DC – set the Good-medium CO2 zone to 0x3840=900ppm and the Medium-bad CO2 zone to 0x05DC=1500ppm.
{% endtab %}

{% tab title="GET" %}
Get the boundary levels.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="110"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>1F – The command code.</td></tr><tr><td>1</td><td>15:8</td><td>Good-medium CO2 zone boundary value in ppm [high byte].</td></tr><tr><td>2</td><td>7:0</td><td>Good-medium CO2 zone boundary value in ppm [low byte].</td></tr><tr><td>3</td><td>15:8</td><td>Medium-bad CO2 zone boundary value in ppm [high byte].</td></tr><tr><td>4</td><td>7:0</td><td>Medium-bad CO2 zone boundary value in ppm [low byte].</td></tr></tbody></table>

**Example command: 0x1F**

**Example response:** 0x**1F**038405DC – when we separate the command code value we get 0x038405D&#x43;**,** which corresponds to Good-medium CO2 zone of 0x3840=900ppm and the Medium-bad CO2 zone of 0x05DC=1500ppm.
{% endtab %}
{% endtabs %}

## CO2 auto-zero value

{% hint style="info" %}
In practice, you are not supposed to change the auto-zero value, as this would directly affect the internal self-calibration algorithm.&#x20;

\
You can get the CO2 auto-zero value in order to check whether normal calibration has worked correctly - e.g. expected values are in the range 0-1500ppm. If you see value of e.g. 20000, please use the SET function to set it back to 400ppm and leave the sensor at fresh air for at least 1.2xMeasurement intervals (if you are using default settings, expose the sensor to fresh air for at least 15 minutes).
{% endhint %}

This command set is used by the device for CO2 measurements compensation in order to get 400ppm in fresh air.

{% tabs %}
{% tab title="SET" %}
Set the auto-zero value.

<table data-header-hidden><thead><tr><th width="139"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>20 – The command code.</td></tr><tr><td>1</td><td>15:8</td><td>Auto-zero CO2 value in ppm [higher byte].</td></tr><tr><td>2</td><td>7:0</td><td>Auto-zero CO2 value in ppm [lower byte].<br><strong>Default</strong> <strong>value 0x0190=400ppm.</strong></td></tr></tbody></table>

**Example command**: 0x200221 – Set the CO2 auto-zero value to 0x0221=545ppm.
{% endtab %}

{% tab title="GET" %}
Get the auto-zero value.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>21 – The command code.</td></tr><tr><td>1</td><td>15:8</td><td>Auto-zero CO2 value in ppm [high byte].</td></tr><tr><td>2</td><td>7:0</td><td>Auto-zero CO2 value in ppm [low byte].</td></tr></tbody></table>

**Example command: 0x21**

**Example command**: 0x**21**0221 – when we separate the command code value we get the CO2 auto-zero value of 0x0221=545ppm.
{% endtab %}
{% endtabs %}

## CO2 measurement period

The commands configures the CO2 measurement period.

{% tabs %}
{% tab title="SET" %}
Set the measurement period.

<table data-header-hidden><thead><tr><th width="139"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>24 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Measurement period in the Good-zone in minutes.<br><strong>Default</strong> <strong>value 0x0F=15min.</strong></td></tr><tr><td>2</td><td>-</td><td>Measurement period in the Medium-zone in minutes.<br><strong>Default</strong> <strong>value 0x0F=15min.</strong></td></tr><tr><td>3</td><td>-</td><td>Measurement period in the Bad-zone in minutes.<br><strong>Default</strong> <strong>value 0x0F=15min.</strong></td></tr></tbody></table>

**Example command**: 0x240A0A0A – Set the measurement periods for all 3 zones to be the same 0x0A=10min.
{% endtab %}

{% tab title="GET" %}
Get the measurement period.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>25 – The command code.</td></tr><tr><td>1</td><td>-</td><td>Measurement period in the Good-zone in minutes.</td></tr><tr><td>2</td><td>-</td><td>Measurement period in the Medium-zone in minutes.</td></tr><tr><td>2</td><td>-</td><td>Measurement period in the Bad-zone in minutes.</td></tr></tbody></table>

**Example command: 0x25**

**Example command**: 0x**25**0A0A0A – when we separate the command code value we get the measurement period of 0x0A=10min, which is the same for all 3 zones.
{% endtab %}
{% endtabs %}

## CO2 auto-zero period

Default auto-zero period, after the factory auto-zeroing, is 192 hours (8 days). During this period the lowest measured CO2 value is accepted as 400ppm and the auto-zero value is obtained automatically. If The period is 0, automatic auto-zero function is disabled, but the obtained or set with command auto-zero value is still used internally.

{% tabs %}
{% tab title="SET" %}
Set the auto-zero period.

<table data-header-hidden><thead><tr><th width="139"></th><th width="101"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>2A – The command code.</td></tr><tr><td>1</td><td>-</td><td>Auto-zero period in hours.<br><strong>Default</strong> <strong>value 0xC0=192hrs.</strong></td></tr></tbody></table>

**Example command**: 0x2A48 – Set the CO2 auto-zero period to 0x48=72hrs.
{% endtab %}

{% tab title="GET" %}
Get the auto-zero period.

<table data-header-hidden><thead><tr><th width="133.99999999999997"></th><th width="111"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>2B – The command code.</td></tr><tr><td>1</td><td>15:8</td><td>Auto-zero period in hours.</td></tr></tbody></table>

**Example command: 0x2B**

**Example command**: 0x**2B**48 – when we separate the command code value we get the auto-zero period of 0x48=72hrs.
{% endtab %}
{% endtabs %}
