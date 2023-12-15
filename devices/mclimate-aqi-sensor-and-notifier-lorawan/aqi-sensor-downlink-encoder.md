# AQI Sensor Downlink encoder

```
const toHex = (cmdName, cmdId, ...params) => {
   cmdId.toString(16).padStart(2, '0') + params.reduce((paramString, param) => {
        return paramString += param.padStart(2, '0')
    }, "")
}

const getJoinRetryPeriod = () => {
    return toHex('GetJoinRetryPeriod', 0x19);
}

const getKeepAliveTime = () => {
    return toHex('GetKeepAliveTime', 0x12);
}


const getUplinkType = () => {
    return toHex('GetUplinkType', 0x1B);
}

const getDeviceVersion = () => {
    return toHex('GetDeviceVersion', 0x04);
}

const getWatchDogParams = () => {
    return toHex('GetWatchDogParams', 0x1D);
}


const receivedKeepaliveCommand = () => {
    return toHex('ReceivedKeepalive', 0x55);
}


const setJoinRetryPeriod = (period) => {
    // period should be passed in minutes
    let periodToPass = (period * 60) / 5;
    return toHex('SetJoinRetryPeriod', 0x10, parseInt(periodToPass).toString(16));
}

const setKeepAlive = (time) => {
    return toHex( 'SetKeepAlive', 0x02, parseInt(time).toString(16));
}

const setUplinkType = (type) => {
    return toHex( 'SetUplinkType', 0x11, type);
}

const setBuzzer = (volume, frequency, activeTime, onTime, offTime) => {
        let byte = parseInt(volume).toString(2).padStart(4, '0') + parseInt(frequency).toString(2).padStart(4, '0');
        let volumeAndFreq = (parseInt(byte, 2)).toString(16);

    return toHex(
        'SetBuzzer', 
        0x03, 
        volumeAndFreq, 
        parseInt(activeTime).toString(16), 
        parseInt(onTime/10).toString(16), 
        parseInt(offTime/10).toString(16)
    );
}

const setAqiLed = (redBehavior, redDuration, greenBehavior, greenDuration, blueBehavior, blueDuration) => {
        let red = (parseInt(parseInt(redBehavior).toString(2).padStart(3, '0') + parseInt(redDuration/10).toString(2).padStart(5, '0'),2)).toString(16);
        let green = (parseInt(parseInt(greenBehavior).toString(2).padStart(3, '0') + parseInt(greenDuration/10).toString(2).padStart(5, '0'),2)).toString(16);
        let blue = (parseInt(parseInt(blueBehavior).toString(2).padStart(3, '0') + parseInt(blueDuration/10).toString(2).padStart(5, '0'),2)).toString(16);

        return toHex(
            'SetAqiLed', 
            0x05, 
            red,
            green,
            blue
        );
}

const setWatchDogParams (periodConfirmenUplinks, periodUnconfirmenUplinks, deviceKeepAlive) {

    let enabledConfirmed = periodConfirmenUplinks !== false;
    let enabledUnconfirmed = periodUnconfirmenUplinks !== false;

    // ATTENTION! periodConfirmenUplinks !MUST! BE DIVIDABLE BY DEVICE KEEPALIVE PERIOD + 7
    let WDPconfirmed = enabledConfirmed ? (periodConfirmenUplinks - 7) / deviceKeepAlive : 0;
    let WDPunconfirmed = enabledUnconfirmed ? periodUnconfirmenUplinks : 0;
    
    return toHex(
        'SetWatchDogParams',
        0x1C,
        decToHex(WDPconfirmed),
        decToHex(WDPunconfirmed)
    )
}
```
