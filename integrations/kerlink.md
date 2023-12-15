# Kerlink

## **Connecting Kerlink MyLNS/WMC to MClimate’s LoRaWAN broker**

### **1. O**nce you have created a Cluster, click on Push Configurations

![](<../.gitbook/assets/Screenshot 2022-02-01 at 12.09.31.png>)

### **2. Create New push configuration**

* **Type - HTTP**
* **Message detail level - Network**

![](<../.gitbook/assets/Screenshot 2022-02-01 at 11.55.27.png>)

### **3. Fill the fields**&#x20;

* Url **- https://lorawan-broker.mclimate.eu**
* Data up route&#x20;
  * **/up-mylns** - for http://mylns.wanesy.com/
  * **/up-wmc** - for https://wmc-poc.wanesy.com

![](<../.gitbook/assets/Screenshot 2023-02-21 at 19.09.31.png>)

### **4.** Go to [https://developers.mclimate.eu ](https://developers.mclimate.eu)and sign in with your MClimate Account.&#x20;

### 5. Go to[ ](https://developers.mclimate.eu/lorawan-token)[https://developers.mclimate.eu/kerlink-token](https://developers.mclimate.eu/kerlink-token) to generate new token

![](<../.gitbook/assets/Screenshot 2022-02-01 at 11.59.46.png>)

### **6. Copy username**

![](<../.gitbook/assets/Screenshot 2022-02-01 at 12.01.59.png>)

### **7.** Add custom headers

* ### header key - 'username', and value - {generated username}
* ### header key - 'm-token', and value - **copied M Token from** [**MClimate Enterprise->Integrations**](https://enterprise.mclimate.eu/integrations)

![](<../.gitbook/assets/Screenshot 2023-02-21 at 19.10.57.png>)

### **8. Go to 'Users' and create new user**&#x20;

This step is required in order to be able to send commands to the devices

* Username - shoud be the one from developers portal
* Email - Please use a valid email, you will be required to confirm it in order to validate the user
* Role - User
* Password - Should be the password copied from the developers portal
* Activation - Enable&#x20;

![](<../.gitbook/assets/Screenshot 2022-02-01 at 12.03.33.png>)

### **9.** Check your email and click on the link in order to confirm your email

### **10. Link the cluster with push configuration**

Payload Type - shoud be Hexadecimal

![](<../.gitbook/assets/Screenshot 2022-02-01 at 12.27.45.png>)
