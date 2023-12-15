# Tektelic

## **Connecting Tektelic to MClimate’s LoRaWAN broker**

### **1. Create a new application server**

![](../.gitbook/assets/mw1920\_1.png)

### **2. Create new Custom Data Converter**

Encode function is generated automatically.

Decode function please copy from here: [**Tektelic MClimate Decoder**](https://mclimate.bit.ai/docs/cZCxvaR76MTb87M5)

![](../.gitbook/assets/mw1920\_Screenshot\_2021-05-12\_at\_16.55.47.png)

### **3. Go to Manage Integrations**

![](../.gitbook/assets/mw1920\_Screenshot\_2021-04-20\_at\_17.29.34.png)

### **4. Create new HTTP Integration**

* Fill the fields&#x20;
  * Type - should be **HTTP**
  * Data Converter - use the one you created - **MClimate Vicki**
  * Application address -  [lorawan-broker.mclimate.eu](https://lorawan-broker.mclimate.eu/)
  * port - **80**
  * Base path - **/tektelic**
* Copy token in the HTTP URL path.

![](<../.gitbook/assets/Screenshot 2023-02-20 at 14.23.51.png>)

* **Create MClimate token**
  * **Go to** [**https://developers.mclimate.eu/lorawan-token**](https://developers.mclimate.eu/lorawan-token) **and Sign in with your MClimate account.**
  * **Enter the Application server, AS\_ID - with token from HTTP URL path, and click Create.**

![](../.gitbook/assets/Screenshot%202021-08-12%20at%2014.13.19.png)

* **Copy the token**

![](../.gitbook/assets/Screenshot%202021-08-12%20at%2014.13.30.png)

* **Create Headers**
  * **1st header**
    * **Key - should be "mclimate\_token".**
    * **Value - Paste the token from developers portal.**
  * **2nd header**
    * **Key - should be "m-token".**
    * **Value - Paste the token from** [**MClimate Enterprise -> Integrations**](https://enterprise.mclimate.eu/integrations)

![](<../.gitbook/assets/Screenshot 2023-02-20 at 14.23.40.png>)

### **5. Move device to Application**

![](../.gitbook/assets/mw1920\_7.png)

### **6. Done**
