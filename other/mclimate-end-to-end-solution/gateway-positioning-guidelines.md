# Gateway Positioning Guidelines

In order to have a well working LoRaWAN network, good signal/coverage is required, which largely depends on gateway positioning within the building and/or with reference to the devices to be serviced. Good gateway coverage is critical and it can make or break your installation.

There are two main things to consider when deploying a LoRaWAN Network:

* The material and shape of the building.
* The location of the sensors in the building.

## Getting started

There are a number of good practices that make life easier when trying to build a good LoRaWAN Network coverage:

1. Expect to need more gateways if the building is dense/has a lot of metal and few windows.
2. Avoid deploying close to elevator shafts, server rooms, in basements, etc. (dense metal inhibits coverage)
3. Deploy gateways in the middle of the space, if possible, 1 to 1.5m high at least. This will give you good coverage over the whole area.
4. Avoid putting sensors right next to the gateway (this sometimes can cause issues due to too strong a signal overloading the gateway front-end), place them at least 3-5 meters away from the gateway.
5. Make sure that the gateway antenna is properly connected and oriented (for most gateways this would be pointing up, check with the gateway manufacturer if need be).

<figure><img src="../../.gitbook/assets/2 (2).png" alt=""><figcaption><p>Example Gateway positioning in a building</p></figcaption></figure>

## Pre-deployment strategies

### The impact of building structure and device location

Different materials attenuate the signal differently and determine what the effective range of a network/gateway would be. Denser materials like concrete, stone, and metal heavily reduce signal coverage, where materials like glass, plastic, wood have little to no impact. Based on these the following points can be made:

* Avoid deploying the gateways near large metal objects or parts of the structure (for example the elevator shaft) that are made out of metal.
* Windows don’t impact coverage much, however some coatings that contain metallic particles could act as a metal screen so make sure to account for these.
* Concrete buildings tend to have wire armatures which limit range.

In short, the denser more metallic the structure is the smaller the coverage of a gateway would be. Use the following chart as reference and avoid positioning the gateways near materials that are lower on the scale:

<figure><img src="../../.gitbook/assets/3 (2).png" alt=""><figcaption><p>Attenuation in materials - Image : <a href="https://akenza.io/blog/howto-test-lora-coverage">Akenza</a></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/4 (2).png" alt=""><figcaption><p>Propagation through coated windors - Image : <a href="https://akenza.io/blog/howto-test-lora-coverage">Akenza</a></p></figcaption></figure>

## Post-deployment optimization

If you follow the aforementioned rules, you should have pretty good coverage already, however you might still need to position additional gateways or move existing ones. Once you have the initial deployment it is good to examine the signal quality of the end devices.&#x20;

As we mentioned, ideally you want to have transmission on SF7 (this is the best in relation to battery life and limiting of interference). If your devices are sending on SF8 to SF9 your coverage is still pretty good, but it could be improved a bit (in case you want to have longer battery life for example). The network would still be very stable. This being said, you need to also take a look at the signal levels, as mentioned RSSI under -90dBm and SNR below -5dB would be considered potentially insufficient for a good coverage and are an indicator for installing additional gateways.

<figure><img src="../../.gitbook/assets/1 (6).png" alt=""><figcaption><p>The effects of SF on transmission</p></figcaption></figure>

In Smart Buildings use-cases, SF11 and SF12 are considered suboptimal and substantially reduce battery life and network capacity. If your devices are operating under such conditions, it is advisable to install one or more gateways close to the area where the affected devices are.

The devices are configured to work dynamically, thus as soon as the coverage improves the Network server will instruct them to move to a lower SF, thus you will not only improve coverage, inhibit potential packet loss, but also reduce interference and improve end-device battery life.

Adhering to these rules you should be able to cover the entire building with a few well positioned gateways (ideally equidistantly between floors and somewhere in the middle in each floor) and perhaps later on add 1-2 more in case some nodes have poor signal quality.

{% hint style="info" %}
Overlapping areas of gateway are recommended for better coverage. There is no negative to installing more LoRaWAN Gateways as the way the network works the strongest signal is the one that is used (de-duplication at the LNS level). Do keep in mind that if you overlap coverage too much you might be overdoing it (you might be able to get aways with less gateways and minimize costs).
{% endhint %}
