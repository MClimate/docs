# Flood event - Available configurations

## Alarm uplink periodicity

{% hint style="info" %}
NOTE: Available for firmware version 1.5 or later.
{% endhint %}

When a flood is detected, you can use this command to define how often do you want to receive an uplink. [The uplink type depends on the configuration you have selected](flood-event-available-configurations.md#flood-event-uplink-messages-type).

When the period zero while AND there's a flood, the uplink is sent continuously respecting the duty cycle. (e.g. on SF7, it'll be sending uplinks roughly every 7 seconds).

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="139">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>08 - Set flood event send time.</td></tr><tr><td>1</td><td>XX - Flood event send time in minutes.  <strong>Default value: 1 minute.</strong></td></tr></tbody></table>

**Example downlink, \[Hex]:** 0802 - Тhe flood event send time is set to 2 minutes.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="137.66666666666666">Byte index</th><th width="225">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>09 – The command code.</td><td>09 – The command code.</td></tr><tr><td>1</td><td></td><td>XX –  Flood event send time in minutes.  </td></tr></tbody></table>

**Example command sent from server, \[Hex]:** 09;

**Example command response, \[Hex]:** 0902 – The flood event send time is 2 minutes.
{% endtab %}
{% endtabs %}

## Flood event uplink messages type

When a flood occurs, you can choose whether the **immediate uplink** is confirmed or unconfirmed.

{% hint style="info" %}
For this functionality to work, the device's periodic uplink type MUST be unconfirmed.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
This command is used to set only the flood event uplink message type.

<table><thead><tr><th width="135">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>13 – The command code.</td></tr><tr><td>1</td><td><p>00 – The flood event uplink message type is unconfirmed;</p><p>01 – The flood event uplink message type is confirmed. <strong>Default</strong>.</p></td></tr></tbody></table>

**Example command, \[Hex]:** 1301 – The server sets the flood event uplink message type to confirmed.
{% endtab %}

{% tab title="GET" %}
This command is used to get only the flood event uplink message type. Server sends the command code and the response is sent from the device together with the next keep-alive command. The keep-alive in the example is omitted for clarity.

<table><thead><tr><th width="123">Byte index</th><th width="157">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td>0</td><td>14 – The command code.</td><td>14 – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – The flood event uplink message type is unconfirmed;</p><p>01 – The flood event uplink message type is confirmed. </p></td></tr></tbody></table>

**Example command sent from server, \[Hex]:** 14;

**Example command response, \[Hex]:** 1401 - The flood event uplink message type is confirmed.&#x20;
{% endtab %}
{% endtabs %}

## Acoustic and LED alarm duration

When there's a flood detected, the Flood Sensor will sound an acoustic and visual alarm, so it can notify the tenants.

If the Alarm time value is set to 0, then the alarm sounds non-stop during the flooding event.&#x20;

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="142">Byte index</th><th>Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>04 - Set flood alarm time.</td></tr><tr><td>1</td><td>XX - Alarm time value. Resolution is 10sec. <strong>Default value is 0</strong></td></tr></tbody></table>

**Example downlink, \[Hex]:** 0402 - Тhe alarm duration is set to 20sec.
{% endtab %}

{% tab title="GET" %}
{% hint style="info" %}
This command is available for firmware version 1.5 or later.
{% endhint %}

<table data-header-hidden><thead><tr><th width="137.66666666666666">Byte index</th><th width="225">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>06 – The command code.</td><td>06 – The command code.</td></tr><tr><td>1</td><td></td><td>XX –  Alarm time value. Resolution is 10sec.</td></tr></tbody></table>

**Example command sent from server, \[Hex]:** 06;

**Example command response, \[Hex]:** 0606 – The alarm duration is 60 sounds.
{% endtab %}
{% endtabs %}
