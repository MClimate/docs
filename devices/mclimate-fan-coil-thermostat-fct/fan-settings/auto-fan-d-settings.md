# Auto Fan - Δ settings



The diagram below shows how the actual fan speed changes when the user has set the fan to auto.

<figure><img src="../../../.gitbook/assets/FCT - AUTO FAN operation" alt="" width="563"><figcaption></figcaption></figure>

Example:\
&#x20;\- **current operational mode: Heating**\
&#x20;\- Δt1 = 1°C\
&#x20;\- Δt2 = 1°C => 20% Δt2 = 0.2°C\
&#x20;\- Δt3 = 1°C => 20% Δt3 = 0.2°C\
&#x20;\- target temperature (w) = 23°C\
&#x20;\- threshold temperature 1 (th1) = w-Δt1 = 23 - 1 = 22°C\
&#x20;\- threshold temperature 2 (th2)  = th1-Δt2 = 22 - 1 = 21°C\
&#x20;\- threshold temperature 3 (th3)  = th2-Δt3 = 21 - 1 = 20°C\
&#x20;\- measured temperature = 22.2°C

1. When the **measured temperature** drops from 22.2 to 22°C (threshold temperature 1 - th1) or lower, the valve(s) fan goes into Low speed mode
2. The temperature keeps dropping to 21°C (threshold temperature 2 - th2), the fan goes into Medium speed mode
3. The temperature drops further to 20°C (threshold temperature 3 - th3), the fan goes into High speed mode
4. Temperature starts increasing till it reach 20.8°C (20%Δt3 threshold), where the fan speed is reduced to Medium.
5. Temperature increases further till it reach 21.8°C (20%Δt2 threshold), where the fan speed is further reduced to Low.
6. Temperature increases still, reaching 23°C (target temperature - w), the Fan turns off.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## Delta temperature 1 (ΔT1)

You can change the delta temperature (ΔT1) with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the delta temperature (ΔT1) with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>6A – The command code.</td></tr><tr><td>1</td><td>XX - ΔT1[°C] * 10. <strong>Default value:</strong> 0x0A (1,0°C)</td></tr></tbody></table>

**Example command**: 0x6A0F;

0x0F\[HEX] = 15\[DEC] => ΔT1 = 15 / 10 = 1,5°C.
{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature step. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>6B – Command code</td><td>6B – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - ΔT1[°C] * 10.</td></tr></tbody></table>

ΔT1\[°C] = XX / 10;

**Example command:** 0x6B;

**Example response:** 0x6B0F;

0x0F\[HEX] = 15\[DEC] => ΔT1 = 15 / 10 = 1,5°C.
{% endtab %}
{% endtabs %}

The allowed ΔT1 range step is 0,5...10°C (0,5°C resolution).

## Delta temperatures 2 (ΔT2) and 3 (ΔT3)&#x20;

You can change the delta temperatures (ΔT2) and (ΔT3) with the following command set.

{% tabs %}
{% tab title="SET" %}
#### You can set the delta temperatures (ΔT1) and (ΔT3) with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>6C – The command code.</td></tr><tr><td>1</td><td>XX - ΔT2[°C] * 10. <strong>Default value:</strong> 0x0A (1,0°C)</td></tr><tr><td>2</td><td>XX - ΔT3[°C] * 10. <strong>Default value:</strong> 0x0A (1,0°C)</td></tr></tbody></table>

**Example command**: 0x6C0F14;

Set the ΔT2 = 1,5°C - 1,5 \* 10 = 15\[DEC] => 0x0F\[HEX].

Set the ΔT3 = 2,0°C - 2 \* 10 = 20\[DEC] => 0x14\[HEX].
{% endtab %}

{% tab title="GET" %}
#### This command gets the target temperature step. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="199"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>6D – Command code</td><td>6D – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - ΔT2[°C] * 10.</td></tr><tr><td>2</td><td></td><td>XX - ΔT3[°C] * 10.</td></tr></tbody></table>

**Example command:** 0x6D;

**Example response:** 0x6D0F14;

ΔT\[°C] = XX / 10;

0x0F\[HEX] = 15\[DEC] => ΔT2 = 15 / 10 = 1,5°C.

0x14\[HEX] = 20\[DEC] => ΔT3 = 20 / 10 = 2,0°C.
{% endtab %}
{% endtabs %}

The allowed (ΔT2) and (ΔT3) range step is 0,5...10°C (0,5°C resolution).

