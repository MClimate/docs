# Loriot

## **Connecting Loriot to MClimate’s LoRaWAN broker**

### **1. O**nce you have created application, click on Access Tokens

![](<../.gitbook/assets/Screenshot 2022-01-19 at 18.58.24.png>)

### **2. Copy your access token**

![](<../.gitbook/assets/Screenshot 2022-01-19 at 18.53.14.png>)

### **3. Go to Output and add new output**

![](<../.gitbook/assets/Screenshot 2022-01-19 at 18.54.16.png>)

### **4. Click on HTTP Push and fill the fields**

* Target URL  - **https://lorawan-broker.mclimate.eu/loriot?m-token={get your M Token from** [**MClimate Enterprite->Integrations**](https://enterprise.mclimate.eu/integrations)**}**
* Authorization header value - **your access token**

![](<../.gitbook/assets/Screenshot 2023-02-20 at 17.49.55.png>)

### **5. Done**

![](<../.gitbook/assets/Screenshot 2022-01-19 at 18.55.59.png>)

