# Algorithm 2 - Proportional control

{% hint style="info" %}
This algorithm is available for devices with firmware version >= 4.0
{% endhint %}

{% hint style="danger" %}
Devices with firmware version >=4.3 have this algorithm removed as Algorithm 3 - Proportional Integral control has been deemed superior due to delivering better results.
{% endhint %}

## **Algorithm logic**

This control algorithm is used by the device to achieve the desired target temperature. Each time the algorithm logic is executed, the motor position is adjusted, so the target temperature is reached. The following block diagram explains the requirements in order for the proportional algorithm logic to be executed.

![](<../../../../.gitbook/assets/image (23).png>)

The proportional algorithm logic calculates new motor position using the expression:

$$MP_{new} = MP_{old} - \cfrac{c*(T_{set} - T_{measured})*MR}{100}$$, where:

$$MP_{new}$$: New motor position in steps.

$$MP_{old}$$: Old motor position in steps.

$$c$$: Proportional algorithm coefficient.

$$T_{set}$$: Target temperature in Celsius degrees.

$$T_{measured}$$: Measured temperature in Celsius degrees.

$$MR$$: Motor range in steps.

Note that the algorithm check period and coefficient parameters can be configured by radio commands.

## **Proportional temperature control algorithm parameters**

{% tabs %}
{% tab title="SET" %}
<table><thead><tr><th width="115.05745554035565">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td>0</td><td>2A – The command code.</td></tr><tr><td>1</td><td>XX – Value for the proportional algorithm coefficient to be set. Maximum acceptable value is 20.</td></tr><tr><td>2</td><td>XX – Value of the proportional algorithm control period, in minutes.</td></tr></tbody></table>

Example command, \[Hex]: 2A040C – Set the proportional algorithm coefficient to 4 and the check period to 12 minutes.
{% endtab %}

{% tab title="GET" %}


<table><thead><tr><th width="135">Byte index</th><th width="157">Sent request</th><th>Response - Meaning</th></tr></thead><tbody><tr><td>0</td><td>29 – The command code.</td><td>29 – The command code.</td></tr><tr><td>1</td><td> </td><td>XX – Value of the proportional algorithm coefficient. Maximum acceptable value is 20. Default value is 3.</td></tr><tr><td>2</td><td> </td><td>XX – Value of the proportional algorithm control period, in minutes. Default value is 10 minutes.</td></tr></tbody></table>

Example command sent from the server, \[Hex]: 29.

Example response, \[Hex]: 29030F – Coefficient: 3, control period: 15 minutes.
{% endtab %}
{% endtabs %}



