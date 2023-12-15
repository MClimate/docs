# Akenza

## **Connecting Akenza to MClimate’s LoRaWAN broker**

### **1. Create API key**

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 13.47.29.png" alt=""><figcaption></figcaption></figure>

### **2. Copy API Key**

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 13.47.42.png" alt="" width="563"><figcaption></figcaption></figure>

### 3.Go to workspaces -> your workspace -> Data flows -> Create data flow -> Connect a device over HTTP

<figure><img src="../.gitbook/assets/Screenshot 2023-05-25 at 17.34.59.png" alt=""><figcaption></figcaption></figure>

### **4. Create output connector -> Webhook**

* **Paste the API key in the Auth headers**
* **The URL shoud be:** [**https://lorawan-broker.mclimate.eu/akenza**](https://lorawan-broker.mclimate.eu/akenza)
* **Method shoud be POST**
* **Get the M-token from** [**https://enterprise.mclimate.eu/integrations**](https://enterprise.mclimate.eu/integrations)
* **Paste the M-token in headers with key "m-token"**
* **Type - HTTP**
* **HTTP Type - All**
* **URL - https://lorawan-broker.mclimate.eu/up-b-one?m-token={your m-token(step2)}**
* **Authentication type - token**
* **Token - Step 3**

<figure><img src="../.gitbook/assets/Screenshot 2023-05-25 at 17.39.16.png" alt=""><figcaption></figcaption></figure>

### **5. Add Device type -> Seach for Vicki**

<figure><img src="../.gitbook/assets/Screenshot 2023-05-25 at 17.39.53.png" alt=""><figcaption></figcaption></figure>

### **6. N**ame the Data flow and you're done&#x20;

