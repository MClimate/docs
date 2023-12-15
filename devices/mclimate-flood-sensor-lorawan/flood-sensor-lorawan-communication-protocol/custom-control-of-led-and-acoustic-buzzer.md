# Custom control of LED and Acoustic Buzzer

Since the device has Buzzer and LED, you can choose to activate them with a downlink regardless whether there's an flood event detected or not.

## Buzzer control command explanation

This command allows you to activate the buzzer with certain settings, such as setting the time duration, adjusting the volume and frequency. See table 4 for details.

<table><thead><tr><th width="150">Byte index</th><th width="150">Bit index</th><th width="450.2">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td>03  – The command will set the buzzer volume and frequency.</td></tr><tr><td>1</td><td>7:4</td><td><p>Buzzer volume, [hex]: </p><p>0: Buzzer volume set to minimum available; </p><p>1: … </p><p>2: … </p><p>3: … </p><p>4: … </p><p>5: … </p><p>6: … </p><p>7: … </p><p>8: … </p><p>9: … </p><p>A: … </p><p>B: … </p><p>C: … </p><p>D: … </p><p>E: Buzzer volume set to maximum available; </p><p>F: Buzzer is off.</p></td></tr><tr><td></td><td>3:0</td><td><p>Buzzer frequency, [hex]: </p><p>0: Buzzer frequency is 1kHz; </p><p>1: Buzzer frequency is 1.5kHz; </p><p>2: Buzzer frequency is 2kHz; </p><p>3: Buzzer frequency is 2.5kHz; </p><p>4: Buzzer frequency is 3kHz; </p><p>5: Buzzer frequency is 3.5kHz; </p><p>6: Buzzer frequency is 4kHz; </p><p>7: Buzzer frequency is 4.5kHz; </p><p>8: Buzzer frequency is 5kHz;</p><p>9: Buzzer frequency is 5.5kHz; </p><p>A: Buzzer frequency is 6kHz; </p><p>B: Reserved; </p><p>C: Reserved; </p><p>D: Reserved; </p><p>E: Reserved; </p><p>F: Reserved.</p></td></tr><tr><td>2</td><td>-</td><td>Time the buzzer to be active. Resolution – 1s. If zero, the buzzer will stay active until buzzer command with volume value ([hex]: F) is received (buzzer turn-off) or the button is pressed. During this time the buzzer continuously alternate loud and silent states.</td></tr><tr><td>3</td><td>-</td><td>On time from the buzz loud-silent period. Resolution – 10ms.</td></tr><tr><td>4</td><td>-</td><td>Off time from the buzz loud-silent period. Resolution – 10ms.</td></tr></tbody></table>

_Table 4._

**Example command, \[Hex]:** 03E50А3246&#x20;

See table 5 for details.

<table><thead><tr><th width="150">Byte index</th><th width="150">Bit index</th><th width="466.2">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>-</td><td>03  – The command will set the buzzer volume and frequency.</td></tr><tr><td>1</td><td>7:4</td><td>0E - Buzzer volume set to maximum available.</td></tr><tr><td></td><td>3:0</td><td>05 - Buzzer frequency is 3.5kHz.</td></tr><tr><td>2</td><td>-</td><td>0А - Time the buzzer to be active is 10 seconds.</td></tr><tr><td>3</td><td>-</td><td>32 - On time from the buzz loud-silent period is 500ms.</td></tr><tr><td>4</td><td>-</td><td>46 - Off time from the buzz loud-silent period is 700ms.</td></tr></tbody></table>

_Table 5._

## LED Control

This command allows you to activate the LED with certain settings. See table 6 for details.

<table><thead><tr><th width="150">Byte index</th><th width="644.7503337783711">Hex value - Meaning</th></tr></thead><tbody><tr><td>0</td><td>02 - The command code.</td></tr><tr><td>1</td><td>03 - LED responsible for Flood.</td></tr><tr><td>2</td><td><p>LED behavior:</p><p>01 - Turn the LED ON;</p><p>02 - Blink fast (10ms on, 200ms off);</p><p>03 - Blink slow (10ms on, 2000ms off);</p><p>04 - Turn the LED OFF.</p></td></tr><tr><td>3</td><td><p>XX - Duration for the LED behavior.</p><p>Duration, [seconds] = XX.</p><p>If zero, do it until next LED related command is received or</p><p>the verify button is pressed.</p></td></tr></tbody></table>

_Table 6._

**Example command, \[Hex]:** 02030204

See table 7 for details.

<table><thead><tr><th width="150">Byte index</th><th width="670.8240178856594">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>02 - The command code.</td></tr><tr><td>1</td><td>03 - LED responsible for Flood.</td></tr><tr><td>2</td><td>02 - Blink fast (10ms on, 200ms off).</td></tr><tr><td>3</td><td>04 - Duration = 4sec.</td></tr></tbody></table>

_Table 7._
