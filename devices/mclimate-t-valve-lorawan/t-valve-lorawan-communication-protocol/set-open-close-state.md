# Set Open/Close state

This command sets up the valve so it alternates between its two states (open/close) for a certain time interval. The whole process is cyclical, meaning it can go indefinitely depending on how it is set up or the valve can move from one state to the other and remain

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>01 – The command code.</td></tr><tr><td>1</td><td>XX – time the valve will be opened for in minutes</td></tr><tr><td>2</td><td>XX – time the valve will be closed for in minutes</td></tr></tbody></table>

**Example command:** 0x010203

02\[HEX] = 02\[DEC] -> the valve will be opened for 2 minutes

03\[HEX] = 03\[DEC] -> the valve will be closed for 3 minutes

At this point it will open again for 2 minutes, close for 3 after, etc.

**Example command:** 0x010200

02\[HEX] = 02\[DEC] -> the valve will be opened for 2 minutes

00\[HEX] = 00\[DEC] -> the valve will be closed for 0 minutes (never closed)

In this case the command will keep the valve permanently open  until another command instructs it to close.

**Example command:** 0x010003

00\[HEX] = 00\[DEC] -> the valve will be opened for 0 minutes (never opened)

03\[HEX] = 03\[DEC] -> the valve will be closed for 3 minutes

In this case the command will keep the valve permanently closed until another command instructs it to open.
{% endtab %}
{% endtabs %}
