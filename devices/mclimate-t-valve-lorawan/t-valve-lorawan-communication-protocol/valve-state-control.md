# Valve state control

## Set Open/Close state short cycle

This command sets up the valve so it alternates between its two states (open/close) for a certain time interval. The whole process is cyclical, meaning it can go indefinitely depending on how it is set up or the valve can move from one state to the other and remain in it.

{% hint style="info" %}
This command is mainly useful for Firmware Version ≤ 1.4 where the extended cycle command below is not available.
{% endhint %}

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

## Set Open/Close state extended cycle

This command is similar to the 01 command above, however it support extended timings. These timings are also reported in the device long keep-alive data. When some of the timings parameter is greater or equal to 255, it's reported as 255 in the long keep-alive data.

{% hint style="info" %}
We recommend using this command for Firmware Versions ≥1.5 as it has the same functionality as the 01 command however it offers extended timings.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0D – The command code.</td></tr><tr><td>1</td><td>XX – valve open time in minutes, bits 15:8</td></tr><tr><td>2</td><td>XX – valve open time in minutes, bits 7:0</td></tr><tr><td>3</td><td>XX - valve close time in minutes, bits 15:8</td></tr><tr><td>4</td><td>XX - valve close time in minutes, bits 7:0</td></tr></tbody></table>

<mark style="color:blue;">Value of 0 for the open/close time isn't accepted by the device.</mark>

**Example command:** 0x0D012C2760

012C\[HEX] = 300\[DEC] = 300 minutes = 5 hours -> the valve will be opened for 5 hours

2760\[HEX] = 10 080\[DEC] = 10 080 minutes = 7 days-> the valve will be closed for 7 days

So, the valve will open for 5 hours after seven days have elapsed, indefinitely
{% endtab %}

{% tab title="GET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="142">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0E – The command code.</td></tr><tr><td>1</td><td>XX – valve open time in minutes, bits 15:8</td></tr><tr><td>2</td><td>XX – valve open time in minutes, bits 7:0</td></tr><tr><td>3</td><td>XX - valve close time in minutes, bits 15:8</td></tr><tr><td>4</td><td>XX - valve close time in minutes, bits 7:0</td></tr></tbody></table>

**Example response:** 0x0E012C2760

012C\[HEX] = 300\[DEC] = 300 minutes = 5 hours -> the valve will be opened for 5 hours

2760\[HEX] = 10 080\[DEC] = 10 080 minutes = 7 days-> the valve will be closed for 7 days

So, the valve will open for 5 hours after seven days have elapsed, indefinitely
{% endtab %}
{% endtabs %}

## Single time limited valve state change

This command is used to change the valve state for a defined time and leave it at the opposite after.&#x20;

{% hint style="warning" %}
If you have used any of the commands above to cyclically open/close the valve, running this one will stop the cycle.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>14 – The command code.</td></tr><tr><td>1</td><td>XX – valve action: 0 - to close the valve for the defined time and open it after, 1 or bigger value - to open the valve for the defined time and close it after</td></tr><tr><td>2</td><td>XX – time duration in minutes, bits 15:8</td></tr><tr><td>3</td><td>XX - time duration in minutes, bits 7:0</td></tr></tbody></table>

**Example command:** 0x1401000A

01\[HEX] = 1\[DEC] opens the valve for 000A\[HEX] = 10\[DEC] =  10 minutes and leaves it closed after

**Example command:** 0x14000258

00\[HEX] = 0\[DEC] closes the valve for 0258\[HEX] = 600\[DEC] =  600 minutes = 6 hours and leaves it open after
{% endtab %}
{% endtabs %}

## General valve state control

Server send that command to simply open or close the valve forever.

{% hint style="warning" %}
If you have used any of the commands above to cyclically open/close the valve, running this one will stop the cycle.
{% endhint %}

{% tabs %}
{% tab title="SET" %}
The command explanation is in the table below.

<table data-header-hidden><thead><tr><th width="137">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>0C – The command code.</td></tr><tr><td>1</td><td>XX – the valve state to change to, 00[HEX] - close the valve, 01[HEX] open the valve</td></tr></tbody></table>

<mark style="color:blue;">Any value for the command parameter greater than 01\[HEX] opens the valve.</mark>

**Example command:** 0x0C00 -> Close the valve

**Example command:** 0x0C01 -> Open the valve
{% endtab %}
{% endtabs %}
