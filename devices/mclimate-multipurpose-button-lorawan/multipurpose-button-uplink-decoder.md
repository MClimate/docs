# ⬆ Multipurpose Button Uplink decoder

```
function Decoder(data){
    function decbin(byte){
        return (parseInt(byte, 16).toString(2)).padStart(8, '0');
    }
    var batteryTmp = ("0" + `${data[2] + data[3]}`.toString(16)).substr(-2)[0];
    var batteryVoltageCalculated = 2 + parseInt("0x"+ batteryTmp , 16) * 0.1;
    var thermistorProperlyConnected = decbin(data[5])[5] == 0;
    var extT1 = ("0" + data[5].toString(16)).substr(-2)[1];
    var extT2 = ("0" + `${data[6]+data[7]}`.toString(16)).substr(-2);
    var temperature = thermistorProperlyConnected ? parseInt(`0x${extT1}${extT2}`, 16) * 0.1 : 0;
    var pressEvent = `${data[8] + data[9]}`;
    if (data[1] == 1) {
        return {
            pressEvent: pressEvent,
            batteryVoltage: batteryVoltageCalculated,
            thermistorProperlyConnected:thermistorProperlyConnected,
            temperature: temperature

        }
    }
}

```

## Helium Decoder&#x20;

```
function Decoder(bytes, port, uplink_info) {
    function decbin(byte){
        return (parseInt(byte, 16).toString(2)).padStart(8, '0');
    }
    var data = bytes.map(function (byte) {
        var number = parseInt(byte).toString(16);
        if( (number.length % 2) > 0) { number= "0" + number }
        return number;
    });
    var batteryTmp = ("0" + `${data[1]}`.toString(16)).substr(-2);
    var batteryVoltageCalculated = 2 + parseInt("0x"+ batteryTmp , 16) * 0.1;
    var thermistorProperlyConnected = decbin(data[2])[5] == 0;
    var extT1 = ("0" + data[2].toString(16)).substr(-2)[1];
    var extT2 = ("0" + `${data[3]}`.toString(16)).substr(-2);
    var temperature = thermistorProperlyConnected ? parseInt(`0x${extT1}${extT2}`, 16) * 0.1 : 0;
    var pressEvent = `${data[4]}`;
    if (data[0] == '01') {
        return {
            "pressEvent": pressEvent,
            "batteryVoltage": batteryVoltageCalculated,
            "thermistorProperlyConnected":thermistorProperlyConnected,
            "temperature": temperature
        }
    }
}
```
