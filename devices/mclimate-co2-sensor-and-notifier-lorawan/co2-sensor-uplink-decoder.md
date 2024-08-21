# ⬆️ CO2 Sensor Uplink Decoder

## Recommended decoder

```
function Decoder (hexData) {
    let deviceData = {};
    try {
        const commandsReadingHelper = (deviceData, hexData, payloadLength) => {

            let resultToPass = {};
            let data = hexData.slice(0, -payloadLength);
            let commands = data.match(/.{1,2}/g);
            let command_len = 0;
            commands.map((command, i) => {
                switch (command.toLowerCase()) {
                    case '15':
                        {
                            try {
                                command_len = 2;
                                let data = { temperatureRangeSettings: { min: parseInt(commands[i + 1], 16), max: parseInt(commands[i + 2], 16) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '14':
                        {
                            try {
                                command_len = 1;
                                let data = { childLock: toBool(parseInt(commands[i + 1], 16)) };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '12':
                        {
                            try {
                                command_len = 1;
                                let data = { keepAliveTime: parseInt(commands[i + 1], 16) };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '13':
                        {
                            try {
                                command_len = 2;
                                let enabled = toBool(parseInt(commands[i + 1], 16));
                                let duration = parseInt(commands[i + 2], 16) * 5;
                                let tmp = ("0" + commands[i + 4].toString(16)).substr(-2);
                                let motorPos2 = ("0" + commands[i + 3].toString(16)).substr(-2);
                                let motorPos1 = tmp[0];
                                let motorPosition = parseInt(`0x${motorPos1}${motorPos2}`, 16);
                                let delta = Number(tmp[1]);
        
                                let data = { openWindowParams: { enabled: enabled, duration: duration, motorPosition: motorPosition, delta: delta } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '18':
                        {
                            try {
                                command_len = 1;
                                let data = { operationalMode: (commands[i + 1]).toString() };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '16':
                        {
                            try {
                                command_len = 2;
                                let data = { internalAlgoParams: { period: parseInt(commands[i + 1], 16), pFirstLast: parseInt(commands[i + 2], 16), pNext: parseInt(commands[i + 3], 16) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '17':
                        {
                            try {
                                command_len = 2;
                                let data = { internalAlgoTdiffParams: { warm: parseInt(commands[i + 1], 16), cold: parseInt(commands[i + 2], 16) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '1b':
                        {
                            try {
                                command_len = 1;
                                let data = { uplinkType: commands[i + 1] };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '19':
                        {
                            try {
                                command_len = 1;
                                let commandResponse = parseInt(commands[i + 1], 16);
                                let periodInMinutes = (commandResponse * 5) / 60;
                                let data = { joinRetryPeriod: periodInMinutes };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '1d':
                        {
                            try {
                                command_len = 2;
                                let wdpC = commands[i + 1] == '00' ? false : parseInt(commands[i + 1], 16);
                                let wdpUc = commands[i + 2] == '00' ? false : parseInt(commands[i + 2], 16);
                                let data = { watchDogParams: { wdpC, wdpUc } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    case '04':
                        {
                            try {
                                command_len = 2;
                                // console.log(hexData)
                                let hardwareVersion = commands[i + 1];
                                let softwareVersion = commands[i + 2];
                                let data = { deviceVersions: { hardware: Number(hardwareVersion), software: Number(softwareVersion) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                      case '1f':
                        {
                            try {
                                command_len = 4;
                                let good_medium = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
                                let medium_bad = parseInt(`${commands[i + 3]}${commands[i + 4]}`, 16);
        
                                let data = { boundaryLevels: { good_medium: Number(good_medium), medium_bad: Number(medium_bad) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
        
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                    case '21':
                        {
                            try {
                                command_len = 2;
                                let data = { autoZeroValue: parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16) };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                    case '23':
                        {
                            try {
                                command_len = 3;
                                let good_zone = parseInt(commands[i + 1], 16);
                                let medium_zone = parseInt(commands[i + 2], 16);
                                let bad_zone = parseInt(commands[i + 3], 16);
                                
                                let data = { notifyPeriod: { good_zone: Number(good_zone), medium_zone: Number(medium_zone), bad_zone: Number(bad_zone) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                    case '25':
                        {
                            try {
                                command_len = 3;
                                let good_zone = parseInt(commands[i + 1], 16);
                                let medium_zone = parseInt(commands[i + 2], 16);
                                let bad_zone = parseInt(commands[i + 3], 16);
                                
                                let data = { measurementPeriod: { good_zone: Number(good_zone), medium_zone: Number(medium_zone), bad_zone: Number(bad_zone) } };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                    case '27':
                        {
                            try {
                                command_len = 9;
                                let duration_good_beeping = parseInt(commands[i + 1], 16);
                                let duration_good_loud = parseInt(commands[i + 2], 16) * 10;
                                let duration_good_silent = parseInt(commands[i + 3], 16) * 10;
        
                                let duration_medium_beeping = parseInt(commands[i + 4], 16);
                                let duration_medium_loud = parseInt(commands[i + 5], 16) * 10;
                                let duration_medium_silent = parseInt(commands[i + 6], 16) * 10;
        
                                let duration_bad_beeping = parseInt(commands[i + 7], 16);
                                let duration_bad_loud = parseInt(commands[i + 8], 16) * 10;
                                let duration_bad_silent = parseInt(commands[i + 9], 16) * 10;
                                
                                let data = { buzzerNotification: {
                                duration_good_beeping: Number(duration_good_beeping), duration_good_loud: Number(duration_good_loud), duration_good_silent: Number(duration_good_silent),
                                duration_medium_beeping: Number(duration_medium_beeping), duration_medium_loud: Number(duration_medium_loud), duration_medium_silent: Number(duration_medium_silent),
                                duration_bad_beeping: Number(duration_bad_beeping), duration_bad_loud: Number(duration_bad_loud), duration_bad_silent: Number(duration_bad_silent) } };
                                
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                    case '29':
                        {
                            try {
                                command_len = 15;
                                let red_good = parseInt(commands[i + 1], 16);
                                let green_good = parseInt(commands[i + 2], 16);
                                let blue_good = parseInt(commands[i + 3], 16);
                                let duration_good =  parseInt(`${commands[i + 4]}${commands[i + 5]}`, 16) * 10;
        
                                let red_medium = parseInt(commands[i + 6], 16);
                                let green_medium = parseInt(commands[i + 7], 16);
                                let blue_medium = parseInt(commands[i + 8], 16);
                                let duration_medium =  parseInt(`${commands[i + 9]}${commands[i + 10]}`, 16) * 10;
        
                                let red_bad = parseInt(commands[i + 11], 16);
                                let green_bad = parseInt(commands[i + 12], 16);
                                let blue_bad = parseInt(commands[i + 13], 16);
                                let duration_bad =  parseInt(`${commands[i + 14]}${commands[i + 15]}`, 16) * 10;
                                
                                let data = { ledNotification: {
                                red_good: Number(red_good), green_good: Number(green_good), blue_good: Number(blue_good), duration_good: Number(duration_good),
                                red_medium: Number(red_medium), green_medium: Number(green_medium), blue_medium: Number(blue_medium), duration_medium: Number(duration_medium),
                                red_bad: Number(red_bad), green_bad: Number(green_bad), blue_bad: Number(blue_bad), duration_bad: Number(duration_bad) } };
                                
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                                
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
                    case '2b':
                        {
                            try {
                                command_len = 1;
                                let data = { autoZeroPeriod: parseInt(commands[i + 1], 16) };
                                Object.assign(resultToPass, { ...resultToPass }, { ...data });
                            } catch (e) {
                                // console.log(e)
                            }
                        }
                        break;
        
                    default:
                        break;
                }
                commands.splice(i,command_len);
        
            })
        
            return resultToPass;
        }
         const handleKeepAliveData = (hexData) => {
             var co2 =  parseInt(hexData.substr(2,4),16);
             var temperature = (parseInt(hexData.substr(6,4),16) - 400) / 10;
             var humidity = Number(((parseInt(hexData.substr(10,2),16) * 100) / 256).toFixed(2));
             var voltage = Number((((parseInt(hexData.substr(12,2),16) * 8) + 1600)/1000).toFixed(2));
             
             let keepaliveData = {
                 CO2: co2,
                 temperature: temperature,
                 humidity: humidity,
                 voltage: voltage
             };
             Object.assign(deviceData, { ...deviceData }, { ...keepaliveData })
         }
 
         if (hexData) {
             let byteArray = hexData.match(/.{1,2}/g).map(byte => { return parseInt(byte, 16) })
             if (byteArray[0] == 1) {
                 handleKeepAliveData(hexData);
             } else {
                 // parse command answers
                 let data = commandsReadingHelper(deviceData, hexData, 14);
                 Object.assign(deviceData, { ...deviceData }, { ...data });
 
                 // get only keepalive from device response
                 let keepaliveData = hexData.slice(-14);
                 handleKeepAliveData(keepaliveData);
             }
 
             return deviceData;
         }
     } catch (e) {
         console.log(e)
         console.log(`Unhandled data: ${hexData}`)
    }
}
```

### TTN V3 Decoder (JavaScript ES5):

<pre><code><strong>function decodeUplink(input) {
</strong>    try{
        var bytes = input.bytes;
        var data = {};
        var hexData = bytes.map(function (byte) {
            var number = parseInt(byte).toString(16);
            if( (number.length % 2) > 0) { number= "0" + number }
            return number;
        });
        hexData = String(hexData).split(",").join("")
        function handleKeepalive(hexData, data){
            var co2 =  parseInt(hexData.substr(2,4),16);
            var temperature = (parseInt(hexData.substr(6,4),16) - 400) / 10;
            var humidity = Number(((parseInt(hexData.substr(10,2),16) * 100) / 256).toFixed(2));
            var voltage = Number((((parseInt(hexData.substr(12,2),16) * 8) + 1600)/1000).toFixed(2));
            
            data.CO2 = co2;
            data.sensorTemperature = temperature;
            data.relativeHumidity = humidity;
            data.batteryVoltage = voltage;
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
                case '1f':
                    {
                        command_len = 4;
                        let good_medium = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
                        let medium_bad = parseInt(`${commands[i + 3]}${commands[i + 4]}`, 16);
                        
                        data.boundaryLevels = { good_medium: Number(good_medium), medium_bad: Number(medium_bad) } ;
                    }
                break;
                case '21':
                    {
                        command_len = 2;
                        data.autoZeroValue = parseInt(`${commands[i + 1]}${commands[i + 2]}`, 16);
                    }
                break;
                case '23':
                    {
                        command_len = 3;
                        let good_zone = parseInt(commands[i + 1], 16);
                        let medium_zone = parseInt(commands[i + 2], 16);
                        let bad_zone = parseInt(commands[i + 3], 16);
                        
                        data.notifyPeriod = { good_zone: Number(good_zone), medium_zone: Number(medium_zone), bad_zone: Number(bad_zone) };
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
                case '27':
                    {
                        command_len = 9;
                        let duration_good_beeping = parseInt(commands[i + 1], 16);
                        let duration_good_loud = parseInt(commands[i + 2], 16) * 10;
                        let duration_good_silent = parseInt(commands[i + 3], 16) * 10;
                        let duration_medium_beeping = parseInt(commands[i + 4], 16);
                        let duration_medium_loud = parseInt(commands[i + 5], 16) * 10;
                        let duration_medium_silent = parseInt(commands[i + 6], 16) * 10;
                        let duration_bad_beeping = parseInt(commands[i + 7], 16);
                        let duration_bad_loud = parseInt(commands[i + 8], 16) * 10;
                        let duration_bad_silent = parseInt(commands[i + 9], 16) * 10;
                        
                        data.buzzerNotification = {
                        duration_good_beeping: Number(duration_good_beeping), duration_good_loud: Number(duration_good_loud), duration_good_silent: Number(duration_good_silent),
                        duration_medium_beeping: Number(duration_medium_beeping), duration_medium_loud: Number(duration_medium_loud), duration_medium_silent: Number(duration_medium_silent),
                        duration_bad_beeping: Number(duration_bad_beeping), duration_bad_loud: Number(duration_bad_loud), duration_bad_silent: Number(duration_bad_silent) };
                    }
                break;
                case '29':
                    {
                        command_len = 15;
                        let red_good = parseInt(commands[i + 1], 16);
                        let green_good = parseInt(commands[i + 2], 16);
                        let blue_good = parseInt(commands[i + 3], 16);
                        let duration_good =  parseInt(`${commands[i + 4]}${commands[i + 5]}`, 16) * 10;

                        let red_medium = parseInt(commands[i + 6], 16);
                        let green_medium = parseInt(commands[i + 7], 16);
                        let blue_medium = parseInt(commands[i + 8], 16);
                        let duration_medium =  parseInt(`${commands[i + 9]}${commands[i + 10]}`, 16) * 10;

                        let red_bad = parseInt(commands[i + 11], 16);
                        let green_bad = parseInt(commands[i + 12], 16);
                        let blue_bad = parseInt(commands[i + 13], 16);
                        let duration_bad =  parseInt(`${commands[i + 14]}${commands[i + 15]}`, 16) * 10;
                        
                        data.ledNotification = {
                        red_good: Number(red_good), green_good: Number(green_good), blue_good: Number(blue_good), duration_good: Number(duration_good),
                        red_medium: Number(red_medium), green_medium: Number(green_medium), blue_medium: Number(blue_medium), duration_medium: Number(duration_medium),
                        red_bad: Number(red_bad), green_bad: Number(green_bad), blue_bad: Number(blue_bad), duration_bad: Number(duration_bad) } ;
                    }
                break;
                case '2b':
                    {
                        command_len = 1;
                        data.autoZeroPeriod = parseInt(commands[i + 1], 16);
                    }
                break;
                default:
                    throw new Error('Unhandled data');
            }
            commands.splice(i,command_len);
        });
        return data;
        }
        
        if (bytes[0] == 1) {
            data = handleKeepalive(hexData, data);
        }else{
            data = handleResponse(bytes,data);
            
            hexData = hexData.slice(-14);
            data = handleKeepalive(hexData, data);
        }
        return {
            data:data
        };
    } catch (e) {
        throw new Error('Unhandled data');
    }
}
</code></pre>

### JS ESC5 decoder

```
function Decoder(bytes){
    var hexData = bytes.map(function(byte){
        let num = byte.toString(16);
        if(num.length<2){
            num = "0"+num;
        }
        return num
    })
    hexData = String(hexData).split(",").join("")

    var co2 =  parseInt(hexData.substr(2,4),16);
    var temperature = (parseInt(hexData.substr(6,4),16) - 400) / 10;
    var humidity = Number(((parseInt(hexData.substr(10,2),16) * 100) / 256).toFixed(2));
    var battery = Number((((parseInt(hexData.substr(12,2),16) * 8) + 1600)/1000).toFixed(2));

    return {
        "co2":co2,
        "temperature": temperature,
        "humidity": humidity,
        "battery": battery
    }
}
```

### DataCake Decoder

```
function decodeUplink(input) {
    try {
        var bytes = input.bytes;
        var data = [];

        // Convert bytes to hex string
        var hexData = bytes.map(function (byte) {
            var number = byte.toString(16);
            return number.length % 2 > 0 ? "0" + number : number;
        }).join("");

        function handleKeepalive(hexData, data) {
            var co2 = parseInt(hexData.substr(2, 4), 16);
            var temperature = (parseInt(hexData.substr(6, 4), 16) - 400) / 10;
            var humidity = Number(((parseInt(hexData.substr(10, 2), 16) * 100) / 256).toFixed(2));
            var voltage = Number((((parseInt(hexData.substr(12, 2), 16) * 8) + 1600) / 1000).toFixed(2));

            data.push({ field: "CO2", value: co2 });
            data.push({ field: "SENSOR_TEMPERATURE", value: temperature });
            data.push({ field: "RELATIVE_HUMIDITY", value: humidity });
            data.push({ field: "BATTERY_VOLTAGE", value: voltage });

            return data;
        }

        function handleResponse(bytes, data) {
            var commands = bytes.map(function (byte) {
                return ("0" + byte.toString(16)).slice(-2);
            });
            commands = commands.slice(0, -7);
            var i = 0;

            while (i < commands.length) {
                var command = commands[i];
                switch (command) {
                    case '04':
                        data.push({
                            field: "DEVICE_VERSIONS",
                            value: {
                                hardware: Number(commands[i + 1]),
                                software: Number(commands[i + 2])
                            }
                        });
                        i += 3;
                        break;
                    case '12':
                        data.push({ field: "KEEP_ALIVE_TIME", value: parseInt(commands[i + 1], 16) });
                        i += 2;
                        break;
                    case '19':
                        var commandResponse = parseInt(commands[i + 1], 16);
                        var periodInMinutes = (commandResponse * 5) / 60;
                        data.push({ field: "JOIN_RETRY_PERIOD", value: periodInMinutes });
                        i += 2;
                        break;
                    case '1b':
                        data.push({ field: "UPLINK_TYPE", value: parseInt(commands[i + 1], 16) });
                        i += 2;
                        break;
                    case '1d':
                        var wdpC = commands[i + 1] === '00' ? false : parseInt(commands[i + 1], 16);
                        var wdpUc = commands[i + 2] === '00' ? false : parseInt(commands[i + 2], 16);
                        data.push({
                            field: "WATCH_DOG_PARAMS",
                            value: { wdpC: wdpC, wdpUc: wdpUc }
                        });
                        i += 3;
                        break;
                    case '1f':
                        var good_medium = parseInt(commands[i + 1] + commands[i + 2], 16);
                        var medium_bad = parseInt(commands[i + 3] + commands[i + 4], 16);
                        data.push({
                            field: "BOUNDARY_LEVELS",
                            value: { good_medium: good_medium, medium_bad: medium_bad }
                        });
                        i += 5;
                        break;
                    case '21':
                        data.push({
                            field: "AUTO_ZERO_VALUE",
                            value: parseInt(commands[i + 1] + commands[i + 2], 16)
                        });
                        i += 3;
                        break;
                    case '23':
                        data.push({
                            field: "NOTIFY_PERIOD",
                            value: {
                                good_zone: parseInt(commands[i + 1], 16),
                                medium_zone: parseInt(commands[i + 2], 16),
                                bad_zone: parseInt(commands[i + 3], 16)
                            }
                        });
                        i += 4;
                        break;
                    case '25':
                        data.push({
                            field: "MEASUREMENT_PERIOD",
                            value: {
                                good_zone: parseInt(commands[i + 1], 16),
                                medium_zone: parseInt(commands[i + 2], 16),
                                bad_zone: parseInt(commands[i + 3], 16)
                            }
                        });
                        i += 4;
                        break;
                    case '27':
                        data.push({
                            field: "BUZZER_NOTIFICATION",
                            value: {
                                duration_good_beeping: parseInt(commands[i + 1], 16),
                                duration_good_loud: parseInt(commands[i + 2], 16) * 10,
                                duration_good_silent: parseInt(commands[i + 3], 16) * 10,
                                duration_medium_beeping: parseInt(commands[i + 4], 16),
                                duration_medium_loud: parseInt(commands[i + 5], 16) * 10,
                                duration_medium_silent: parseInt(commands[i + 6], 16) * 10,
                                duration_bad_beeping: parseInt(commands[i + 7], 16),
                                duration_bad_loud: parseInt(commands[i + 8], 16) * 10,
                                duration_bad_silent: parseInt(commands[i + 9], 16) * 10
                            }
                        });
                        i += 10;
                        break;
                    case '29':
                        data.push({
                            field: "LED_NOTIFICATION",
                            value: {
                                red_good: parseInt(commands[i + 1], 16),
                                green_good: parseInt(commands[i + 2], 16),
                                blue_good: parseInt(commands[i + 3], 16),
                                duration_good: parseInt(commands[i + 4] + commands[i + 5], 16) * 10,
                                red_medium: parseInt(commands[i + 6], 16),
                                green_medium: parseInt(commands[i + 7], 16),
                                blue_medium: parseInt(commands[i + 8], 16),
                                duration_medium: parseInt(commands[i + 9] + commands[i + 10], 16) * 10,
                                red_bad: parseInt(commands[i + 11], 16),
                                green_bad: parseInt(commands[i + 12], 16),
                                blue_bad: parseInt(commands[i + 13], 16),
                                duration_bad: parseInt(commands[i + 14] + commands[i + 15], 16) * 10
                            }
                        });
                        i += 16;
                        break;
                    case '2b':
                        data.push({ field: "AUTO_ZERO_PERIOD", value: parseInt(commands[i + 1], 16) });
                        i += 2;
                        break;
                    default:
                        i += 1;
                        break;
                }
            }
            return data;
        }

        if (bytes[0] == 1) {
            data = handleKeepalive(hexData, data);
        } else {
            data = handleResponse(bytes, data);
            hexData = hexData.slice(-14);
            data = handleKeepalive(hexData, data);
        }
        return data;
    } catch (e) {
        throw new Error('Unhandled data: ' + e.message);
    }
}

function Decoder(payload, port) {
    var decoded = decodeUplink({ bytes: payload, fPort: port });

    // Array where we store the fields that are being sent to Datacake
    var datacakeFields = [];

    // Convert each field from decoded and convert them to Datacake format
    decoded.forEach(function (item) {
        datacakeFields.push({ field: item.field, value: item.value });
    });

    // Forward data to Datacake
    return datacakeFields;
}
```
