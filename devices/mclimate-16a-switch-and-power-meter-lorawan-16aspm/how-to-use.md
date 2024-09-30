# 🛠️ How to use

## Commissioning

We recommend you register your device with your LNS provider of choice first and foremost. This will help speed the onboarding process.

* Open your LoRaWAN® Network provider access panel and add the device using the supplied Serial Number, DevEUI, AppEUI (JoinEUI) and AppKey.

<figure><img src="../../.gitbook/assets/image (54).png" alt="" width="368"><figcaption></figcaption></figure>

{% hint style="info" %}
You can get the DevEUI, AppEUI (JoinEUI) and AppKey information from the LoRaWAN credentials.csv file we sent you with the fulfillment confirmation. If you are missing this info contact us at [lorawan-support@mclimate.eu](mailto:lorawan-support@mclimate.eu) and we will sort out the issue.
{% endhint %}

* Continue the Installation with the instructions of your LoRaWAN® Network provider.

Your devices is registered with the LNS at this point and if properly wired and powered it should have no issue joining the LNS right away. Proceed to the next section in order to properly power it.

{% hint style="warning" %}
Remember that this is a LoRaWAN Class C device, some LNSs onboard devices as Class A by default (TTN/TTI for example). Make sure to adjust the settings so it is perceived as a Class C device.
{% endhint %}

## Wiring the device

It is very important you wire the device properly. Remember, this is a Wet Rely device which commutates line voltage/current, thus improper wiring can damage the MClimate device and/or the appliance it is connected to.

The diagram below should be used as guidance for wiring the device.

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

## LED status

| State                 | Meaning                                                                                                                                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2s ON, 1s OFF         | Device is powering up                                                                                                                                                                                    |
| 1s ON, 1s OFF         | Device is trying to join the LoRaWAN Network.                                                                                                                                                            |
| Solid ON              | Device has successfully joined the LoRaWAN network                                                                                                                                                       |
| 1/4s ON, 1/4s OFF     | Joining the LoRaWAN network has failed.                                                                                                                                                                  |
| 2s OFF, 2s ON, 2s OFF | Alarm activated - overcurrent, overpower, overheating or overvoltage protection activated. Once alarm is indicated, the device shows joined/not joined status for 5s and continues indicating the alarm. |

## Button actions

| State           | Meaning                                                                                                                                                                                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2 quick presses | <p>Switch relay state</p><ul><li>LED: 1s OFF, 1s ON, 1s OFF - relay closed</li><li>LED: 1/2s OFF, 1/2s ON, 1/2s OFF, 1/2s ON - relay opened</li></ul><p><em>After relay status indication, LED continues to show the joined/not joined status as described above.</em></p> |
| 10s press       | Restart the device, trigger new join-request, preserve the status of the relay                                                                                                                                                                                             |

## Device behavior in different scenarios

In order to better understand how the device behaves we have provided a series of short videos to illustrate different scenarios, based on its workings and how the LED behaves.

### Scenario 1 - successful network join procedure

The devices is powered on, it initiates the network join procedure, it joins the network successfully and enters normal operation mode.

{% embed url="https://youtu.be/BAK1tgwgI7s" fullWidth="false" %}
Scenario 1
{% endembed %}

### Scenario 2 - failed network join procedure

The devices is powered on, it initiates the network join procedure, however it does not manage to join on this attempt and remains in a disconnected state (indicated by the LED) until the next join-request.

{% embed url="https://youtu.be/F_NVXGPPA-A" %}
Scenario 2
{% endembed %}

## Scenario 3 - protection event trigger

The device is working in normal operation mode, a protection even is triggered (over current/voltage/temperature/power) and this is reflected in the LED status. After a time the device recovers (the condition that cause the protection to trigger is reverted to normal levels) and enters normal operation mode again.

{% embed url="https://youtu.be/bZuzgpNbpmE" %}
Scenario 3
{% endembed %}

## Scenario 4 - relay state change to closed

The device is working in normal operation mode, the button is pressed 2x in quick succession, the relay state changes from open to closed.

{% embed url="https://youtu.be/sxXxe2jyZJQ" %}
Scenario 4
{% endembed %}

## Scenario 5 - relay state change to open

The device is working in normal operation mode, the button is pressed 2x in quick succession, the relay state changes from closed to open.

{% embed url="https://youtu.be/QHFVYh46IuI" %}
Scenario 5
{% endembed %}

## Scenario 6 - device reset, initiate re-join procedure

The device is working in normal operation mode, the button is pressed for 10 seconds. The device is reset and it enters into a cycle depicted in Scenario 1.

{% embed url="https://youtu.be/UsTfBHUOsYg" %}
