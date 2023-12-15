---
description: A collection of examples how to compose/decode messages.
---

# Appendix (examples)

### Command examples.

Example containing more than 1 command for sent/received server packet uses alternate colors for each command (and optional command data) for ease of understanding.

#### Command example 1

&#x20;This example shows sent and received server message. The sent message contains 2 commands for Vicki:

* Read software and hardware version (Command code 0x04);
* Set motor position to 300 steps and display digits/target temperature to 29 Celsius degrees (Command code 0x31).

&#x20;The next received server message will contain also 2 commands from Vicki:

* The response to command code 0x04;
* The standard periodically sent keep-alive command with its data.

Server sends, \[hex]: 0431012C1D.

Server receives, \[hex]: 042321011D5A78FA2C01F080.

#### Command example 2

&#x20;This example shows server packet which consists of 7 Vicki commands:

* Set keep-alive period (Command code 0x02) to 11 minutes;
* Set temperature ranges (Command code 0x08) to 15 and 26 Celsius degrees;
* Set device operational mode (Command code 0x0D) to online automatic control;
* Set target temperature (Command code 0x0E) to 24 Celsius degrees.
* Get keep-alive period (Command code 0x12);
* Get temperature ranges (Command code 0x15);
* Get device operational mode (Command code 0x18).

Server sends, \[hex]: 020B080F1A0D010E18121518.

With the next keep-alive the server will receive and the requested data from Vicki:

Server receives, \[hex]: 120B150F1A1801011863530000008000.
