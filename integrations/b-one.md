# B-One

## **Connecting B-One to MClimate’s LoRaWAN broker**

### **1. Add Forwarding Rule**

![](<../.gitbook/assets/Screenshot 2023-03-30 at 20.18.24.png>)

* **Type - HTTP**
* **HTTP Type - All**
* **URL - https://lorawan-broker.mclimate.eu/up-b-one?m-token={your m-token(step2)}**
* **Authentication type - token**
* **Token - Step 3**

### **2.** Go to [https://enterprise.mclimate.eu/integrations](https://enterprise.mclimate.eu/integrations) and create your m-token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.58.06 (1).png" alt=""><figcaption></figcaption></figure>

**Copy the token.**

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.05.53.png" alt=""><figcaption></figcaption></figure>

**Paste it in the URL**&#x20;

### **3.** Go to [https://developers.mclimate.eu ](https://developers.mclimate.eu)and sign in with your MClimate Account.&#x20;

{% hint style="warning" %}
Due to security reasons, we advice you to create a separate account in your B.One tenant for MClimate.

You have to authenticate a B.One account with MClimate's system using B.One's username and password, so downlinks can reach work successfully and maintain the integrity of communication security.
{% endhint %}

**Go to** [**https://developers.mclimate.eu/b-one-token**](https://developers.mclimate.eu/b-one-token) **to generate new token**

![](<../.gitbook/assets/Screenshot 2023-03-30 at 20.25.35.png>)

**Copy the token**

![](<../.gitbook/assets/Screenshot 2023-03-30 at 20.25.47.png>)

### **4.** Done
