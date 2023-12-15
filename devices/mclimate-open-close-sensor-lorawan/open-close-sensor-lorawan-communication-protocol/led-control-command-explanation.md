# LED control command explanation

This command allows you to activate the LED with certain settings. See table 16 for details.

<table><thead><tr><th width="150">Byte index</th><th width="650.233644859813">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>05 – The command code.</td></tr><tr><td>1</td><td><p>LED behaviour: </p><p>01 - Turn the LED ON; </p><p>02 - Blink fast (10ms on, 200ms off);</p><p>03 - Blink slow (10ms on, 2000ms off);</p><p>04 - Turn the LED OFF.</p></td></tr><tr><td>2</td><td><p>XX - Duration for the LED behaviour. </p><p>Duration, [seconds] = XX * 10. </p><p>If zero, do it until next LED related command is received or</p><p>the verify button is pressed.</p></td></tr></tbody></table>

_Table 16_&#x20;

**Example command, \[Hex]:** 050204

See table 17 for details.

<table><thead><tr><th width="150">Byte index</th><th width="675.4285714285713">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>05 – The command code.</td></tr><tr><td>1</td><td>02 - Blink fast (10ms on, 200ms off).</td></tr><tr><td>2</td><td>04 - Duration = 4 * 10  = 40sec.</td></tr></tbody></table>

_Table 17_
