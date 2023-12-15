# Appendix (examples)

## **Command examples.**

Example containing more than 1 command for sent/received server packet uses alternate colors for each command (and surrounding command data) for ease of understanding.

### **Command example 1**

This example shows sent and received server message. The sent message contains single command for the end-node device – read software and hardware version (Command code 0x04). The next received server message will contain 2 commands from the device:

* The response to command code 0x04;
* The standard periodically sent keep-alive command with its data.

Server sends, \[hex]: 04.

Server receives, \[hex]: 04108001027549CD0180.

### **Command example 2**

This example shows sent and received server packet which consists of more commands. The sent packet consists of 8 end-node commands:

* Set keep-alive period (Command code 0x02) to 4 minutes;
* Set network join time (Command code 0x10) to 5 minutes (300s);
* Set uplink messages (Command code 0x11) type to unconfirmed;
* Disable LoRaWAN radio watch-dog (Command code 0x1C) for both confirmed and unconfirmed uplinks;
* Get keep-alive period (Command code 0x12);
* Get network join time (Command code 0x19);
* Get uplink messages type (Command code 0x1B);
* Get LoRaWAN radio watch-dog configurations (Command code 0x1D).

&#x20;The next received packet from the server contains the requested commands answers and a keep-alive command data. Note that the order of the received command responses isn’t equal to the order of the sent requests.

Server sends, \[hex]: 0204103C11001C000012191B1D.

Server receives, \[hex]: 12041B00193C1D000001027549CD0180.

### &#x20;
