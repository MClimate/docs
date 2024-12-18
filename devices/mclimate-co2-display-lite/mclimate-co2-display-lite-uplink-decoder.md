# ⬆️ MClimate CO2 Display lite Uplink decoder

## Decoder (JavaScript ES5):

```
function decodeUplink(input) {
    try{
        var bytes = input.bytes;
        var data = {};
        const toBool = value => value == '1';
        const calculateTemperature = (rawData) => (rawData - 400) / 10;
        const calculateHumidity = (rawData) => (rawData * 100) / 256;
        
        function handleKeepalive(bytes) {
            let data = {};
        
            // Temperature calculation from two bytes
            let temperatureRaw = (bytes[1] << 8) | bytes[2]; // Shift byte[1] left by 8 bits and OR with byte[2]
            data.sensorTemperature = Number(calculateTemperature(temperatureRaw).toFixed(2));
        
            // Humidity calculation
            data.relativeHumidity = Number(calculateHumidity(bytes[3]).toFixed(2));
        
            // Battery voltage calculation from two bytes
            let batteryVoltageRaw = (bytes[4] << 8) | bytes[5];
            data.batteryVoltage = Number((batteryVoltageRaw / 1000).toFixed(2));
        
            // CO2 calculation from bytes 6 and 7
            let co2Low = bytes[6]; // Lower byte of CO2
            let co2High = (bytes[7] & 0xF8) >> 3; // Mask the upper 5 bits and shift them right
            data.CO2 = (co2High << 8) | co2Low; // Shift co2High left by 8 bits and combine with co2Low
        
            // Power source status
            data.powerSourceStatus = bytes[7] & 0x07; // Extract the last 3 bits directly
        
            // Light intensity from two bytes
            let lightIntensityRaw = (bytes[8] << 8) | bytes[9];
            data.lux = lightIntensityRaw;
        
            return data;
        }
    
        function handleResponse(bytes, data){
        var commands = bytes.map(function(byte){
            return ("0" + byte.toString(16)).substr(-2); 
        });
        commands = commands.slice(0,-8);
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
                case '1f':
                    {
                        command_len = 4;
                        let good_medium = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
                        let medium_bad = parseInt(`${commands[i + 3]}${commands[i + 4]}`, 16);
                        
                        data.boundaryLevels = { good_medium: Number(good_medium), medium_bad: Number(medium_bad) } ;
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
                case '21':
                    {
                        command_len = 2;
                        data.autoZeroValue = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
                    }
                break;
                case '25':
                    {
                        command_len = 3;
                        let good_zone = parseInt(commands[i + 1], 16);
                        let medium_zone = parseInt(commands[i + 2], 16);
                        let bad_zone = parseInt(commands[i + 3], 16);
                        
                        data.measurementPeriod = { good_zone: Number(good_zone), medium_zone: Number(medium_zone), bad_zone: Number(bad_zone) } ;
                    }
                break;
                case '2b':
                    {
                        command_len = 1;
                        data.autoZeroPeriod = parseInt(commands[i + 1], 16);
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
                case '80':
                    {
                        command_len = 1;
                        data.measurementBlindTime = parseInt(commands[i + 1], 16) ;
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
            bytes = bytes.slice(-10);
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
        var decbin = function (number) {
            if (number < 0) {
                number = 0xFFFFFFFF + number + 1;
            }
            number = number.toString(2);
            return "00000000".substr(number.length) + number;
        };

        function handleKeepalive(bytes, data) {
            var tempHex = '0' + bytes[1].toString(16) + bytes[2].toString(16);
            var tempDec = parseInt(tempHex, 16);
            var temperatureValue = calculateTemperature(tempDec);
            var humidityValue = calculateHumidity(bytes[3]);
            var batteryHex = '0' + bytes[4].toString(16) + bytes[5].toString(16);
            var batteryVoltageCalculated = parseInt(batteryHex, 16) / 1000;
            var temperature = temperatureValue;
            var humidity = humidityValue;
            var batteryVoltage = batteryVoltageCalculated;
            var ppmBin = decbin(bytes[6]);
            var ppmBin2 = decbin(bytes[7]);
            ppmBin = ppmBin2.slice(0, 5) + ppmBin;
            var ppm = parseInt(ppmBin, 2);
            var powerSourceStatus = ppmBin2.slice(5, 8);
            var lux = parseInt('0' + bytes[8].toString(16) + bytes[9].toString(16), 16);

            data.sensorTemperature = Number(temperature.toFixed(2));
            data.relativeHumidity = Number(humidity.toFixed(2));
            data.batteryVoltage = Number(batteryVoltage.toFixed(3));
            data.CO2 = ppm;
            data.powerSourceStatus = parseInt(powerSourceStatus, 2);
            data.lux = lux;

            return data;
        }

        function handleResponse(bytes, data) {
            var commands = bytes.map(function (byte) {
                return ("0" + byte.toString(16)).substr(-2);
            });
            commands = commands.slice(0, -8);
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
                    case '1f':
                        command_len = 4;
                        var good_medium = parseInt(commands[i + 1] + commands[i + 2], 16);
                        var medium_bad = parseInt(commands[i + 3] + commands[i + 4], 16);
                        data.boundaryLevels = { good_medium: Number(good_medium), medium_bad: Number(medium_bad) };
                        break;
                    case '1d':
                        command_len = 2;
                        var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
                        var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                        data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
                        break;
                    case '21':
                        command_len = 2;
                        data.autoZeroValue = parseInt(commands[i + 1] + commands[i + 2], 16);
                        break;
                    case '25':
                        command_len = 3;
                        var good_zone = parseInt(commands[i + 1], 16);
                        var medium_zone = parseInt(commands[i + 2], 16);
                        var bad_zone = parseInt(commands[i + 3], 16);
                        data.measurementPeriod = { good_zone: Number(good_zone), medium_zone: Number(medium_zone), bad_zone: Number(bad_zone) };
                        break;
                    case '2b':
                        command_len = 1;
                        data.autoZeroPeriod = parseInt(commands[i + 1], 16);
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
                    case '80':
                        command_len = 1;
                        data.measurementBlindTime = parseInt(commands[i + 1], 16);
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
            bytes = bytes.slice(-10);
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
