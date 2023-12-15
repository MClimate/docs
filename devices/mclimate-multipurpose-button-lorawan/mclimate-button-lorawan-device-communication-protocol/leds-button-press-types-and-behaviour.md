# LEDs, button press types and behaviour

There are three separate types of clicks supported by the button. After each click the button waits for 600ms to check if another click is coming. Once the click type has been determined, the device sends a confirmed uplink with the temperature data and the click type information.&#x20;

**Supported click types:**

1. Single click
2. Double click
3. Triple click

**LEDs indications:**

* The GREEN LED is activated while the button is pressed
* The side LEDs alternate when the LoRaWAN message is being sent
* The GREEN LED lights up when the event is sent and acknowledged by the gateway and LNS
* If the message has not been successfully acknowledged, the RED LED activates
* If a message is not allowed to be sent at the moment (due to RF duty-cycle restrictions), the RED light activates after you release the button.
* If the sensor is NOT connected to a network, then the SIDE and RED LEDs activate.

###
