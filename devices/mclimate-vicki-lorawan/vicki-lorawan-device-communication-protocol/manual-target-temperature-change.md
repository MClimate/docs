# Manual target temperature change

{% hint style="info" %}
Command is available only for firmware >= 3.5
{% endhint %}

The command below is used to indicate the application server that the user has changed the target temperature manually - by hand. The command is sent together with the keepalive of the device.

<table data-header-hidden><thead><tr><th width="145.22132253711203"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>28 – The command code.</td></tr><tr><td>1</td><td>XX – New value of the target temperature, in Celsius degrees.</td></tr></tbody></table>
