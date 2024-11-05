# Milesight

## **Connecting Milesight to MClimate’s LoRaWAN broker**

### **1.** Go to [https://enterprise.mclimate.eu/integrations](https://enterprise.mclimate.eu/integrations) and create your m-token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.58.06 (1).png" alt=""><figcaption></figcaption></figure>

Copy the token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.05.53.png" alt=""><figcaption></figcaption></figure>

### **2. Go to Network Server-> Applications->{your\_application}->Add new Data transmission with type HTTP**

<figure><img src="../.gitbook/assets/Milesight 0 (1).png" alt=""><figcaption></figcaption></figure>

### **3. Add headers and URL**

{% hint style="warning" %}
Depending on your device firmware the fields values in this section are different, make sure you follow the instructions that match your firmware version. You can see it in the Status page.
{% endhint %}

<figure><img src="../.gitbook/assets/image (1) (4).png" alt=""><figcaption><p>Milesgiht Gateway Firmware version</p></figcaption></figure>

#### Firmware version  ≤ 60.0.0.42-r4 / 56.0.0.3-r1

* **Type - HTTP**
* **m-token:** your token from Enterprise _(Step 1)_
* **username:** apiuser _(this is not an example it is static for all gateways)_
* **password:** password _(this is not an example it is static for all gateways)_
* **url:** the public IP address of the gateway _**(ex: 212.39.89.221)**_

{% hint style="warning" %}
Make sure that the IP is exposed and accessible from outside of your LAN. We need it for sending downlinks, if you are behind a NAT check your router for the public IP (the local one would not work).
{% endhint %}

A correctly filled out example is shown in the image below.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>HTTP Header fields</p></figcaption></figure>

#### Firmware version ≥ 60.0.0.42-r5 / 56.0.0.4

With these newer Firmware devices you would need an AES-128 bit encrypted password. Using the link below you can easily generate one:

{% embed url="https://anycript.com/crypto" %}
AES encryption tool
{% endembed %}

Fill in the parameters from the table below:

| Parameter           | Value                                                               |
| ------------------- | ------------------------------------------------------------------- |
| Encryption text     | <mark style="color:blue;">THE LOGIN PASSWORD FOR THE GATEWAY</mark> |
| Secret Key          | 1111111111111111 (static value)                                     |
| Encryption Key Size | 128 Bits                                                            |
| Encryption Mode     | CBC                                                                 |
| IV (optional)       | 2222222222222222 (static value)                                     |
| Output format       | Base64                                                              |

A correctly filled out form would look as the one in the image below. Press the Encrypt button and you will be given a string to copy from the Encrypted Text field.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>AES-128 bit encrypted password in Base64 form</p></figcaption></figure>

* **Type - HTTP**
* **m-token:** your token from Enterprise _(Step 1)_
* **username:** your gateway login username
* **password:** your gateway login password that we encrypted in the previous step
* **url:** the public IP address of the gateway _**(ex: 212.39.89.221)**_

{% hint style="warning" %}
Make sure that the IP is exposed and accessible from outside of your LAN. We need it for sending downlinks, if you are behind a NAT check your router for the public IP (the local one would not work).
{% endhint %}

A correctly filled out example is shown in the image below.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>HTTP Header fields</p></figcaption></figure>

### **4.** Add URL

The uplink data URL should be:

[https://lorawan-broker.mclimate.eu/milesight](https://lorawan-broker.mclimate.eu/milesight)&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>MClimate URL</p></figcaption></figure>

### **5.** Done
