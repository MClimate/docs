# Buzzer control

This command controls the Buzzer notifier. You can adjust the timing, frequency of the signal it emits, etc.

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>03 – The command code</td></tr><tr><td>1</td><td><p><em>XX – Buzzer volume and frequency</em><br>XX[7:4] - Buzzer volume:<br>0x0 - Buzzer volume set to minimum<br>...</p><p>0xE - Buzzer volume set to maximum 0xF - Buzzer is off<br><br><em>XX[3:0] - Buzzer frequency increments</em> of 0.5kHz<br>0x0 - Buzzer frequency 1kHz<br>0x1  - Buzzer frequency 1.5kHz<br>...<br>0xA - Buzzer frequency 6kHz<br>0xB to 0xF - Reserved</p></td></tr><tr><td>2</td><td>XX –  Buzzer active time in seconds (1 second resolution)<br>Time the buzzer to be active. Resolution – 1s. If zero, the buzzer will stay active until buzzer command with volume 0xF is received (buzzer turn-off) or the verify button is pressed. During this time the buzzer continuously alternate loud and silent states.</td></tr><tr><td>3</td><td>XX - On time for the buzz loud-silent period. Resolution – 10ms</td></tr><tr><td>4</td><td>XX - Off time for the buzz loud-silent period. Resolution – 10ms.</td></tr></tbody></table>

**Example command:** 0x03EA050A0A

EA\[HEX]:\
\[7:4]=0xE - Buzzer volume set to maximum\
\[3:0]=0xA - Buzzer frequency 6kHz

05\[HEX] = 05\[DEC] -> Buzzer active for 5 seconds

0A\[HEX] = 10\[DEC] -> Buzzer on time 10x10ms=100ms=0.1s

0A\[HEX] = 10\[DEC] -> Buzzer off time 10x10ms=100ms=0.1s
{% endtab %}
{% endtabs %}
