# ⬆ Open/Close Sensor uplink decoder

## Recommended decoder (JavaScript ES6)

```
function decoder(data) {
    const decbin = (byte)=>{
            return (parseInt(byte, 16).toString(2)).padStart(8, '0');
        }
	let hexArray = data.match(/.{1,2}/g).map((byte)=>{ return byte })
    let batteryTmp = ("0" + `${hexArray[1]}`.toString(16)).substr(-2);
    let batteryVoltageCalculated = ((parseInt("0x"+ batteryTmp , 16) * 8) + 1600)/1000;
    let thermistorProperlyConnected = decbin(hexArray[2])[5] == 0;
    let extT1 = ("0" + hexArray[2].toString(16)).substr(-2)[1];
    let extT2 = ("0" + `${hexArray[3]}`.toString(16)).substr(-2);
    let temperature = (thermistorProperlyConnected ? parseInt(`0x${extT1}${extT2}`, 16) * 0.1 : 0).toFixed(2);
    let counter = parseInt(`0x${hexArray[4]}${hexArray[5]}${hexArray[6]}`, 16)
    let status = parseInt(hexArray[7],16);
    let events = {"01": "keepalive", "20" : "reed switch", "21" : "push button"}
    return  {
        event: events[hexArray[0]],
        status: status,
        counter: counter,
        batteryVoltage: batteryVoltageCalculated,
        thermistorProperlyConnected:thermistorProperlyConnected,
        temperature: Number(temperature)
    }
}
```

## TTN V3 Decoder (JavaScript ES5):

```
function decodeUplink(input) {
	var bytes = input.bytes;
    function decbin(byte){
        return (parseInt(byte, 16).toString(2)).padStart(8, '0');
    }
    var data = bytes.map(function (byte) {
        var number = parseInt(byte).toString(16);
        if( (number.length % 2) > 0) { number= "0" + number }
        return number;
    });
    var batteryTmp = ("0" + `${data[1]}`.toString(16)).substr(-2);
    var batteryVoltageCalculated = ((parseInt("0x"+ batteryTmp , 16) * 8) + 1600)/1000;
    var thermistorProperlyConnected = decbin(data[2])[5] == 0;
    var extT1 = ("0" + data[2].toString(16)).substr(-2)[1];
    var extT2 = ("0" + `${data[3]}`.toString(16)).substr(-2);
    var temperature = (thermistorProperlyConnected ? parseInt(`0x${extT1}${extT2}`, 16) * 0.1 : 0).toFixed(2);
    var counter = parseInt(`0x${data[4]}${data[5]}${data[6]}`, 16)
    var status = parseInt(data[7],16);
    var events = {01: "keepalive", 20 : "reed switch", 21 : "push button"}
    return {
        data: {
            event: events[Number(data[0])],
            status: status,
            counter: counter,
            batteryVoltage: batteryVoltageCalculated,
            thermistorProperlyConnected:thermistorProperlyConnected,
            temperature: Number(temperature)
        }
    }
}
```
