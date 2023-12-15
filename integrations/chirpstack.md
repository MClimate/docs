# Chirpstack

## **Connecting Chirpstack V4 to MClimate’s LoRaWAN broker**

### **1. Create a new application**

![](<../.gitbook/assets/Screenshot 2023-02-19 at 14.29.14.png>)

### **2. Go to API Keys and create new key**

![](<../.gitbook/assets/Screenshot 2023-02-19 at 14.29.44.png>)

### **3. Copy Token**

![](<../.gitbook/assets/Screenshot 2023-02-19 at 14.30.05.png>)

### **4. Click on "add" in integrations tab in created application**

![](<../.gitbook/assets/Screenshot 2023-02-19 at 14.31.33.png>)

### **5. Add HTTP integration**

* Fill the fields&#x20;
  * Payload marshaler - **JSON**
  * Endpoint URL - **https://lorawan-broker.mclimate.eu/chirpstack**
  * Headers
    * header name - **m-token**, header value - **copied M Token from** [**MClimate Enterprise->Integrations**](https://enterprise.mclimate.eu/integrations)
    * header name - **token**, header value - **copied API Token**
    * header name - **url,** header value - **your** [**ChirpStack Application Server**](https://www.chirpstack.io/application-server/api/) **Url with exposed port 8090**\
      **( example: http://212.39.89.221:8090 )**

![](<../.gitbook/assets/123 (2).png>)

### **6. Done**

##

## **Connecting Chirpstack V3 to MClimate’s LoRaWAN broker**

### **1. Create a new application**

![](<../.gitbook/assets/Screenshot 2021-06-24 at 11.27.30.png>)

### **2. Go to API Keys and create new key**

![](<../.gitbook/assets/Screenshot 2021-06-24 at 11.37.47.png>)

### **3. Copy Token**

![](<../.gitbook/assets/Screenshot 2021-06-24 at 11.38.08.png>)

### **4. Click on "add" in integrations tab in created application**

![](<../.gitbook/assets/Screenshot 2021-06-24 at 11.28.03.png>)

### **5. Add HTTP integration**

Fill the fields&#x20;

* Payload marshaler - **JSON**
* Endpoint URL - **https://lorawan-broker.mclimate.eu/chirpstack**
* Headers
  * header name - **m-token**, header value - **copied M Token from** [**MClimate Enterprise->Integrations**](https://enterprise.mclimate.eu/integrations)
  * header name - **token**, header value - **copied API Token**
  * header name - **url,** header value - **your** [**ChirpStack Application Server**](https://www.chirpstack.io/application-server/api/) **Url with exposed port 8080**\
    **( example: http://212.39.89.221:8080 )**

![](<../.gitbook/assets/123 (1).png>)

### **5. Done**
