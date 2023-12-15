# LED control command explanation

This command allows you to activate the green LED with certain settings. See table 11 for details.

<table><thead><tr><th width="150">Byte index</th><th width="650.233644859813">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>05 – The command code.</td></tr><tr><td>1</td><td><p>LED behaviour: </p><p>01 - Turn the LED ON; </p><p>02 - Blink fast (100ms on, 100ms off);</p><p>03 - Blink slow (100ms on, 1000ms off);</p><p>04 - Turn the LED OFF.</p></td></tr><tr><td>2</td><td><p>XX - Duration for the LED behaviour. </p><p>Duration, [seconds] = XX * 10. </p><p>If zero, do it until next LED related command is received or</p><p>the verify button is pressed.</p></td></tr></tbody></table>

_Table 11_&#x20;

**Example command, \[Hex]:** 050204

See table 12 for details.

<table><thead><tr><th width="150">Byte index</th><th width="675.4285714285713">Hex value – Meaning</th></tr></thead><tbody><tr><td>0</td><td>05 – The command code.</td></tr><tr><td>1</td><td>02 - Blink fast (100ms on, 100ms off).</td></tr><tr><td>2</td><td>04 - Duration = 4 * 10  = 40sec.</td></tr></tbody></table>

_Table 12_
