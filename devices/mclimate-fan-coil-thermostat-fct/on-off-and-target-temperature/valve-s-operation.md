# Valve(s) operation

Regardless of the application (wiring diagram) choice, the valve(s) are operated in the following manner.&#x20;

The corresponding valve is activated together with the fan as the measured temperature crosses the _**Δt1**_ threshold in relation with the target temperature _**w**_. As the temperature in the room reaches the target temperature, the valve(s) and the fan are deactivated.

<figure><img src="../../../.gitbook/assets/FCT - Valves operation" alt=""><figcaption></figcaption></figure>

Example:\
&#x20;\- **current operational mode: Heating**\
&#x20;\- Δt1 = 1°C\
&#x20;\- target temperature (w) = 23°C\
&#x20;\- threshold temperature = w-Δt1 = 23 - 1 = 22°C)\
&#x20;\- measured temperature = 22.2°C

1. When the **measured temperature** drops from 22.2 to 22°C (threshold temperature) or lower, the valve(s) and fan are activates.
2. They stay active until the **measured temperature** is equal or greater to the **target temperature (w)**.
3. Once the target **temperature (w)** has been reached the valve(s) and fan deactivate.
4. When the temperature drops to 22°C again the the valve(s) and fan activate again, etc.

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Information how to change Δt1 is to be found [here](../fan-settings/auto-fan-d-settings.md#delta-temperature-dt1).
