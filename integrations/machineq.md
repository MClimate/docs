# MachineQ

## **Connecting MachineQ central to MClimate’s LoRaWAN broker**

### **1. Go to Integration->**&#x41;pplication Management and click Add application

![](<../.gitbook/assets/Screenshot 2022-09-09 at 16.22.15.png>)

### **2. Copy Client ID and save it somewhere**

![](<../.gitbook/assets/Screenshot 2022-09-09 at 16.39.04.png>)

### **3. Copy Client secret**

<figure><img src="../.gitbook/assets/Screenshot 2022-09-09 at 16.22.38.png" alt=""><figcaption></figcaption></figure>

### **4. Get downlink token**

* **Go to** [**https://developers.mclimate.eu/lorawan-token**](https://developers.mclimate.eu/lorawan-token) **and Sign in with your MClimate account.**
* **Paste the Client Id** &#x20;
* **Paste the Client secret.**

![](<../.gitbook/assets/Screenshot 2022-09-09 at 16.23.11.png>)

* **Copy the token**

<figure><img src="../.gitbook/assets/Screenshot 2022-09-09 at 16.23.23 (1).png" alt=""><figcaption></figcaption></figure>

### 5. Go back to Integrations -> Output profiles and add output profile

<figure><img src="../.gitbook/assets/Screenshot 2022-09-09 at 16.20.40.png" alt=""><figcaption></figcaption></figure>

### 6. Add devices&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2022-09-09 at 16.20.54.png" alt=""><figcaption></figcaption></figure>

### 7. Add destination, select webook

<figure><img src="../.gitbook/assets/Screenshot 2022-09-09 at 16.21.06.png" alt=""><figcaption></figcaption></figure>

### 8. Enter the URL in the destination

* **The URL should be** [**https://lorawan-broker.seemelissa.com/up-machineq**](https://lorawan-broker.seemelissa.com/up-machineq)&#x20;
* **Output format - Extended**
* **Token type - downlink-token**
* **Token value - paste the token from the developers portal**
* **Click add**

![](<../.gitbook/assets/Screenshot 2022-09-09 at 16.24.51.png>)

### 9. Done :tada:
