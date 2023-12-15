# ⬆ T-Valve Uplink Decoder

##

## Recommended decoder (JavaScript ES6)

```
function Decoder(bytes){
    let byteArray = bytes.match(/.{1,2}/g).map(byte => 
            (parseInt(byte, 16).toString(2)).padStart(8, '0')
        )

    let messageTypes = ['keepalive', 'testButtonPressed', 'floodDetected', 'controlButtonPressed', 'fraudDetected'];
    const toBool = value => value == '1';
    const shortPackage = (byteArray) => {
        return {
            reason: messageTypes[parseInt(byteArray[0].slice(0, 2))],
            valveState: toBool(byteArray[0][3]),
            boxTamper: toBool(byteArray[0][4]),
            floodDetectionWireState: toBool(byteArray[0][5]),
            flood: toBool(byteArray[0][6]),
            magnet: toBool(byteArray[0][7]),
            alarmValidated: toBool(byteArray[1][0]),
            manualOpenIndicator: toBool(byteArray[1][1]),
            manualCloseIndicator: toBool(byteArray[1][2]),
        }
    }
    const longPackage = (byteArray) => {
        return {
            reason: messageTypes[parseInt(byteArray[0].slice(0, 2))],
            valveState: toBool(byteArray[0][3]),
            boxTamper: toBool(byteArray[0][4]),
            floodDetectionWireState: toBool(byteArray[0][5]),
            flood: toBool(byteArray[0][6]),
            magnet: toBool(byteArray[0][7]),
            alarmValidated: toBool(byteArray[1][0]),
            manualOpenIndicator: toBool(byteArray[1][1]),
            manualCloseIndicator: toBool(byteArray[1][2]),
            closeTime: parseInt(byteArray[2], 2),
            openTime: parseInt(byteArray[3], 2),
            temp1: parseInt(byteArray[4], 2),
            temp2: parseInt(byteArray[5], 2),
            battery: (parseInt(byteArray[6], 2) * 4) + 3000,
        }
    }
    if(byteArray.length > 2){
        return longPackage(byteArray);
    }else{
        return shortPackage(byteArray);
    }
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

## TTN V3 Decoder (JavaScript ES5):

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
