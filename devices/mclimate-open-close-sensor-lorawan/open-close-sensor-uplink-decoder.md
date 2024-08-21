# ⬆️ Open/Close Sensor uplink decoder

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

### DataCake Decoder

```
function decodeUplink(input) {
    var bytes = input.bytes;

    function decbin(byte) {
        var bin = (parseInt(byte, 16).toString(2));
        return "00000000".slice(bin.length) + bin; // Manually pad with leading zeros
    }

    function calculateBatteryVoltage(byte) {
        return byte * 8 + 1600;
    }

    function calculateTemperature(rawData) {
        return rawData / 10.0;
    }

    function handleKeepalive(bytes, data) {
        // Byte 1: Device battery voltage
        var batteryVoltage = calculateBatteryVoltage(bytes[1]) / 1000;
        data.batteryVoltage = Number(batteryVoltage.toFixed(1));

        // Byte 2: Thermistor operational status and temperature data (bits 9:8)
        var thermistorConnected = (bytes[2] & 0x04) === 0; // Bit 2
        var temperatureHighBits = bytes[2] & 0x03; // Bits 1:0

        // Byte 3: Thermistor temperature data (bits 7:0)
        var temperatureLowBits = bytes[3];
        var temperatureRaw = (temperatureHighBits << 8) | temperatureLowBits;
        var temperatureCelsius = calculateTemperature(temperatureRaw);
        data.thermistorProperlyConnected = thermistorConnected;
        data.temperature = Number(temperatureCelsius.toFixed(1));

        // Byte 4-6: Counter data
        var counter = parseInt((bytes[4] || '00') + (bytes[5] || '00') + (bytes[6] || '00'), 16);
        data.counter = counter;

        // Byte 7: Status or event code
        var status = parseInt(bytes[7] || '0', 16);
        data.status = status;

        return data;
    }

    function handleResponse(bytes, data) {
        var commands = bytes.map(function (byte) {
            return ("0" + byte.toString(16)).substr(-2);
        });

        commands = commands.slice(0, -5); // Adjust slice to avoid slicing too much data
        var command_len = 0;

        commands.forEach(function (command, i) {
            switch (command) {
                case '04':
                    command_len = 2;
                    var hardwareVersion = commands[i + 1];
                    var softwareVersion = commands[i + 2];
                    data.deviceVersions = { hardware: Number(hardwareVersion), software: Number(softwareVersion) };
                    break;
                case '12':
                    command_len = 1;
                    data.keepAliveTime = parseInt(commands[i + 1], 16);
                    break;
                case '19':
                    command_len = 1;
                    var commandResponse = parseInt(commands[i + 1], 16);
                    var periodInMinutes = commandResponse * 5 / 60;
                    data.joinRetryPeriod = periodInMinutes;
                    break;
                case '1b':
                    command_len = 1;
                    data.uplinkType = parseInt(commands[i + 1], 16);
                    break;
                case '1d':
                    command_len = 2;
                    var wdpC = commands[i + 1] === '00' ? false : parseInt(commands[i + 1], 16);
                    var wdpUc = commands[i + 2] === '00' ? false : parseInt(commands[i + 2], 16);
                    data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
                    break;
                case '1f':
                    command_len = 1;
                    data.sendEventLater = parseInt(commands[i + 1], 16);
                    break;
                default:
                    break;
            }
            commands.splice(i, command_len);
        });
        return data;
    }

    var data = {};

    if (bytes[0] === 1) {
        data = handleKeepalive(bytes, data);
    } else {
        data = handleResponse(bytes, data);
        // Handle the remaining keepalive data if required after response
        bytes = bytes.slice(-5);
        data = handleKeepalive(bytes, data);
    }

    return { data: data };
}

function Decoder(payload, port) {
    var decoded = decodeUplink({ bytes: payload, fPort: port }).data;

    // Array where we store the fields that are being sent to Datacake
    var datacakeFields = [];

    // Convert each field from decoded and convert them to Datacake format
    for (var key in decoded) {
        if (decoded.hasOwnProperty(key)) {
            datacakeFields.push({ field: key.toUpperCase(), value: decoded[key] });
        }
    }

    // Forward data to Datacake
    return datacakeFields;
}
```
