# ⬆️ MClimate HT Display Lite Uplink decoder

## Decoder (JavaScript ES5):

```
function decodeUplink(input) {
        try{
            var bytes = input.bytes;
            var data = {};
            const toBool = value => value == '1';
            var calculateTemperature = function (rawData){return (rawData - 400) / 10};
            var calculateHumidity = function(rawData){return (rawData * 100) / 256};
            function handleKeepalive(bytes, data){
                var tempRaw = (bytes[1] << 8) | bytes[2];
                var temperatureValue = calculateTemperature(tempRaw);
                var humidityValue = calculateHumidity(bytes[3]);
                var lux = (bytes[4] << 8) | bytes[5];

                let batteryVoltageCalculated = ((bytes[6] << 8) | bytes[7])/1000;
                
                var powerSourceStatus = parseInt(bytes[8], 16);

                data.sensorTemperature = Number(temperatureValue.toFixed(2));
                data.relativeHumidity = Number(humidityValue.toFixed(2));
                data.batteryVoltage = Number(batteryVoltageCalculated.toFixed(3));
                data.powerSourceStatus = powerSourceStatus;
                data.lux = lux;

                return data;
            }
        
            function handleResponse(bytes, data){
            var commands = bytes.map(function(byte){
                return ("0" + byte.toString(16)).substr(-2); 
            });
            commands = commands.slice(0,-9);
            var command_len = 0;
        
            commands.map(function (command, i) {
                console.log(command)
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
                    case '14':
                        {
                            command_len = 1;
                            data.childLock = toBool(parseInt(commands[i + 1], 16)) ;
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
                    case '34':
                        {
                            command_len = 1;
                            data.displayRefreshPeriod = parseInt(commands[i + 1], 16) ;
                        }
                    break;
                    case '41':
                        {
                            command_len = 1;
                            data.currentTemperatureVisibility = parseInt(commands[i + 1], 16) ;
                        }
                    break;
                    case '43':
                        {
                            command_len = 1;
                            data.humidityVisibility = parseInt(commands[i + 1], 16) ;
                        }
                    break;
                    case '45':
                        {
                            command_len = 1;
                            data.lightIntensityVisibility = parseInt(commands[i + 1], 16) ;
                        }
                    break;
                    case '47':
                        {
                            command_len = 1;
                            data.measurementBlindTime = parseInt(commands[i + 1], 16) ;
                        }
                    break;
                    case '49':
                        {
                            command_len = 1;
                            data.measurementPeriod = parseInt(commands[i + 1], 16) ;
                        }
                    break;
                    case 'a4':
                        {
                            command_len = 1;
                            data.region = parseInt(commands[i + 1], 16);
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
                bytes = bytes.slice(-9);
                data = handleKeepalive(bytes, data);
            }
            return {data: data};
        } catch (e) {
            console.log(e)
            throw new Error('Unhandled data');
        }
    }
```

## DataCake Decoder

```
function decodeUplink(input) {
    try {
        var bytes = input.bytes;
        var data = {};
        var toBool = function (value) { return value == '1'; };
        var calculateTemperature = function (rawData) { return (rawData - 400) / 10; };
        var calculateHumidity = function (rawData) { return (rawData * 100) / 256; };

        function handleKeepalive(bytes, data) {
            var tempRaw = (bytes[1] << 8) | bytes[2];
            var temperatureValue = calculateTemperature(tempRaw);
            var humidityValue = calculateHumidity(bytes[3]);
            var lux = (bytes[4] << 8) | bytes[5];

            var batteryVoltageCalculated = ((bytes[6] << 8) | bytes[7]) / 1000;
            var powerSourceStatus = parseInt(bytes[8], 16);

            data.sensorTemperature = Number(temperatureValue.toFixed(2));
            data.relativeHumidity = Number(humidityValue.toFixed(2));
            data.batteryVoltage = Number(batteryVoltageCalculated.toFixed(3));
            data.powerSourceStatus = powerSourceStatus;
            data.lux = lux;

            return data;
        }

        function handleResponse(bytes, data) {
            var commands = bytes.map(function (byte) {
                return ("0" + byte.toString(16)).substr(-2);
            });
            commands = commands.slice(0, -9);
            var command_len = 0;

            commands.map(function (command, i) {
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
                    case '14':
                        command_len = 1;
                        data.childLock = toBool(parseInt(commands[i + 1], 16));
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
                        var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
                        var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                        data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
                        break;
                    case '34':
                        command_len = 1;
                        data.displayRefreshPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case '41':
                        command_len = 1;
                        data.currentTemperatureVisibility = parseInt(commands[i + 1], 16);
                        break;
                    case '43':
                        command_len = 1;
                        data.humidityVisibility = parseInt(commands[i + 1], 16);
                        break;
                    case '45':
                        command_len = 1;
                        data.lightIntensityVisibility = parseInt(commands[i + 1], 16);
                        break;
                    case '47':
                        command_len = 1;
                        data.measurementBlindTime = parseInt(commands[i + 1], 16);
                        break;
                    case '49':
                        command_len = 1;
                        data.measurementPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case 'a4':
                        command_len = 1;
                        data.region = parseInt(commands[i + 1], 16);
                        break;
                    default:
                        break;
                }
                commands.splice(i, command_len);
            });
            return data;
        }

        if (bytes[0] == 1) {
            data = handleKeepalive(bytes, data);
        } else {
            data = handleResponse(bytes, data);
            bytes = bytes.slice(-9);
            data = handleKeepalive(bytes, data);
        }
        return { data: data };
    } catch (e) {
        console.log(e);
        throw new Error('Unhandled data');
    }
}

function Decoder(payload, port) {
    var decoded = decodeUplink({ bytes: payload, fPort: port }).data;

    // Extract Gateway Information
    try {
        decoded.LORA_RSSI = (!!normalizedPayload.gateways && !!normalizedPayload.gateways[0] && normalizedPayload.gateways[0].rssi) || 0;
        decoded.LORA_SNR = (!!normalizedPayload.gateways && !!normalizedPayload.gateways[0] && normalizedPayload.gateways[0].snr) || 0;
        decoded.LORA_DATARATE = normalizedPayload.data_rate;
    } catch (e) {
        console.log(JSON.stringify(e));
    }

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
