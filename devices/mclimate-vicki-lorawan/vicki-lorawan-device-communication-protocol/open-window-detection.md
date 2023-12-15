# Open window detection

{% hint style="info" %}
The open window detection function works by looking for a sudden drop in temperature.

The detection algorithm takes readings every 1 minute, if the temperature dropped more than the threshold value, the valve is closed.

Therefore, it's not 100% reliable and can be affected by outdoor temperature, position of the device on the radiator, position of the radiator on the room and more factors.
{% endhint %}

## Open window commands with delta t 0.1 accuracy

{% hint style="warning" %}
These commands are only available for f.w. >= 4.2

For f.w. < 4.2, please use the command with accuracy 1.0 (described further below)
{% endhint %}

{% tabs %}
{% tab title="SET" %}
### Set open window detection parameters (0.1 accuracy)

To detect open window, the difference between the currently and previously measured temperatures must be equal or greater than specified temperature difference. New temperature value is got each minute.

<table data-header-hidden><thead><tr><th width="136.33333333333331">Byte index</th><th width="94">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>45 – The command will set Vicki open window detection parameters.</td></tr><tr><td>1</td><td>7:1</td><td>Reserved.</td></tr><tr><td>1</td><td>0</td><td><p>1 – Enables the open window detection functionality. </p><p>0 – Disable <strong>(Default).</strong></p></td></tr><tr><td>2</td><td>-</td><td>XX – Duration for the valve to stay closed after open window detection. Resolution – 5 minutes. Default is 10 minutes.</td></tr><tr><td>3</td><td>-</td><td>XX – Temperature difference to detect open window detection (In Celsius degrees), pre-multiplied by 10. <strong>Default is 1.0 Celsius.</strong></td></tr></tbody></table>

**Example downlink:** 0x4501060D – Enable open window detection; set the duration for the valve to be closed to 30min; set the temperature delta to 1.3°C.
{% endtab %}

{% tab title="GET" %}
### Get open window detection parameters (0.1 accuracy)

&#x20;This command is used to get Vicki open window detection parameters. Server sends the command code and the response is sent from Vicki together with the next keep-alive command.&#x20;

<table data-header-hidden><thead><tr><th width="97">Byte index</th><th width="134">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>46 – Command code.</td><td>46 – The command code.</td></tr><tr><td>1</td><td></td><td>Bits [7:1] - Reserved</td></tr><tr><td>1</td><td></td><td><p>Bit 8: Open window detection enable/disable bit</p><ul><li>1: Open window functionality is enabled;</li><li>0: Open window functionality is disabled.</li></ul></td></tr><tr><td>2</td><td></td><td>XX – duration for the valve to be at the desired position, after open window detection. Resolution – 5 minutes. Default value is 2, meaning 10 minutes.</td></tr><tr><td>3</td><td></td><td>XX - Temperature delta with resolution 0.1 Celsius degrees. Value is premultiplied by 10.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x46;

**Example command response:** 0x4601020F - Enable the open-window detection, duration is 10 minutes, delta is 0x0F = 15/10 = 1.5 degrees Celsius
{% endtab %}
{% endtabs %}

## Open window commands with delta t 1.0 accuracy

{% tabs %}
{% tab title="SET" %}
### Set open window detection parameters (1.0 accuracy)

&#x20;To detect open window, the difference between the currently and previously measured temperatures must be equal or greater than specified temperature difference. New temperature value is got each minute. In Table 9 is described the data which the server sends to Vicki to set the open window detection parameters.

{% hint style="warning" %}
In firmware versions >= 3.5, Vicki is fully closing the valve, regardless of the motorPosition defined in bytes 3 and 4 below.
{% endhint %}

<table data-header-hidden><thead><tr><th width="136.33333333333331">Byte index</th><th width="94">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>-</td><td>06 – The command will set Vicki open window detection parameters.</td></tr><tr><td>1</td><td>7:1</td><td>Reserved.</td></tr><tr><td>1</td><td>0</td><td>1 – Enables the open window detection functionality. 0 – disable it (Default).</td></tr><tr><td>2</td><td>-</td><td>XX – Duration for the valve to stay closed after open window detection. Resolution – 5 minutes. Default is 10 minutes.</td></tr><tr><td>3</td><td>-</td><td>XX – motor position to be set when open window detected, bits 7:0.</td></tr><tr><td>4</td><td>7:4</td><td>X – motor position to be set when open window detected, bits 11:8.</td></tr><tr><td>4</td><td>3:0</td><td>X – temperature difference to detect open window detection (In Celsius degrees). Default is 2 Celsius.</td></tr></tbody></table>

Table 9

**Example command 1:** 0x0601041C23 – Enable open window detection; set the duration for the valve to be closed to 20min; set the motor position to 540 steps; set the temperature delta to 3°C.

**Example command 2:** 0x0600041C23 – Disable open window detection.
{% endtab %}

{% tab title="GET" %}
### Get open window detection parameters (1.0 accuracy)

&#x20;This command is used to get Vicki open window detection parameters. Server sends the command code and the response is sent from Vicki together with the next keep-alive command. The sent command request and the received command response are described in Table 20. The keep-alive in the response is omitted for clarity.

<table data-header-hidden><thead><tr><th width="97">Byte index</th><th width="77">Bit index</th><th width="134">Sent request</th><th>Received response</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>-</td><td>13 – Command code.</td><td>13 – The command code.</td></tr><tr><td>1</td><td>7:1</td><td></td><td>Reserved;</td></tr><tr><td>1</td><td>0</td><td></td><td><p>Open window detection enable/disable bit:</p><ul><li>1: Open window functionality is enabled;</li><li>0: Open window functionality is disabled.</li></ul></td></tr><tr><td>2</td><td>-</td><td></td><td>XX – duration for the valve to be at the desired position, after open window detection. Resolution – 5 minutes.</td></tr><tr><td>3</td><td>-</td><td></td><td>XX – motor position to set when open window detected, bits 7:0.</td></tr><tr><td>4</td><td>7:4</td><td></td><td>X – motor position to set when open window detected, bits 11:8.</td></tr><tr><td>4</td><td>3:0</td><td></td><td>X – temperature difference to detect open window detection (In Celsius degrees).</td></tr></tbody></table>

Table 20

**Example command sent from server:** 0x13;

**Example command response 1:** 0x130102F412 – Open window detection functionality is enabled. When open window is detected, the motor will stay for 10 minutes on the specified position. Desired motor position is 500 steps. Open window will be detected when the temperature difference between the previously and currently measured temperatures become 2°C or greater.

**Example command response 2:** 0x130002F412 – Open window detection functionality is disabled.
{% endtab %}
{% endtabs %}



