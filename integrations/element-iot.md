# Element-IoT

## **Connecting Element-IoT to the MClimate LoRaWAN Broker**

### 1. In the Element-IoT Platform go to the Automation -> Streams section and create a new Stream

Provide a name, for example "MClimate"

Select the "Source type" from the drop down menu, it should be "**Devices in folder including children".** This will include all the devices in the folder.

Select the appropriate folder for your device set.

Save.

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Stream creation</p></figcaption></figure>

### 2. Generating the M-token and API key

In order for the integration to work properly an authentication method is required which utilized an M-tone (from the Enterprise platform) and an API key (from Element-IoT). we need to generate a set to later use for the Rule engine.

Go to [https://enterprise.mclimate.eu/integrations](https://enterprise.mclimate.eu/integrations)

Create a new token, give it a name and copy it from the next window. Make sure to keep it someplace safe, you won't be allowed to copy it over again, rather create a new one.

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption><p>M-token creation</p></figcaption></figure>

In Element-IoT go to Settings -> API Keys. Add a new API Key with the following configuration options and give it a name.

**Authentication method** - API Key

**Role** - Admin

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>API Key creation</p></figcaption></figure>

### 3. Next you need to create a "Rule" to associate to the Stream to properly route the data. Go to the Automation > Rules section and create a new one

Give it a name, for example "MClimate HTTP".

**Execute action** - immediately.

**Event source** - select the previously created stream "MClimate" for the Even stream and for the Even select "Packet added".

**Condition** - click on the field to manually type the condition for the filter and enter "true".

Leave the Execute once" option un-checked.

**Action** - select the "Send HTTP request" option from the drop-down menu.

**HTTP Method** - select "POST"

**URL** - past the MClimate broker url here: [https://lorawan-broker.mclimate.eu/element-iot](https://lorawan-broker.mclimate.eu/element-iot)

**HTTP Headers** - there are two custom headers here, the value of which would be specific for your integration. You need to enter the following text in the field:

_m-token:{your M-token created in Enterprise in point 2)_

_api-key:{your API Key created in Element-IoT in point 2)_

Refer to the image below for example values (yours will differ)

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption><p>HTTP Header creation</p></figcaption></figure>

Select all the check boxes available.

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>JSON options selection</p></figcaption></figure>

Save and you are done.
