# Helium

## **Connecting Helium to MClimate’s LoRaWAN broker**

### **1. Create a new label**

![](<../.gitbook/assets/Screenshot 2021-10-19 at 14.41.22.png>)

### **2. Add this Label to a Device**

![](<../.gitbook/assets/Screenshot 2021-10-19 at 14.42.01.png>)

### **3. Add a custom HTTP integration**

![](<../.gitbook/assets/Screenshot 2021-10-19 at 14.42.33.png>)

### **4. Add Integration**

* Fill the fields&#x20;
  * **POST**
  * Endpoint URL - https://lorawan-broker.mclimate.eu/helium
  * HTTP Headers - [M-token (check step 5-6)](helium.md#5.-go-to-https-enterprise.mclimate.eu-integrations-and-create-your-m-token.)

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.59.01.png" alt=""><figcaption></figcaption></figure>

### 5. Go to [https://enterprise.mclimate.eu/integrations](https://enterprise.mclimate.eu/integrations) and create your m-token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.58.06 (1).png" alt=""><figcaption></figcaption></figure>

Copy the token.

<figure><img src="../.gitbook/assets/Screenshot 2023-01-27 at 17.05.53.png" alt=""><figcaption></figcaption></figure>

### 6. Create HTTP header with key with name “m-token” and for value paste the token from the enterprise.

### **7. Go to "Flows"**

* Drag & drop the label node
* Drag & drop the integration node
* Connect them

![](<../.gitbook/assets/Screenshot 2021-10-19 at 14.44.01.png>)
