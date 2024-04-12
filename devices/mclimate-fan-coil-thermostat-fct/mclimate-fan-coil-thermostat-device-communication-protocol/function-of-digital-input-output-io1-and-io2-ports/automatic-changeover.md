# Automatic changeover

In case your Fan Coil Unit is 2-pipe type and you use it both for heating in the winter and cooling in the summer, you can add an additional 10k NTC sensor to the OCC port of the FCT and let the FCT determine if it's hot or cold water running in the system and therefore whether it should set the current operational mode to heating or cooling.

{% hint style="info" %}
The automatic change-over is applicable only in applications 00 and 01 - 2-pipe fan coil systems with 3-speed fan.
{% endhint %}

When the FCT detects that it's hot water running through the pipe (using the installed 10k NTC sensor) it automatically changes the current operational mode to "Heating" and allowed operation modes to "Heating/Ventilation" when the threshold temperature is reached. &#x20;

Alternatively, if using the installed 10k NTC the FCT measures that the water in the pipe is cold, it automatically changes the current operational mode to "Cooling" and the allowed operational modes to "Cooling/Ventilation" when the threshold temperature is reached.

{% hint style="success" %}
When you enable the automatic change-over, the OCC port cannot be used for any other feature (e.g. dew-point sensor, filter alarm sensor, occupancy switch, etc).
{% endhint %}

{% hint style="danger" %}
Change-over is disabled when the frost protection is active. It is re-enabled once frost protection is no longer active.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
#### The command enables/disables automatic changeover.

<table data-header-hidden><thead><tr><th width="140"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>5E – The command code.</td></tr><tr><td>1</td><td><p>00: Deactivated.  <strong>Default value.</strong></p><p>01: Activated. </p></td></tr></tbody></table>

**Example downlink:** 0x5E01 – Activated automatic changeover.
{% endtab %}

{% tab title="GET" %}
#### Get the automatic changeover status.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>5F – Command code</td><td>5F – Command code</td></tr><tr><td>1</td><td> </td><td>00:  Automatic changeover is deactivated. <br>01:  Automatic changeover is activated.</td></tr></tbody></table>

**Example downlink sent from server:** 0x5F;

**Example uplink response:** 0x5F01 – Automatic changeover is activated.
{% endtab %}
{% endtabs %}

## Threshold changeover temperatures

You can change the threshold changeover temperature with the following command set.

{% tabs %}
{% tab title="SET" %}
#### This command is used to set the threshold changeover temperatures values.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>64 – The command code.</td></tr><tr><td>1</td><td>XX – Cooling threshold temperature.  <strong>Default value:</strong> 0x0F (15°C).</td></tr><tr><td>2</td><td>XX – Heating threshold temperature.  <strong>Default value:</strong> 0x28 (40°C).</td></tr></tbody></table>

**Example command:** 0x64102B – Sets the cooling threshold temp. to 16°C and the heating threshold temp. to 43°C.
{% endtab %}

{% tab title="GET" %}
#### This command is used to get the threshold changeover temperatures.&#x20;

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>65 – Command code</td><td>65 – Command code</td></tr><tr><td>1</td><td> </td><td>XX – Cooling threshold temperature.</td></tr><tr><td>2</td><td></td><td>XX – Heating threshold temperature.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x65;

**Example command:** 0x65102B – The cooling threshold temp. is 16°C and the heating threshold temp. is 43°C.

In the example above, the keep-alive data is omitted from the response for clarity.
{% endtab %}
{% endtabs %}

The allowed cooling threshold temperature range is 5...20°C (1°C  resolution).

The allowed heating threshold temperature range is 30...60°C (1°C  resolution).
