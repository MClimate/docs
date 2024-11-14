# Keep-alive

## Keep-alive explanation

The Keep-alive is a periodically sent message which contains the most important device data.

T-Valve has two types of keep-alive packets, depending on the payload length, a Short and a Long one.

<table><thead><tr><th width="158">Packet payload size [Bytes]</th><th>Description</th></tr></thead><tbody><tr><td><strong>Packet payload size [Bytes]</strong></td><td><strong>Description</strong></td></tr><tr><td>Short [2]</td><td>Sent over regular time periods (the period is set with command <a href="keep-alive-period.md">0x07</a> from the server). The packet contains the device temperature sensors data from the last measurement and the water valve state. Temperature measurement is done once per hour.</td></tr><tr><td>Long [5]</td><td>Full device data. Such a packet is send from the device on certain events or by server request with command 0x08 or once per day</td></tr></tbody></table>

## Short payload

<table data-header-hidden><thead><tr><th width="108">Byte index</th><th width="126.00000000000003">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>[7:0]</td><td>Temperature measured by sensor 1. This sensor measures the water temperature, thus only positive values are expected. The resolution is 0.5°C. The temperature is calculated by the expression:<br>T, [°C] = (Bits[7:0])/2</td></tr><tr><td>1</td><td>7</td><td>Valve state, the values are in BIN format:<br>0 - The valve is closed – water isn’t flowing<br>1 - The valve is open – water is flowing.</td></tr><tr><td>1</td><td>[6:0]</td><td>Temperature measured by sensor 2. This sensor measures the ambient temperature. The measurement range is (-10°C to 50°C) and the resolution is 0.5°C. The temperature is calculated by the expression:<br>T, [°C] = ((Bits[6:0])-20)/2<br><strong>Examples:</strong><br>T = (20 - 20) / 2 = 0°C<br>T = (120 - 20) / 2 = 50°C<br>T = (0 - 20) / 2 = -10°C<br>T = (75 - 20) / 2 = 27.5°C</td></tr></tbody></table>

**Example packet: 0x0044**

00\[HEX] = 0\[DEC] -> T, \[°C] = 0/2 = 0°C

The water temperature is 0°C

44\[HEX] = 01000100\[BIN] ->\
\[7] = 0 -> Valve is open\
\[6:0] = 01000100-> T, \[°C] = (68-20)/2 = 24°C

## Long Payload

<table data-header-hidden><thead><tr><th width="108">Byte index</th><th width="74.00000000000003">Bit index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Bit index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>[7:5]</td><td>Reason to send the packet, the values are in BIN format:<br>000 - Requested by server command 0x08 or one day elapsed<br>001 - Device test switches combination is pressed<br>010 - Flood detected by device sensor<br>011: - “Open” or “Close” push-button is pressed<br>100 - Fraud detected – box tamper switch or magnetic sensor</td></tr><tr><td>0</td><td>4</td><td>Reserved</td></tr><tr><td>0</td><td>3</td><td>Box tamper status, the values are in BIN format:<br>0 - No box tamper detected<br>1 - Box tamper detected</td></tr><tr><td>0</td><td>2</td><td>Flood detector wire status, the values are in BIN format:<br>0 - The wire is working<br>1 - Wire is not working</td></tr><tr><td>0</td><td>1</td><td>Flood detection status, the values are in BIN format:<br>0 - No flood detected<br>1 - Flood detected</td></tr><tr><td>0</td><td>0</td><td>Magnet detection status, the values are in BIN format:<br>0 - No magnet presence is detected<br>1 - Magnet presence is detected</td></tr><tr><td>1</td><td>7</td><td>Alarm validation indicator. This bit is set to 1 when the user presses the “Verify” button when leakage alarm is active. After, on any response from the application server that bit is cleared</td></tr><tr><td>1</td><td>6</td><td>Manual valve open indicator, the values are in BIN format:<br>0 - Manual opening of the is disabled<br>1 - Manual opening of the valve is enabled</td></tr><tr><td>1</td><td>5</td><td>Manual valve close indicator, the values are in BIN format:<br>0 - Manual closing of the is disabled<br>1 - Manual closing of the valve is enabled</td></tr><tr><td>1</td><td>[4:0]</td><td>Device software version</td></tr><tr><td>2</td><td>[7:0]</td><td>In reduced access mode controls the valve close time. The resolution is in minutes</td></tr><tr><td>3</td><td>[7:0]</td><td>In reduced access mode controls the valve open time. The resolution is in minutes</td></tr><tr><td>4</td><td>[7:0]</td><td>Battery voltage. It is calculated by the formula:<br>Battery voltage, [mV] = (Bits[7:0])*8 + 1600</td></tr></tbody></table>

**Example packet: 0х64620000A4**

64620000A4\[HEX] = 0110 0100 0110 0010 0000 0000 0000 0000 1010 0100\[BIN]

**Byte 0:**\
\[7:5] = 011 -> Reason for packet “Open” or “Close” push-button is pressed\
\[3] = 0 -> No box tamper detected\
\[2] = 1 -> Wire is not working\
\[1] = 0 -> No flood detected\
\[0] = 0 -> No magnet presence is detected

**Byte 1:**\
\[7] = 0 -> Alarm not verified\
\[6] = 1 -> Manual open enabled\
\[5] = 1 -> Manual close enabled\
\[4:0] = 00010 -> Firmware version 2

**Byte 2:**\
\[7:0] = 0000 0000 -> Close time 0 minutes

**Byte 3:**\
\[7:0] = 0000 0000 -> Open time 0 minutes

**Byte 4:**\
\[7:0] = 1010 0100 -> Battery voltage, \[mV] = 164\*8 + 1600 = 2912mV
