# ⬆️ MClimate CO2 Display Uplink decoder

## Decoder (JavaScript ES5):

```
function decodeUplink(input) {
    try {
        var bytes = input.bytes;
        var data = {};
        const toBool = value => value == '1';
        var calculateTemperature = function (rawData) { return (rawData - 400) / 10 };
        var calculateHumidity = function (rawData) { return (rawData * 100) / 256 };
        let decbin = (number) => {
            if (number < 0) {
                number = 0xFFFFFFFF + number + 1
            }
            number = number.toString(2);
            return "00000000".substr(number.length) + number;
        }
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
            ppmBin = `${ppmBin2.slice(0, 5)}${ppmBin}`
            var ppm = parseInt(ppmBin, 2);
            var powerSourceStatus = ppmBin2.slice(5, 8);
            var lux = parseInt('0' + bytes[8].toString(16) + bytes[9].toString(16), 16);
            var pir = toBool(bytes[10]);
            data.sensorTemperature = Number(temperature.toFixed(2));
            data.relativeHumidity = Number(humidity.toFixed(2));
            data.batteryVoltage = Number(batteryVoltage.toFixed(3));
            data.ppm = ppm;
            data.powerSourceStatus = parseInt(powerSourceStatus, 2);
            data.lux = lux;
            data.pir = pir;
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
                            data.childLock = toBool(parseInt(commands[i + 1], 16));
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
                    case '1f':
                        {
                            command_len = 4;
                            let good_medium = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
                            let medium_bad = parseInt(`${commands[i + 3]}${commands[i + 4]}`, 16);

                            data.boundaryLevels = { good_medium: Number(good_medium), medium_bad: Number(medium_bad) };
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

                            data.measurementPeriod = { good_zone: Number(good_zone), medium_zone: Number(medium_zone), bad_zone: Number(bad_zone) };
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
                            data.displayRefreshPeriod = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '3d':
                        {
                            command_len = 1;
                            data.pirSensorStatus = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '3f':
                        {
                            command_len = 1;
                            data.pirSensorSensitivity = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '41':
                        {
                            command_len = 1;
                            data.currentTemperatureVisibility = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '43':
                        {
                            command_len = 1;
                            data.humidityVisibility = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '45':
                        {
                            command_len = 1;
                            data.lightIntensityVisibility = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '47':
                        {
                            command_len = 1;
                            data.pirInitPeriod = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '49':
                        {
                            command_len = 1;
                            data.pirMeasurementPeriod = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '4b':
                        {
                            command_len = 1;
                            data.pirCheckPeriod = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '4d':
                        {
                            command_len = 1;
                            data.pirBlindPeriod = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '80':
                        {
                            command_len = 1;
                            data.measurementBlindTime = parseInt(commands[i + 1], 16);
                        }
                        break;
                    case '83':
                        {
                            command_len = 1;
                            let bin = decbin(parseInt(commands[i + 1], 16));
                            let chart = Number(bin[5]);
                            let digital_value = Number(bin[6]);
                            let emoji = Number(bin[7]);
                            data.imagesVisibility ={ chart, digital_value, emoji };
                        }
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
            bytes = bytes.slice(-11);
            data = handleKeepalive(bytes, data);
        }
        return { data: data };
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

        // Helper functions
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

        var padHex = function (num) {
            if (num === undefined) {
                return '00';
            }
            var hex = num.toString(16);
            return hex.length === 1 ? '0' + hex : hex;
        };

        function handleKeepalive(bytes, data) {
            if (bytes.length < 11) {
                return data;
            }

            var tempHex = padHex(bytes[1]) + padHex(bytes[2]);
            var tempDec = parseInt(tempHex, 16);
            var temperatureValue = calculateTemperature(tempDec);
            var humidityValue = calculateHumidity(bytes[3]);
            var batteryHex = padHex(bytes[4]) + padHex(bytes[5]);
            var batteryVoltageCalculated = parseInt(batteryHex, 16) / 1000;
            var ppmBin = decbin(bytes[6]);
            var ppmBin2 = decbin(bytes[7]);
            ppmBin = ppmBin2.slice(0, 5) + ppmBin;
            var ppm = parseInt(ppmBin, 2);
            var powerSourceStatus = ppmBin2.slice(5, 8);
            var lux = parseInt(padHex(bytes[8]) + padHex(bytes[9]), 16);
            var pir = toBool(bytes[10]);

            data.sensorTemperature = Number(temperatureValue.toFixed(2));
            data.relativeHumidity = Number(humidityValue.toFixed(2));
            data.batteryVoltage = Number(batteryVoltageCalculated.toFixed(3));
            data.ppm = ppm;
            data.powerSourceStatus = parseInt(powerSourceStatus, 2);
            data.lux = lux;
            data.pir = pir;

            return data;
        }

        function handleResponse(bytes, data) {
            var commands = bytes.map(function (byte) {
                return padHex(byte);
            });

            var i = 0;
            while (i < commands.length) {
                var command = commands[i];
                if (commands[i + 1] === undefined) break;

                switch (command) {
                    case '04':
                        if (commands[i + 2] !== undefined) {
                            data.deviceVersions = {
                                hardware: Number(commands[i + 1]),
                                software: Number(commands[i + 2])
                            };
                            i += 3;
                        } else {
                            i += 1;
                        }
                        break;
                    case '12':
                        if (commands[i + 1] !== undefined) {
                            data.keepAliveTime = parseInt(commands[i + 1], 16);
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '14':
                        if (commands[i + 1] !== undefined) {
                            data.childLock = toBool(parseInt(commands[i + 1], 16));
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '19':
                        if (commands[i + 1] !== undefined) {
                            var commandResponse = parseInt(commands[i + 1], 16);
                            data.joinRetryPeriod = (commandResponse * 5) / 60;
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '1b':
                        if (commands[i + 1] !== undefined) {
                            data.uplinkType = parseInt(commands[i + 1], 16);
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '1d':
                        if (commands[i + 2] !== undefined) {
                            var wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
                            var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                            data.watchDogParams = { wdpC: wdpC, wdpUc: wdpUc };
                            i += 3;
                        } else {
                            i += 1;
                        }
                        break;
                    case '2f':
                        if (commands[i + 1] !== undefined) {
                            data.targetTemperature = parseInt(commands[i + 1], 16);
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '32':
                        if (commands[i + 1] !== undefined) {
                            data.heatingStatus = parseInt(commands[i + 1], 16);
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '34':
                        if (commands[i + 1] !== undefined) {
                            data.displayRefreshPeriod = parseInt(commands[i + 1], 16);
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    case '36':
                        if (commands[i + 1] !== undefined) {
                            data.sendTargetTempDelay = parseInt(commands[i + 1], 16);
                            i += 2;
                        } else {
                            i += 1;
                        }
                        break;
                    default:
                        i += 1; // Move to the next byte if no matching command
                        break;
                }
            }

            return data;
        }

        if (bytes[0] == 1) {
            data = handleKeepalive(bytes, data);
        } else {
            data = handleResponse(bytes, data);
            if (bytes.length >= 11) {
                bytes = bytes.slice(-11);
                var keepaliveData = handleKeepalive(bytes, {});
                for (var key in keepaliveData) {
                    data[key] = keepaliveData[key];
                }
            }
        }
        return { data: data };
    } catch (e) {
        throw new Error('Unhandled data: ' + e.message);
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
