# Orbiwise

## **Connecting Orbiwise to MClimate’s LoRaWAN broker**

### **1. Creating an Application**

Go to the Applications -> Manage Applications section and click Add Application.

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption><p>Application creation</p></figcaption></figure>

### **2. Fill the fields**

* **Account ID**&#x20;
* **Password and Passrod Confirmation - leave empty**
* **URL:** [**https://lorawan-broker.mclimate.eu**](https://lorawan-broker.mclimate.eu)
* **Path prefix: /up-orbiwise**
* **Authentication Methods: Basic**
* **Username and Password - the credentials you use for your Orbiwise account**
* **Data format - hex**
* **Store payload: On failure to push**
* **Subscriptions - only 'payloads\_ul' and 'payloads\_dl'**

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption><p>Application configuration</p></figcaption></figure>

### **3. Start Push**

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption><p>Start Push</p></figcaption></figure>

### **4. Assign the app to the devices**

Head to the Devices -> Manage Devices section.

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption><p>Manage Device</p></figcaption></figure>

Select the desired devices use the App Assignment action via the Bulk Action menu.

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption><p>Selecting devices</p></figcaption></figure>

Select your application and Add it.

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption><p>Adding the Application</p></figcaption></figure>

### 5. Done :tada:
