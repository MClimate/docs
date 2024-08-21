# ⬆️ T-Valve Uplink Decoder

##

## Recommended decoder&#x20;

```
function decodeUplink(input) {
	var bytes = input.bytes;
	var data = {};
	var messageTypes = ['keepalive', 'testButtonPressed', 'floodDetected', 'controlButtonPressed', 'fraudDetected'];

	function shortPackage(byteArray) {
		data.reason = 'keepalive',
			data.waterTemp = (byteArray[0] & 0xFF) / 2, // Extract all 8 bits (7:0) from byte 0 and divide by 2
			data.valveState = !!(byteArray[1] & 0b10000000), // Extract bit 7 from byte 1
			data.ambientTemp = ((byteArray[1] & 0b01111111) - 20) / 2; // Extract bits 6:0 from byte 1, subtract 20, and divide by 2
		return data
	}
	function longPackage(byteArray) {
		data.reason = messageTypes[(byteArray[0] >> 5) & 0b111],  // Extract bits 7:5 using right shift and mask
			data.boxTamper = !!(byteArray[0] & (1 << 3)),             // Extract bit 3
			data.floodDetectionWireState = !!(byteArray[0] & (1 << 2)), // Extract bit 2
			data.flood = !!(byteArray[0] & (1 << 1)),                 // Extract bit 1
			data.magnet = !!(byteArray[0] & 1),                       // Extract bit 0
			data.alarmValidated = !!(byteArray[1] & (1 << 7)),        // Extract bit 7
			data.manualOpenIndicator = !!(byteArray[1] & (1 << 6)),   // Extract bit 6
			data.manualCloseIndicator = !!(byteArray[1] & (1 << 5)),  // Extract bit 5
			data.softwareVersion = byteArray[1] & 0b11111,            // Extract bits 4:0
			data.closeTime = byteArray[2],                            // Byte 2
			data.openTime = byteArray[3],                             // Byte 3
			data.battery = ((byteArray[4] * 8) + 1600) / 1000;        // Byte 4, battery calculation
		return data;
	}

	const handleResponse = (bytes, data) => {
		var commands = bytes.map(function (byte) {
			return ("0" + byte.toString(16)).substr(-2);
		});
		var command_len = 0;
		commands.map(function (command, i) {
			switch (command) {
				case '0e':
					{
						command_len = 4;
						let openingTime = (parseInt(commands[i + 1], 16) << 8) | parseInt(commands[i + 2], 16)
						let closingTime = (parseInt(commands[i + 3], 16) << 8) | parseInt(commands[i + 4], 16)
						data.openCloseTimeExtended = { openingTime: Number(openingTime), closingTime: Number(closingTime) };
					}
					break;
				case '0f':
					{
						command_len = 1;
						data.emergencyOpenings = parseInt(commands[i + 1], 16);
					}
					break;
				case '10':
					{
						command_len = 1;
						data.floodAlarmTime = parseInt(commands[i + 1], 16);
					}
					break;
				case '11':
					{
						command_len = 1;
						data.workingVoltage = parseInt(`${commands[i + 1]}`, 16);
					}
					break;
				case '12':
					{
						command_len = 1;
						data.keepAliveTime = parseInt(`${commands[i + 1]}`, 16);
					}
					break;
				case '13':
					{
						command_len = 1;
						data.deviceFloodSensor = parseInt(`${commands[i + 1]}`, 16);
					}
					break;
				case '16':
					{
						command_len = 1;
						var commandResponse = parseInt(commands[i + 1], 16);
						var periodInMinutes = commandResponse * 5 / 60;
						data.joinRetryPeriod = periodInMinutes;
					}
					break;
				case '18':
					{
						command_len = 1;
						data.uplinkType = parseInt(commands[i + 1], 16);
					}
					break;
				case '1a':
					{
						command_len = 2;
						var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
						var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
						data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
					}
					break;
				case 'a0':

					command_len = 4;
					var fuota_address = (parseInt(commands[i + 1], 16) << 24) | (parseInt(commands[i + 2], 16) << 16) | (parseInt(commands[i + 3], 16) << 8) | parseInt(commands[i + 4], 16);
					var fuota_address_raw = (parseInt(commands[i + 1], 16) << 24) | (parseInt(commands[i + 2], 16) << 16) | (parseInt(commands[i + 3], 16) << 8) | parseInt(commands[i + 4], 16);
					data.fuota = { fuota_address, fuota_address_raw };
					break;
				default:
					break;
			}
			commands.splice(i, command_len);
		});
		return data;
	}

	if (bytes.length == 5) {
		data = longPackage(bytes);
	} else if (bytes.length == 2) {
		data = shortPackage(bytes);
	} else {
		data = longPackage(bytes, data);
		bytes = bytes.slice(5);
		data = handleResponse(bytes, data);
	}
	return { data: data };
}
```

## TTN V3 Decoder (T-Valve for flow meter):

```
function decodeUplink(input) {
	var bytes = input.bytes;
	var decbin = function(number) {
		return parseInt(number, 10).toString(2);
	};
	var hexData = bytes.map(function (byte) {
        var number = parseInt(byte).toString(16);
        if( (number.length % 2) > 0) { number= "0" + number }
        return number;
    });
	var byteArray = bytes.map(function(byte) {
		var number = decbin(byte);
		return Array(9 - number.length).join('0') + number;
	});

	var messageTypes = [ 'keepalive', 'testButtonPressed', 'floodDetected', 'controlButtonPressed', 'fraudDetected' ];
	toBool = function(value) {
		return value == '1';
	};
	periodicData = function(byteArray) {
		return {
			data: {
				reason: 'keepalive',
				waterTemp: parseInt(byteArray[0], 2)/2,
				valveState: toBool(byteArray[1][0]),
				ambientTemp: (parseInt(byteArray[1].slice(1, 8), 2)-20)/2,
				flow: parseInt(byteArray[2]+byteArray[3]+byteArray[4]+byteArray[5], 2)
			}
		};
	};
	fullDeviceData = function(byteArray) {
		return {
			data: {
				reason: messageTypes[parseInt(byteArray[0].slice(0, 3),2)],
				boxTamper: toBool(byteArray[0][4]),
				floodDetectionWireState: toBool(byteArray[0][5]),
				flood: toBool(byteArray[0][6]),
				magnet: toBool(byteArray[0][7]),
				alarmValidated: toBool(byteArray[1][0]),
				manualOpenIndicator: toBool(byteArray[1][1]),
				manualCloseIndicator: toBool(byteArray[1][2]),
				closeTime: parseInt(byteArray[2], 2),
				openTime: parseInt(byteArray[3], 2),
				battery: ((parseInt(byteArray[4], 2) * 8) + 1600)/1000,
			}
		};
	};
	if (byteArray.length > 5) {
		return periodicData(byteArray);
	} else {
		return fullDeviceData(byteArray);
	}
}

```

## Chirpstack Decoder:

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

	var messageTypes = [ 'keepalive', 'testButtonPressed', 'floodDetected', 'controlButtonPressed', 'fraudDetected' ];
	toBool = function(value) {
		return value == '1';
	};
	shortPackage = function(byteArray) {
		return {
			data: {
				reason: 'keepalive',
				waterTemp: parseInt(byteArray[0], 2)/2,
				valveState: toBool(byteArray[1][0]),
				ambientTemp: (parseInt(byteArray[1].slice(1, 8), 2)-20)/2,
			}
		};
	};
	longPackage = function(byteArray) {
		return {
			data: {
				reason: messageTypes[parseInt(byteArray[0].slice(0, 3),2)],
				boxTamper: toBool(byteArray[0][4]),
				floodDetectionWireState: toBool(byteArray[0][5]),
				flood: toBool(byteArray[0][6]),
				magnet: toBool(byteArray[0][7]),
				alarmValidated: toBool(byteArray[1][0]),
				manualOpenIndicator: toBool(byteArray[1][1]),
				manualCloseIndicator: toBool(byteArray[1][2]),
				closeTime: parseInt(byteArray[2], 2),
				openTime: parseInt(byteArray[3], 2),
				battery: ((parseInt(byteArray[4], 2) * 8) + 1600)/1000,
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
