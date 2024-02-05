# Firmware Upgrade Over The Air (FUOTA)

Firmware Upgrade Over The Air (FUOTA) is a crucial process for the remote management of Internet of Things (IoT) devices. It enables the wireless update of firmwarе on devices that are part of an IoT network, making it possible for manufacturers and service providers to deploy firmware updates without needing physical access to the devices.

{% hint style="info" %}
We've first released FUOTA in Q2 2022. We have since updated a large number of our devices to the latest available firmware.&#x20;

Some facts about FUOTA:

* It DOES NOT impact battery life of the device significantly.
* If a device's FUOTA session fails, the device will not freeze, but it will continue working as normally with the previous firmware image.
{% endhint %}

### FUOTA and LoRaWAN

In the context of LoRaWAN, which is a low-power wide-area network protocol designed for IoT devices, FUOTA is particularly valuable because many of these devices are deployed in locations that are difficult or costly to reach. FUOTA ensures that devices operating on any public or private LoRaWAN network can receive updates efficiently without compromising their battery life or duty-cycle, which is critical for long-term deployments.

#### Benefits for Smart Buildings

1. **Continuous Improvement:** Firmware enhancements can be rolled out to optimize device performance and add new features.
2. **Reduced Costs:** Automatic updates eliminate the need for manual servicing, reducing maintenance costs.
3. **Compliance:** Ensures devices remain compliant with evolving regulations and standards.

Overall, FUOTA is an essential component for maintaining and improving a network of IoT devices critical to the smart building ecosystem.&#x20;

## What's the difference between LoRaWAN FUOTA and NFC/Wi-Fi/Bluetooth/Serial FUOTA?

While LoRaWAN FUOTA allows over-the-air updates in LoRaWAN networks, technologies such as NFC (Near Field Communication), Bluetooth and Serial firmware upgrade requires close physical proximity. NFC and Bluetooth updates are initiated by bringing an NFC-enabled device close to the IoT device, making the process suitable for smaller-scale or individual updates.  Serial update means physically interfacing the device's circuit board with a connector and a programmer & laptop.&#x20;

However, LoRaWAN FUOTA provides a much more scalable solution for IoT deployments, allowing the update of countless devices across multiple sites without the need for physical interaction. This brings significant savings in terms of time and logistic costs, plus it minimizes downtime.&#x20;

### **Initiating a FUOTA session**

{% hint style="info" %}
As of now, the way to initiate FUOTA is to connect your LNS to our Cloud and email us (lorawan-support@mclimate.eu) a list of Serial numbers of devices you wish to update.

Instructions on how to connect your LNS to our Cloud are to be found in the bar on the left, in section Integrations.
{% endhint %}

### What if my MClimate devices do not support FUOTA?

If you have a sizeable deployment, please get in touch with us at lorawan-support@mclimate.eu to discuss options for an on-site Serial update to the latest firmware, which will also add FUOTA for the future.
