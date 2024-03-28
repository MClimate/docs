# Firefly

## **Connecting Firefly to MClimate’s LoRaWAN broker**

### **1. Go to {your o**rganization}-> Settings-> API Keys, create new one and copy it&#x20;

![](<../.gitbook/assets/Screenshot 2022-11-09 at 13.54.08.png>)

### **2. Go to Sinks and click on create new sink**&#x20;

![](<../.gitbook/assets/Screenshot 2022-11-09 at 13.55.10.png>)

### **3. Get downlink token**

* **Go to** [**https://developers.mclimate.eu/lorawan-token**](https://developers.mclimate.eu/lorawan-token) **and Sign in with your MClimate account.**
* **Enter the name of the webhook**
* **Paste the API Key.**

![](<../.gitbook/assets/Screenshot 2022-11-09 at 14.17.17 (1).png>)

* **Copy the token**

![](<../.gitbook/assets/Screenshot 2022-11-09 at 13.55.27.png>)

### 4.Enter the URL in the Webhook

* **The URL should be** [**https://lorawan-broker.mclimate.eu/firefly?token=**](https://lorawan-broker.seemelissa.com/firefly?token=600f97b5abc986ab95a81029de29c5d7\&url=lora.national.iothub.no)**{developers\_portal\_token}** [**\&url= {optional url of your instance}**](https://lorawan-broker.seemelissa.com/firefly?token=600f97b5abc986ab95a81029de29c5d7\&url=lora.national.iothub.no)**\&m-token={your\_m-token}**
* **\*Default downlink URL is api.fireflyiot.com**
* **Content Type is application/json**
* **Triggers should be All Events**

![](<../.gitbook/assets/Screenshot 2022-11-09 at 13.57.03.png>)

### 5. Save new webhook

### 6. Done
