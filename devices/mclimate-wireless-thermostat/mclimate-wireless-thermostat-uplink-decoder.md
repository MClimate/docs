# ⬆️ MClimate Wireless Thermostat Uplink decoder

## TTN V3 Decoder (JavaScript ES5):

```
function decodeUplink(input) {
    try{
        var bytes = input.bytes;
        var data = {};
        const toBool = value => value == '1';
        var calculateTemperature = function (rawData){return (rawData - 400) / 10};
        var calculateHumidity = function(rawData){return (rawData * 100) / 256};
        var decbin = function (number) {
            if (number < 0) {
                number = 0xFFFFFFFF + number + 1
            }
            number = number.toString(2);
            return "00000000".substr(number.length) + number;
        }
        function handleKeepalive(bytes, data){
            var tempRaw = (bytes[1] << 8) | bytes[2];
            var temperature = calculateTemperature(tempRaw);
            var humidity = calculateHumidity(bytes[3]);
            let batteryVoltage = ((bytes[4] << 8) | bytes[5])/1000;

            var targetTemperature, powerSourceStatus, lux, pir;
        if(bytes[0] == 1){
            targetTemperature = bytes[6];
            powerSourceStatus = bytes[7];
            lux = (bytes[8] << 8) | bytes[9];
            pir = toBool(bytes[10]);
        }else{
            targetTemperature = parseInt(`${decbin(bytes[6])}${decbin(bytes[7])}`, 2)/10;
            powerSourceStatus = bytes[8];
            lux = (bytes[9] << 8) | bytes[10];
            pir = toBool(bytes[11]);
        }

            data.sensorTemperature = Number(temperature.toFixed(2));
            data.relativeHumidity = Number(humidity.toFixed(2));
            data.batteryVoltage = Number(batteryVoltage.toFixed(3));
            data.targetTemperature = targetTemperature;
            data.powerSourceStatus = powerSourceStatus;
            data.lux = lux;
            data.pir = pir;
            return data;
        }
    
        function handleResponse(bytes, data, keepaliveLength){
        var commands = bytes.map(function(byte){
            return ("0" + byte.toString(16)).substr(-2); 
        });
        commands = commands.slice(0,-keepaliveLength);
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
                case '15':
                    {
                        command_len = 2;
                        data.temperatureRangeSettings = { min: parseInt(commands[i + 1], 16), max: parseInt(commands[i + 2], 16) };
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
                        var wdpC = commands[i + 1] == '00' ? false : (parseInt(commands[i + 1], 16))
                        var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                        data.watchDogParams= { wdpC: wdpC, wdpUc: wdpUc } ;
                    }
                break;
                case '2f':
                    {
                        command_len = 1;
                        data.targetTemperature = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '30':
                    {
                        command_len = 1;
                        data.manualTargetTemperatureUpdate = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '32':
                    {
                        command_len = 1;
                        data.heatingStatus = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '34':
                    {
                        command_len = 1;
                        data.displayRefreshPeriod = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '36':
                    {
                        command_len = 1;
                        data.sendTargetTempDelay = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '38':
                    {
                        command_len = 1;
                        data.automaticHeatingStatus = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '3a':
                    {
                        command_len = 1;
                        data.sensorMode = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '3d':
                    {
                        command_len = 1;
                        data.pirSensorStatus = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '3f':
                    {
                        command_len = 1;
                        data.pirSensorSensitivity = parseInt(commands[i + 1], 16) ;
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
                        data.pirInitPeriod = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '49':
                    {
                        command_len = 1;
                        data.pirMeasurementPeriod = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '4b':
                    {
                        command_len = 1;
                        data.pirCheckPeriod = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '4d':
                    {
                        command_len = 1;
                        data.pirBlindPeriod = parseInt(commands[i + 1], 16) ;
                    }
                break;
                case '4f':
                    {
                        command_len = 1;
                        data.temperatureHysteresis = parseInt(commands[i + 1], 16)/10 ;
                    }
                break;
                case '51':
                    {
                        command_len = 2;
                        data.targetTemperature = parseInt(`0x${commands[i + 1]}${commands[i + 2]}`, 16)/10  ;
                    }
                break;
                case '53':
                    {
                        command_len = 1;
                        data.targetTemperatureStep = parseInt(commands[i + 1], 16) / 10;
                    }
                break;
                case '54':
                    {
                        command_len = 2;
                        data.manualTargetTemperatureUpdate = parseInt(`0x${commands[i + 1]}${commands[i + 2]}`, 16)/10;
                    }
                break;
                case 'a0':
                    {
                        command_len = 4;
                        var fuota_address = parseInt(`${commands[i + 1]}${commands[i + 2]}${commands[i + 3]}${commands[i + 4]}`, 16)
                        var fuota_address_raw = `${commands[i + 1]}${commands[i + 2]}${commands[i + 3]}${commands[i + 4]}`
                        data.fuota = { fuota_address, fuota_address_raw };
                    }
                break;
                default:
                    break;
            }
            commands.splice(i,command_len);
        });
        return data;
        }
        if (bytes[0] == 1|| bytes[0] == 129) {
            data = handleKeepalive(bytes, data);
        }else{
            var keepaliveLength = 11;
            var potentialKeepAlive = bytes.slice(-12);
            if(potentialKeepAlive[0] == 129) keepaliveLength = 12;
            data = handleResponse(bytes,data, keepaliveLength);
            bytes = bytes.slice(-keepaliveLength);
            data = handleKeepalive(bytes, data);
        }
        return {data: data};
    } catch (e) {
        console.log(e)
        throw new Error('Unhandled data');
    }
}
```

## Milesight Decoder

```
function Decode(port, bytes) {
    try {
        var data = {};
        
        function toBool(value) {
            return value == '1';
        }
        
        function calculateTemperature(rawData) {
            return (rawData - 400) / 10;
        }
        
        function calculateHumidity(rawData) {
            return (rawData * 100) / 256;
        }
        
        function decbin(number) {
            if (number < 0) {
                number = 0xFFFFFFFF + number + 1;
            }
            number = number.toString(2);
            return "00000000".substr(number.length) + number;
        }
        
        function handleKeepalive(bytes, data) {
            var tempRaw = (bytes[1] << 8) | bytes[2];
            var temperature = calculateTemperature(tempRaw);
            var humidity = calculateHumidity(bytes[3]);
            var batteryVoltage = ((bytes[4] << 8) | bytes[5]) / 1000;

            var targetTemperature, powerSourceStatus, lux, pir;
            if (bytes[0] == 1) {
                targetTemperature = bytes[6];
                powerSourceStatus = bytes[7];
                lux = (bytes[8] << 8) | bytes[9];
                pir = toBool(bytes[10]);
            } else {
                targetTemperature = parseInt(decbin(bytes[6]) + decbin(bytes[7]), 2) / 10;
                powerSourceStatus = bytes[8];
                lux = (bytes[9] << 8) | bytes[10];
                pir = toBool(bytes[11]);
            }

            data.sensorTemperature = Number(temperature.toFixed(2));
            data.relativeHumidity = Number(humidity.toFixed(2));
            data.batteryVoltage = Number(batteryVoltage.toFixed(3));
            data.targetTemperature = targetTemperature;
            data.powerSourceStatus = powerSourceStatus;
            data.lux = lux;
            data.pir = pir;
            return data;
        }

        function handleResponse(bytes, data, keepaliveLength) {
            var commands = bytes.map(function (byte) {
                return ("0" + byte.toString(16)).substr(-2);
            });
            commands = commands.slice(0, -keepaliveLength);
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
                    case '15':
                        command_len = 2;
                        data.temperatureRangeSettings = { min: parseInt(commands[i + 1], 16), max: parseInt(commands[i + 2], 16) };
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
                    case '2f':
                        command_len = 1;
                        data.targetTemperature = parseInt(commands[i + 1], 16);
                        break;
                    case '30':
                        command_len = 1;
                        data.manualTargetTemperatureUpdate = parseInt(commands[i + 1], 16);
                        break;
                    case '32':
                        command_len = 1;
                        data.heatingStatus = parseInt(commands[i + 1], 16);
                        break;
                    case '34':
                        command_len = 1;
                        data.displayRefreshPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case '36':
                        command_len = 1;
                        data.sendTargetTempDelay = parseInt(commands[i + 1], 16);
                        break;
                    case '38':
                        command_len = 1;
                        data.automaticHeatingStatus = parseInt(commands[i + 1], 16);
                        break;
                    case '3a':
                        command_len = 1;
                        data.sensorMode = parseInt(commands[i + 1], 16);
                        break;
                    case '3d':
                        command_len = 1;
                        data.pirSensorStatus = parseInt(commands[i + 1], 16);
                        break;
                    case '3f':
                        command_len = 1;
                        data.pirSensorSensitivity = parseInt(commands[i + 1], 16);
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
                        data.pirInitPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case '49':
                        command_len = 1;
                        data.pirMeasurementPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case '4b':
                        command_len = 1;
                        data.pirCheckPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case '4d':
                        command_len = 1;
                        data.pirBlindPeriod = parseInt(commands[i + 1], 16);
                        break;
                    case '4f':
                        command_len = 1;
                        data.temperatureHysteresis = parseInt(commands[i + 1], 16) / 10;
                        break;
                    case '51':
                        command_len = 2;
                        data.targetTemperature = parseInt("0x" + commands[i + 1] + commands[i + 2], 16) / 10;
                        break;
                    case '53':
                        command_len = 1;
                        data.targetTemperatureStep = parseInt(commands[i + 1], 16) / 10;
                        break;
                    case '54':
                        command_len = 2;
                        data.manualTargetTemperatureUpdate = parseInt("0x" + commands[i + 1] + commands[i + 2], 16) / 10;
                        break;
                    case 'a0':
                        command_len = 4;
                        var fuota_address = parseInt(commands[i + 1] + commands[i + 2] + commands[i + 3] + commands[i + 4], 16);
                        var fuota_address_raw = commands[i + 1] + commands[i + 2] + commands[i + 3] + commands[i + 4];
                        data.fuota = { fuota_address: fuota_address, fuota_address_raw: fuota_address_raw };
                        break;
                    default:
                        break;
                }
                commands.splice(i, command_len);
            });
            return data;
        }

        if (bytes[0] == 1 || bytes[0] == 129) {
            data = handleKeepalive(bytes, data);
        } else {
            var keepaliveLength = 11;
            var potentialKeepAlive = bytes.slice(-12);
            if (potentialKeepAlive[0] == 129) keepaliveLength = 12;
            data = handleResponse(bytes, data, keepaliveLength);
            bytes = bytes.slice(-keepaliveLength);
            data = handleKeepalive(bytes, data);
        }
        return { data: data };
    } catch (e) {
        console.log(e);
        throw new Error('Unhandled data');
    }
}
```

## DataCake Decoder

```
function decodeUplink(input) {
    var bytes = input.bytes;
    var data = {};
    var resultToPass = {};
    var toBool = function(value) { return value == '1'; };

    function merge_obj(obj1, obj2) {
        var obj3 = {};
        for (var attrname in obj1) { obj3[attrname] = obj1[attrname]; }
        for (var attrname2 in obj2) { obj3[attrname2] = obj2[attrname2]; }
        return obj3;
    }

    var calculateTemperature = function(rawData) { return (rawData - 400) / 10; };
    var calculateHumidity = function(rawData) { return (rawData * 100) / 256; };
    var decbin = function(number) {
        if (number < 0) {
            number = 0xFFFFFFFF + number + 1;
        }
        number = number.toString(2);
        return "00000000".substr(number.length) + number;
    };

    function handleKeepalive(bytes, data) {
        var tempRaw = (bytes[1] << 8) | bytes[2];
        var temperature = calculateTemperature(tempRaw);
        var humidity = calculateHumidity(bytes[3]);
        var batteryVoltage = ((bytes[4] << 8) | bytes[5]) / 1000;

        var targetTemperature, powerSourceStatus, lux, pir;
        if (bytes[0] == 1) {
            targetTemperature = bytes[6];
            powerSourceStatus = bytes[7];
            lux = (bytes[8] << 8) | bytes[9];
            pir = toBool(bytes[10]);
        } else {
            targetTemperature = parseInt(decbin(bytes[6]) + decbin(bytes[7]), 2) / 10;
            powerSourceStatus = bytes[8];
            lux = (bytes[9] << 8) | bytes[10];
            pir = toBool(bytes[11]);
        }

        data.sensorTemperature = Number(temperature.toFixed(2));
        data.relativeHumidity = Number(humidity.toFixed(2));
        data.batteryVoltage = Number(batteryVoltage.toFixed(3));
        data.targetTemperature = targetTemperature;
        data.powerSourceStatus = powerSourceStatus;
        data.lux = lux;
        data.pir = pir;
        return data;
    }

    function handleResponse(bytes, data, keepaliveLength) {
        var commands = bytes.map(function(byte) {
            return ("0" + byte.toString(16)).substr(-2);
        });
        commands = commands.slice(0, -keepaliveLength);
        var command_len = 0;

        commands.forEach(function(command, i) {
            switch (command) {
                case '04':
                    command_len = 2;
                    var hardwareVersion = commands[i + 1];
                    var softwareVersion = commands[i + 2];
                    var dataK = { deviceVersions: { hardware: Number(hardwareVersion), software: Number(softwareVersion) } };
                    resultToPass = merge_obj(resultToPass, dataK);
                    break;
                case '12':
                    command_len = 1;
                    var dataC = { keepAliveTime: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataC);
                    break;
                case '14':
                    command_len = 1;
                    var dataB = { childLock: toBool(parseInt(commands[i + 1], 16)) };
                    resultToPass = merge_obj(resultToPass, dataB);
                    break;
                case '15':
                    command_len = 2;
                    var dataA = { temperatureRangeSettings: { min: parseInt(commands[i + 1], 16), max: parseInt(commands[i + 2], 16) } };
                    resultToPass = merge_obj(resultToPass, dataA);
                    break;
                case '19':
                    command_len = 1;
                    var commandResponse = parseInt(commands[i + 1], 16);
                    var periodInMinutes = commandResponse * 5 / 60;
                    var dataH = { joinRetryPeriod: periodInMinutes };
                    resultToPass = merge_obj(resultToPass, dataH);
                    break;
                case '1b':
                    command_len = 1;
                    var dataG = { uplinkType: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataG);
                    break;
                case '1d':
                    command_len = 2;
                    var wdpC = commands[i + 1] == '00' ? false : (parseInt(commands[i + 1], 16));
                    var wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                    var dataJ = { watchDogParams: { wdpC: wdpC, wdpUc: wdpUc } };
                    resultToPass = merge_obj(resultToPass, dataJ);
                    break;
                case '2f':
                    command_len = 1;
                    var dataM = { targetTemperature: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataM);
                    break;
                case '30':
                    command_len = 1;
                    var dataN = { manualTargetTemperatureUpdate: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataN);
                    break;
                case '32':
                    command_len = 1;
                    var dataO = { heatingStatus: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataO);
                    break;
                case '34':
                    command_len = 1;
                    var dataP = { displayRefreshPeriod: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataP);
                    break;
                case '36':
                    command_len = 1;
                    var dataQ = { sendTargetTempDelay: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataQ);
                    break;
                case '38':
                    command_len = 1;
                    var dataR = { automaticHeatingStatus: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataR);
                    break;
                case '3a':
                    command_len = 1;
                    var dataS = { sensorMode: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataS);
                    break;
                case '3d':
                    command_len = 1;
                    var dataT = { pirSensorStatus: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataT);
                    break;
                case '3f':
                    command_len = 1;
                    var dataU = { pirSensorSensitivity: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataU);
                    break;
                case '41':
                    command_len = 1;
                    var dataV = { currentTemperatureVisibility: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataV);
                    break;
                case '43':
                    command_len = 1;
                    var dataW = { humidityVisibility: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataW);
                    break;
                case '45':
                    command_len = 1;
                    var dataX = { lightIntensityVisibility: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataX);
                    break;
                case '47':
                    command_len = 1;
                    var dataY = { pirInitPeriod: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataY);
                    break;
                case '49':
                    command_len = 1;
                    var dataZ = { pirMeasurementPeriod: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataZ);
                    break;
                case '4b':
                    command_len = 1;
                    var dataAA = { pirCheckPeriod: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataAA);
                    break;
                case '4d':
                    command_len = 1;
                    var dataAB = { pirBlindPeriod: parseInt(commands[i + 1], 16) };
                    resultToPass = merge_obj(resultToPass, dataAB);
                    break;
                case '4f':
                    command_len = 1;
                    var dataAC = { temperatureHysteresis: parseInt(commands[i + 1], 16) / 10 };
                    resultToPass = merge_obj(resultToPass, dataAC);
                    break;
                case '51':
                    command_len = 2;
                    var dataAD = { targetTemperature: parseInt('0x' + commands[i + 1] + commands[i + 2], 16) / 10 };
                    resultToPass = merge_obj(resultToPass, dataAD);
                    break;
                case '53':
                    command_len = 1;
                    var dataAE = { targetTemperatureStep: parseInt(commands[i + 1], 16) / 10 };
                    resultToPass = merge_obj(resultToPass, dataAE);
                    break;
                case '54':
                    command_len = 2;
                    var dataAF = { manualTargetTemperatureUpdate: parseInt('0x' + commands[i + 1] + commands[i + 2], 16) / 10 };
                    resultToPass = merge_obj(resultToPass, dataAF);
                    break;
                case 'a0':
                    command_len = 4;
                    var fuota_address = parseInt(commands[i + 1] + commands[i + 2] + commands[i + 3] + commands[i + 4], 16);
                    var fuota_address_raw = commands[i + 1] + commands[i + 2] + commands[i + 3] + commands[i + 4];
                    var dataAG = { fuota: { fuota_address: fuota_address, fuota_address_raw: fuota_address_raw } };
                    resultToPass = merge_obj(resultToPass, dataAG);
                    break;
                default:
                    break;
            }
            commands.splice(i, command_len);
        });
        return resultToPass;
    }

    if (bytes[0] == 1 || bytes[0] == 129) {
        data = merge_obj(data, handleKeepalive(bytes, data));
    } else {
        var keepaliveLength = 11;
        var potentialKeepAlive = bytes.slice(-12);
        if (potentialKeepAlive[0] == 129) keepaliveLength = 12;
        data = merge_obj(data, handleResponse(bytes, data, keepaliveLength));
        bytes = bytes.slice(-keepaliveLength);
        data = merge_obj(data, handleKeepalive(bytes, data));
    }

    return { data: data };
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
