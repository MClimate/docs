# ThingPark Enterprise

## **Connecting ThingPark to MClimate’s LoRaWAN broker**

### **1. Create a new application server**

![](../.gitbook/assets/mw1920\_t1.png)

### **2. Content-type should be JSON untyped**

![](../.gitbook/assets/mw1920\_t2.png)

### **3. Add destination**

**Destination of MClimate’s LoRaWAN broker for ThingPark is: https://lorawan-broker.mclimate.eu/thingpark**

![](../.gitbook/assets/mw1920\_t3.png)

### **4. Securing the tunnel**

* **Go to** [**https://developers.mclimate.eu/lorawan-token**](https://developers.mclimate.eu/lorawan-token) **and Sign in with your MClimate account.**
* **Enter the Application server, AS\_ID, and click Create.**

![](../.gitbook/assets/mw1920\_t4.png)

* **Copy the token**

![](../.gitbook/assets/mw1920\_t6.png)

* **Active Uplink/Downlink security in your application server**
  * **Enter the AS ID - should be the same as that in the developers portal.**
  * **Paste the Token in the authentication key field.**
  * **Leave timestamp deviation empty.**

![](../.gitbook/assets/mw1920\_t7.png)

### **5.** Go to [https://enterprise.mclimate.eu/integrations](https://enterprise.mclimate.eu/integrations) and create your m-token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.05.40.png" alt=""><figcaption></figcaption></figure>

Copy the token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.05.53.png" alt=""><figcaption></figcaption></figure>

### 6. Create custom HTTP header with key with name “m-token” and for value paste the token from the enterprise.

### **7. Create new AS routing profile**&#x20;

![](../.gitbook/assets/mw1920\_t8.png)

### **8. Add Destination**&#x20;

![](../.gitbook/assets/mw1920\_t9.png)

### **9. In Device settings -> Choose the routing profile**

![](../.gitbook/assets/mw1920\_t10.png)

### **10. Done**
