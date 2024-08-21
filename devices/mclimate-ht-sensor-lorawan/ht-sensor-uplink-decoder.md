# ⬆️ HT Sensor Uplink Decoder

### MClimate HT Sensor Uplink Parser

```
var calculateTemperature = function (rawData){return (rawData - 400) / 10};
var calculateHumidity = function(rawData){return (rawData * 100) / 256};
function decbin(byte){
    return (parseInt(byte, 16).toString(2)).padStart(8, '0');
}
function Decoder(hexData){
    var data = hexData;
    var tempHex = ("0" + data[1].toString(16)).substr(-2) + ("0" + data[2].toString(16)).substr(-2);
    var tempDec = parseInt(tempHex, 16);
    var temperatureValue = calculateTemperature(tempDec);
    var humidityValue = calculateHumidity(data[3]);
    var batteryTmp = ("0" + data[4].toString(16)).substr(-2)[0];
    var batteryVoltageCalculated = 2 + parseInt("0x" + batteryTmp, 16) * 0.1;
    var reason = data[0];
    var temperature = temperatureValue;
    var humidity = humidityValue;
    var batteryVoltage = batteryVoltageCalculated;
    var thermistorProperlyConnected = decbin(data[5])[5] == 0;
    var extT1 = ("0" + data[5].toString(16)).substr(-2)[1];
    var extT2 = ("0" + data[6].toString(16)).substr(-2);
    var extThermistorTemperature = thermistorProperlyConnected ? parseInt(`0x${extT1}${extT2}`, 16) * 0.1 : 0;

    // check if it is a keepalive
    if (reason == 1) {
        return {
            reason: 'keepalive',
            temperature: temperature,
            humidity:humidity,
            batteryVoltage: batteryVoltage,
            thermistorProperlyConnected:thermistorProperlyConnected,
            extThermistorTemperature:extThermistorTemperature

        }
    }
}
```

### TTN V3 Decoder (JavaScript ES5):

```
function decodeUplink(input) {
	try{
		var bytes = input.bytes;
		var data = {};
		var calculateTemperature = function (rawData){return (rawData - 400) / 10};
		var calculateHumidity = function(rawData){return (rawData * 100) / 256};
		function decbin (number) {
		if (number < 0) {
			number = 0xFFFFFFFF + number + 1;
		}
		return parseInt(number, 10).toString(2);
		}

		function handleKeepalive(bytes, data){
			var tempHex = '0' + bytes[1].toString(16) + bytes[2].toString(16);
			var tempDec = parseInt(tempHex, 16);
			var temperatureValue = calculateTemperature(tempDec);
			var humidityValue = calculateHumidity(bytes[3]);
			var batteryTmp = ("0" + bytes[4].toString(16)).substr(-2)[0];
			var batteryVoltageCalculated = 2 + parseInt("0x" + batteryTmp, 16) * 0.1;
			var temperature = temperatureValue;
			var humidity = humidityValue;
			var batteryVoltage = batteryVoltageCalculated;
			var thermistorProperlyConnected = decbin(bytes[5])[5] == 0;

			var extT1 = ("0" + bytes[5].toString(16)).substr(-2)[1];

			var extT2 = ("0" + bytes[6].toString(16)).substr(-2);
			var extThermistorTemperature = 0;
			if(thermistorProperlyConnected){
				extThermistorTemperature = parseInt("0x"+extT1+""+extT2, 16) * 0.1;
			}

			data.sensorTemperature = Number(temperature.toFixed(2));
			data.relativeHumidity = Number(humidity.toFixed(2));
			data.batteryVoltage = Number(batteryVoltage.toFixed(2));
			data.thermistorProperlyConnected = thermistorProperlyConnected;
			data.extThermistorTemperature = extThermistorTemperature;
			return data;
		}
	
		function handleResponse(bytes, data){

		var commands = bytes.map(function(byte){
			return ("0" + byte.toString(16)).substr(-2); 
		});
		commands = commands.slice(0,-7);
		var command_len = 0;
	
		commands.map(function (command, i) {
			switch (command) {
				case '04':
					{
						command_len = 2;
						var hardwareVersion = commands[i + 1];
						var softwareVersion = commands[i + 2];
						data.deviceVersions = { hardware: Number(hardwareVersion), software: Number(softwareVersion) };
					}
				break;
				case '12':
					{
						command_len = 1;
						data.keepAliveTime = parseInt(commands[i + 1], 16);
					}
				break;
				case '19':
					{
						command_len = 1;
						var commandResponse = parseInt(commands[i + 1], 16);
						var periodInMinutes = commandResponse * 5 / 60;
						data.joinRetryPeriod =  periodInMinutes;
					}
				break;
				case '1b':
					{
						command_len = 1;
						data.uplinkType = parseInt(commands[i + 1], 16) ;
					}
				break;
				case '1d':
					{
						command_len = 2;
						var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
						var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
						data.watchDogParams= { wdpC: wdpC, wdpUc: wdpUc } ;
					}
				break;
				default:
					break;
			}
			commands.splice(i,command_len);
		});
		return data;
		}
		if (bytes[0] == 1) {
			data = handleKeepalive(bytes, data);

		}else{
			data = handleResponse(bytes,data);
			bytes = bytes.slice(-7);
			data = handleKeepalive(bytes, data);
		}
		return {data: data};
	} catch (e) {
		throw new Error(e);
	}
}
```

### Chirpstack Decoder (JavaScript ES5)

```
function Decode(fPort, bytes, variables) {
    try{
        var data = {};
        var calculateTemperature = function (rawData){return (rawData - 400) / 10};
        var calculateHumidity = function(rawData){return (rawData * 100) / 256};
        function decbin (number) {
        if (number < 0) {
            number = 0xFFFFFFFF + number + 1;
        }
        return parseInt(number, 10).toString(2);
        }
        function handleKeepalive(bytes, data){
            var tempHex = '0' + bytes[1].toString(16) + bytes[2].toString(16);
            var tempDec = parseInt(tempHex, 16);
            var temperatureValue = calculateTemperature(tempDec);
            var humidityValue = calculateHumidity(bytes[3]);
            var batteryTmp = ("0" + bytes[4].toString(16)).substr(-2)[0];
            var batteryVoltageCalculated = 2 + parseInt("0x" + batteryTmp, 16) * 0.1;
            var temperature = temperatureValue;
            var humidity = humidityValue;
            var batteryVoltage = batteryVoltageCalculated;
            var thermistorProperlyConnected = decbin(bytes[5])[5] == 0;
            var extT1 = ("0" + bytes[5].toString(16)).substr(-2)[1];
            var extT2 = ("0" + bytes[6].toString(16)).substr(-2);
            var extThermistorTemperature = 0;
            if(thermistorProperlyConnected){
                extThermistorTemperature = parseInt("0x"+extT1+""+extT2, 16) * 0.1;
            }
            data.sensorTemperature = Number(temperature.toFixed(2));
            data.relativeHumidity = Number(humidity.toFixed(2));
            data.batteryVoltage = Number(batteryVoltage.toFixed(2));
            data.thermistorProperlyConnected = thermistorProperlyConnected;
            data.extThermistorTemperature = extThermistorTemperature;
            return data;
        }
    
        function handleResponse(bytes, data){
        var commands = bytes.map(function(byte){
            return ("0" + byte.toString(16)).substr(-2); 
        });
        commands = commands.slice(0,-7);
        var command_len = 0;
    
        commands.map(function (command, i) {
            switch (command) {
                case '04':
                    {
                        command_len = 2;
                        var hardwareVersion = commands[i + 1];
                        var softwareVersion = commands[i + 2];
                        data.deviceVersions = { hardware: Number(hardwareVersion), software: Number(softwareVersion) };
                    }
                break;
                case '12':
                    {
                        command_len = 1;
                        data.keepAliveTime = parseInt(commands[i + 1], 16);
                    }
                break;
                case '19':
                    {
                        command_len = 1;
                        var commandResponse = parseInt(commands[i + 1], 16);
                        var periodInMinutes = commandResponse * 5 / 60;
                        data.joinRetryPeriod =  periodInMinutes;
                    }
                break;
                case '1b':
                    {
                        command_len = 1;
                        data.uplinkType = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '1d':
                    {
                        command_len = 2;
                        var deviceKeepAlive = 5;
                        var wdpC = commands[i + 1] == '00' ? false : commands[i + 1] * deviceKeepAlive + 7;
                        var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                        data.watchDogParams= { wdpC: wdpC, wdpUc: wdpUc } ;
                    }
                break;
                default:
                    break;
            }
            commands.splice(i,command_len);
        });
        return data;
        }
        if (bytes[0] == 1) {
            data = handleKeepalive(bytes, data);
        }else{
            data = handleResponse(bytes,data);
            bytes = bytes.slice(-7);
            data = handleKeepalive(bytes, data);
        }
        return data;
    } catch (e) {
        console.log(e)
        throw new Error('Unhandled data');
    }
}
```

### DataCake Decoder

```
function decodeUplink(input) {
    try {
        var bytes = input.bytes;
        var data = {};

        // Helper functions
        var calculateTemperature = function (rawData) { return (rawData - 400) / 10; };
        var calculateHumidity = function (rawData) { return (rawData * 100) / 256; };
        function decbin(number) {
            if (number < 0) {
                number = 0xFFFFFFFF + number + 1;
            }
            return parseInt(number, 10).toString(2);
        }

        function handleKeepalive(bytes, data) {
            var tempHex = '0' + bytes[1].toString(16) + bytes[2].toString(16);
            var tempDec = parseInt(tempHex, 16);
            var temperatureValue = calculateTemperature(tempDec);
            var humidityValue = calculateHumidity(bytes[3]);
            var batteryTmp = ("0" + bytes[4].toString(16)).substr(-2)[0];
            var batteryVoltageCalculated = 2 + parseInt("0x" + batteryTmp, 16) * 0.1;
            var thermistorProperlyConnected = decbin(bytes[5])[5] == 0;
            var extT1 = ("0" + bytes[5].toString(16)).substr(-2)[1];
            var extT2 = ("0" + bytes[6].toString(16)).substr(-2);
            var extThermistorTemperature = thermistorProperlyConnected ? parseInt("0x" + extT1 + extT2, 16) * 0.1 : 0;

            data.sensorTemperature = Number(temperatureValue.toFixed(2));
            data.relativeHumidity = Number(humidityValue.toFixed(2));
            data.batteryVoltage = Number(batteryVoltageCalculated.toFixed(2));
            data.thermistorProperlyConnected = thermistorProperlyConnected;
            data.extThermistorTemperature = extThermistorTemperature;
            return data;
        }

        function handleResponse(bytes, data) {
            var commands = bytes.map(function (byte) {
                return ("0" + byte.toString(16)).substr(-2);
            });
            commands = commands.slice(0, -7);
            var i = 0;

            while (i < commands.length) {
                var command = commands[i];
                switch (command) {
                    case '04':
                        data.deviceVersions = {
                            hardware: Number(commands[i + 1]),
                            software: Number(commands[i + 2])
                        };
                        i += 3;
                        break;
                    case '12':
                        data.keepAliveTime = parseInt(commands[i + 1], 16);
                        i += 2;
                        break;
                    case '19':
                        var commandResponse = parseInt(commands[i + 1], 16);
                        data.joinRetryPeriod = (commandResponse * 5) / 60;
                        i += 2;
                        break;
                    case '1b':
                        data.uplinkType = parseInt(commands[i + 1], 16);
                        i += 2;
                        break;
                    case '1d':
                        var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
                        var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                        data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
                        i += 3;
                        break;
                    default:
                        i += 1;
                        break;
                }
            }
            return data;
        }

        if (bytes[0] == 1) {
            data = handleKeepalive(bytes, data);
        } else {
            data = handleResponse(bytes, data);
            bytes = bytes.slice(-7);
            var keepaliveData = handleKeepalive(bytes, {});
            for (var key in keepaliveData) {
                data[key] = keepaliveData[key];
            }
        }
        return { data: data };
    } catch (e) {
        throw new Error(e.message);
    }
}

function Decoder(payload, port) {
    var decoded = decodeUplink({ bytes: payload, fPort: port }).data;

    // Array where we store the fields that are being sent to Datacake
    var datacakeFields = [];

    // Take each field from decoded and convert them to Datacake format
    for (var key in decoded) {
        if (decoded.hasOwnProperty(key)) {
            datacakeFields.push({ field: key.toUpperCase(), value: decoded[key] });
        }
    }

    // Forward data to Datacake
    return datacakeFields;
}
```
