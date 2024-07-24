# Operational modes & temperature control algorithms

## Device operational modes

&#x20;The device has 4 operation modes:

* **Offline** – device is not connected to the network. This means that the device can’t join to the LoRaWAN network or doesn’t receive confirmation on the sent keep-alive commands. In this mode the device uses one of the internal temperature control algorithms to achieve target temperature;
* **Manual control** – device is connected to the network; internal temperature control algorithm is disabled. Motor position is determined by the server. **Default online mode for f.w. <= 3.4**
* **Automatic temperature control** - device is connected to the network; internal temperature control algorithm is enabled; Target temperature is determined by the server. **Default online mode for f.w. >=3.5**
* **Automatic temperature control with external temperature reading** – device is connected to the network; internal temperature control algorithms are enabled; internal temperature sensor is disabled; Target temperature and sensor reading is determined by the server.

{% hint style="danger" %}
In f.w. versions <= 4.0, you MUST use confirmed uplinks in case you want to use Online manual control or Automatic temperature control with external temperature reading**.**
{% endhint %}

The offline mode is entered automatically when the device has lost connection with the server. If the device later restores its server connection the mode is changed automatically to the previously selected online mode.&#x20;

{% tabs %}
{% tab title="SET" %}


<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0D – The command code.</td></tr><tr><td>1</td><td><p>00 – Online manual control mode. Default for firmware &#x3C;= 3.4</p><p>01 – Online automatic control mode. Default for firmware >= 3.5</p><p>02 – Online automatic control mode with external temperature reading.</p></td></tr></tbody></table>

Table 14

**Example command:** 0x0D01

With the example command, online automatic control mode is chosen.
{% endtab %}

{% tab title="GET" %}
This command is used to get Vicki online operational mode. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The sent command request and the received command response are described in Table 25. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="132.66666666666666">Byte index</th><th width="149">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>18 – Command code.</td><td>18 – The command code.</td></tr><tr><td>1</td><td></td><td><p>XX – Device online mode value:</p><p>00 – Online manual control mode;</p><p>01 – Online automatic control mode;</p><p>02 – Online automatic control mode with external temperature reading.</p></td></tr></tbody></table>

Table 25

**Example downlink sent by the server:** 0x18;

**Example command response:** 0x1801 – Vicki works in online automatic control mode.
{% endtab %}
{% endtabs %}

## Available temperature control algorithms

There are two available temperature control algorithms:

1. Equal directional control - available for f.w. < 4.2. (removed in 4.2)
2. Proportional control - available and **default** for f.w. versions >= 4.0 (removed in 4.3)
3. Proportional Integral control - available and **default** for f.w. versions >= 4.2 (only available algorithm in >= 4.3)

Once you have selected operational mode "Automatic temperature control", you have the option to set which temperature control algorithm you want to use.

Read more about [Equal directional control algorithm](algorithm-1-equal-directional-control.md).&#x20;

Read more about [Proportional control algorithm](algorithm-2-proportional-control.md).

Read more about [Proportional Integral control algorithm](algorithm-3-proportional-integral.md).

## Temperature control algorithm selection and retrieval

{% hint style="info" %}
This feature is available in firmware >= 4.0
{% endhint %}

{% hint style="warning" %}
The following commands are not supported in firmware >=4.3
{% endhint %}

{% tabs %}
{% tab title="SET" %}
<table data-header-hidden><thead><tr><th width="135"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>2C – The command code.</td></tr><tr><td>1</td><td><p>XX – Value to set according to the desired temperature control algorithm to be used by the device.</p><p>00: Use the "Proportional control" algorithm (not available in f.w.  >= 4.3)</p><p>01: Use the "Equal directional control" algorithm (not available in f.w. >= 4.2)<br>02: Use the "Proportional Integral control" algorithm.</p></td></tr></tbody></table>

Example command, \[Hex]: 2C02 – Set the device to use the "Proportional Integral control" algorithm.
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="131.66666666666666"></th><th width="179"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>2B – The command code.</td><td>2B – The command code.</td></tr><tr><td>1</td><td> </td><td><p>XX – Indicate the currently used algorithm for temperature control.</p><p>00: Proportional control algorithm used. <strong>Default for f.w. >= 4.0</strong></p><p>01: Equal directional control used. (deprecated in f.w. >=4.2)<br>02: For the device to use the "Proportional Integral control" algorithm. <strong>Default for f.w. >= 4.2</strong></p></td></tr></tbody></table>

Example command sent from the server, \[Hex]: 2B.

Example response, \[Hex]: 2B00 – Currently the Proportional control algorithm is in use.
{% endtab %}
{% endtabs %}

## Device primary operational mode

This command is used to change the device primary operational mode. Possible choices are **heating (default for the device)** and **cooling**. Switching from heating to cooling mode is required, when during the summer, cold water flow through the radiator. At the cold radiator water period end, switch to heating mode is required. Note that for both modes device functionalities open window detection and internal temperature control algorithm are available. The command data is described in Table 30. The keep-alive in the response is omitted for clarity.

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="137">Byte index</th><th>Hex Value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex Value - Meaning</strong></td></tr><tr><td>0</td><td>1E - The command code</td></tr><tr><td>1</td><td><p>00 – Vicki operates in heating mode (default for the device);</p><p>01 – Vicki operates in cooling mode.</p></td></tr></tbody></table>

Table 30
{% endtab %}

{% tab title="GET" %}
<table data-header-hidden><thead><tr><th width="140">Byte index</th><th width="138.66666666666666">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>1F – Command code.</td><td>1F – The command code.</td></tr><tr><td>1</td><td></td><td><p>00 – Device primary operational mode is heating;</p><p>01 – Device primary operational mode is cooling.</p></td></tr></tbody></table>

Table 31
{% endtab %}
{% endtabs %}



