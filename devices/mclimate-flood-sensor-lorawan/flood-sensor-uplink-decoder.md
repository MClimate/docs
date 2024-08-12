# ⬆️ Flood Sensor Uplink Decoder

### Uplink Decoder  - TTI (JavaScript ECMAScript 5)

```
function decodeUplink(input) {
	var bytes = input.bytes;
	var data = {};
	var decbin = function (number) {
		return parseInt(number, 10).toString(2);
	};
	var byteArray = bytes.map(function (byte) {
		var number = decbin(byte);
		return Array(9 - number.length).join('0') + number;
	});
	let messageTypes = ['keepalive', 'testButtonPressed', 'floodDetected', 'fraudDetected','fraudDetected'];
	toBool = function (value) {
		return value == '1';
	};
	const handleKeepAliveData = (byteArray, data) => {
		shortPackage = function (byteArray) {
			data.reason = messageTypes[parseInt(byteArray[0].slice(0, 3), 2)];
			data.boxTamper = toBool(byteArray[0][4]);
			data.flood = toBool(byteArray[0][6]);
			data.battery = (parseInt(byteArray[1], 2) * 16) / 1000;
			return data
		};
		longPackage = function (byteArray) {
				data.reason = messageTypes[parseInt(byteArray[0].slice(0, 3), 2)];
				data.boxTamper = toBool(byteArray[0][4]);
				data.flood = toBool(byteArray[0][6]);
				data.battery = (parseInt(byteArray[1], 2) * 16) / 1000;
				data.temperature = parseInt(byteArray[2], 2);
			return data
		};

		if (byteArray.length > 2) {
			return longPackage(byteArray,data);
		} else {
			return shortPackage(byteArray,data);
		}
	}


	const handleResponse = (bytes, data) => {
		var commands = bytes.map(function (byte) {
			return ("0" + byte.toString(16)).substr(-2);
		});
		commands = commands.slice(0, -3);
		var command_len = 0;

		commands.map(function (command, i) {
			switch (command) {
				case '06':
					{
					command_len = 1;
					data.alarmDuration = parseInt(commands[i + 1], 16) ;
					}
				break;
				case '07':
            		{
                    // console.log(hexData)
						command_len = 2;
						let hardwareVersion = commands[i + 1];
						let softwareVersion = commands[i + 2];
						data.deviceVersions = { hardware: Number(hardwareVersion), software: Number(softwareVersion) } ;
            		}
            		break;
				case '09':
					{
						command_len = 1;
						data.floodEventSendTime = parseInt(commands[i + 1], 16) ;
					}
				break;
				case '12':
					{
						command_len = 2;
						data.keepAliveTime = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
					}
					break;
				case '19':
					{
						command_len = 1;
						var commandResponse = parseInt(commands[i + 1], 16);
						var periodInMinutes = commandResponse * 5 / 60;
						data.joinRetryPeriod = periodInMinutes;
					}
					break;
				case '1b':
					{
						command_len = 1;
						data.uplinkType = parseInt(commands[i + 1], 16);
					}
					break;
				case '1d':
					{
						command_len = 2;
						var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
						var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
						data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
					}
					break;


				default:
					break;
			}
			commands.splice(i, command_len);
		});
		return data;
	}

	if (byteArray.length <= 3) {
		data = handleKeepAliveData(byteArray, data);
	} else {
		data = handleResponse(bytes, data);
		byteArray = byteArray.slice(-3);
		data = handleKeepAliveData(byteArray, data);
	}
	return { data: data };
}
```

### Uplink Decoder (JavaScript ECMAScript 6)

```
function Decoder(bytes){
     let byteArray = bytes.match(/.{1,2}/g).map(byte => 
            (parseInt(byte, 16).toString(2)).padStart(8, '0')
        )
    let messageTypes = ['keepalive', 'testButtonPressed', 'floodDetected', 'fraudDetected','fraudDetected'];
    const toBool = value => value == '1';
    const shortPackage = (byteArray) => {
        return {
            reason: messageTypes[parseInt(byteArray[0].slice(0, 3),2)],
            boxTamper: toBool(byteArray[0][4]),
            flood: toBool(byteArray[0][6]),
            battery: (parseInt(byteArray[1], 2) * 16)/1000,
        }
    }
    const longPackage = (byteArray) => {
        return {
            reason: messageTypes[parseInt(byteArray[0].slice(0, 3),2)],
            boxTamper: toBool(byteArray[0][4]),
            flood: toBool(byteArray[0][6]),
            battery: (parseInt(byteArray[1], 2) * 16)/1000,
            temp1: parseInt(byteArray[2], 2),
        }
    }
    if(byteArray.length > 2){
        return longPackage(byteArray);
    }else{
        return shortPackage(byteArray);
    }
}
```

### Uplink Decoder  - Chirpstack

```
function decodeUplink(input) {
	var bytes = input.bytes;
	var decbin = function(number) {
		return parseInt(number, 10).toString(2);
	};
	var byteArray = bytes.map(function(byte) {
		var number = decbin(byte);
		return Array(9 - number.length).join('0') + number;
	});
	var messageTypes = [ 'keepalive', 'testButtonPressed', 'floodDetected', 'fraudDetected' ];
	toBool = function(value) {
		return value == '1';
	};
	shortPackage = function(byteArray) {
		return {
			data: {
                reason: messageTypes[parseInt(byteArray[0].slice(0, 3),2)],
                boxTamper: toBool(byteArray[0][4]),
                flood: toBool(byteArray[0][6]),
                battery: (parseInt(byteArray[1], 2) * 16)/1000,
			}
		};
	};
	longPackage = function(byteArray) {
		return {
			data: {
                reason: messageTypes[parseInt(byteArray[0].slice(0, 3),2)],
                boxTamper: toBool(byteArray[0][4]),
                flood: toBool(byteArray[0][6]),
                battery: (parseInt(byteArray[1], 2) * 16)/1000,
                temperature: parseInt(byteArray[2], 2),
			}
		};
	};
	if (byteArray.length > 2) {
		return longPackage(byteArray);
	} else {
		return shortPackage(byteArray);
	}
}
```
