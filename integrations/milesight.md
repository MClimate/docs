# Milesight

## **Connecting Milesight to MClimate’s LoRaWAN broker**

### **1.** Go to [https://enterprise.mclimate.eu/integrations](https://enterprise.mclimate.eu/integrations) and create your m-token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.58.06 (1).png" alt=""><figcaption></figcaption></figure>

**Copy the token.**

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.05.53.png" alt=""><figcaption></figcaption></figure>

### **2. Go to Network Server-> Applications->{your\_application}->Add new Data transmission with type HTTP**

<figure><img src="../.gitbook/assets/Milesight 0 (1).png" alt=""><figcaption></figcaption></figure>

### **3. Add headers and URL**

* **Type - HTTP**
* **m-token:** your token from Enterprise _(Step 1)_
* **username:** apiuser _(this is not an example it is static for all gateways)_
* **password:** password _(this is not an example it is static for all gateways)_
* **url:** the public IP address of the gateway _**(ex: 212.39.89.221)**_

{% hint style="info" %}
Make sure that the IP is exposed and accessible from the outside world. We need it for sending downlinks, if you are behind a NAT check your router for the public IP (the local one would not work).
{% endhint %}

### **4.** Add URL

### The uplink data URL should be:

### [https://lorawan-broker.mclimate.eu/milesight](https://lorawan-broker.mclimate.eu/milesight)&#x20;

<figure><img src="../.gitbook/assets/Mclimate 3.png" alt=""><figcaption></figcaption></figure>

### **5.** Done
