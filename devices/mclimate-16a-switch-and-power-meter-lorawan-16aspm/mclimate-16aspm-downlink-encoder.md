# ⬇️ MClimate 16ASPM Downlink encoder

## TTN V3 Encoder:

```
function encodeDownlink(input) {
    var bytes = [];
    var key, i;
    for (key in input.data) {
        if (input.data.hasOwnProperty(key)) {
            switch (key) {
                case "setKeepAlive":
                    bytes.push(0x02);
                    bytes.push(input.data.setKeepAlive);
                    break;
                case "getKeepAliveTime":
                    bytes.push(0x12);
                    break;
                case "getDeviceVersions":
                    bytes.push(0x04);
                    break;
                case "setJoinRetryPeriod":
                    var periodToPass = Math.floor((input.data.setJoinRetryPeriod * 60) / 5);
                    bytes.push(0x10);
                    bytes.push(periodToPass);
                    break;
                case "getJoinRetryPeriod":
                    bytes.push(0x19);
                    break;
                case "setUplinkType":
                    bytes.push(0x11);
                    bytes.push(input.data.setUplinkType);
                    break;
                case "getUplinkType":
                    bytes.push(0x1b);
                    break;
                case "setWatchDogParams":
                    bytes.push(0x1c);
                    bytes.push(input.data.setWatchDogParams.confirmedUplinks);
                    bytes.push(input.data.setWatchDogParams.unconfirmedUplinks);
                    break;
                case "getWatchDogParams":
                    bytes.push(0x1d);
                    break;
                case "setOverheatingThresholds":
                    bytes.push(0x1e);
                    bytes.push(input.data.setOverheatingThresholds.trigger);
                    bytes.push(input.data.setOverheatingThresholds.recovery);
                    break;
                case "getOverheatingThresholds":
                    bytes.push(0x1f);
                    break;
                case "setOvervoltageThresholds":
                    bytes.push(0x20);
                    bytes.push(input.data.setOvervoltageThresholds.trigger);
                    bytes.push(input.data.setOvervoltageThresholds.recovery);
                    break;
                case "getOvervoltageThresholds":
                    bytes.push(0x21);
                    break;
                case "setOvercurrentThreshold":
                    bytes.push(0x22);
                    bytes.push(input.data.setOvercurrentThreshold);
                    break;
                case "getOvercurrentThreshold":
                    bytes.push(0x23);
                    break;
                case "setOverpowerThreshold":
                    bytes.push(0x24);
                    bytes.push(input.data.setOverpowerThreshold);
                    break;
                case "getOverpowerThreshold":
                    bytes.push(0x25);
                    break;
                case "setAfterOverheatingProtectionRecovery":
                    bytes.push(0x59);
                    bytes.push(input.data.setAfterOverheatingProtectionRecovery);
                    break;
                case "getAfterOverheatingProtectionRecovery":
                    bytes.push(0x5a);
                    break;

                case "setLedIndicationMode":
                    bytes.push(0x5b);
                    bytes.push(input.data.setLedIndicationMode);
                    break;
                case "getLedIndicationMode":
                    bytes.push(0x5c);
                    break;
                case "setRelayRecoveryState":
                    bytes.push(0x5e);
                    bytes.push(input.data.setRelayRecoveryState);
                    break;
                case "getRelayRecoveryState":
                    bytes.push(0x5f);
                    break;
                case "setRelayState":
                    bytes.push(0xc1);
                    bytes.push(input.data.setRelayState);
                    break;
                case "getRelayState":
                    bytes.push(0xb1);
                    break;
                case "getOverheatingEvents":
                    bytes.push(0x60);
                    break;
                case "getOvervoltageEvents":
                    bytes.push(0x61);
                    break;
                case "getOvercurrentEvents":
                    bytes.push(0x62);
                    break;
                case "getOverpowerEvents":
                    bytes.push(0x63);
                    break;
                case "getOverheatingRecoveryTime":
                    bytes.push(0x70);
                    break;
                case "getOvervoltageRecoveryTime":
                    bytes.push(0x71);
                    break;
                case "getOvercurrentRecoveryTemp":
                    bytes.push(0x72);
                    break;
                case "getOverpowerRecoveryTemp":
                    bytes.push(0x73);
                    break;

                case "sendCustomHexCommand":
                    var sendCustomHexCommand = input.data.sendCustomHexCommand;
                    for (i = 0; i < sendCustomHexCommand.length; i += 2) {
                        var byte = parseInt(sendCustomHexCommand.substr(i, 2), 16);
                        bytes.push(byte);
                    }
                    break;
                default:
                    break;
            }
        }
    }
    return {
        bytes: bytes,
        fPort: 1,
        warnings: [],
        errors: [],
    };
}

function decodeDownlink(input) {
    return {
        data: {
            bytes: input.bytes,
        },
        warnings: [],
        errors: [],
    };
}

// example downlink commands
// {"setRelayState":1} --> 0xC101
// {"getDeviceVersions": ""} -->0x04
// {"getKeepAliveTime": ""} --> 0x12
```

## Milesight Encoder:

```
function Encode(port, input) {
    var bytes = [];
    var key, i;
    if(!input.hasOwnProperty('data')){
        input.data = input
    }

    for (key in input.data) {
        if (input.data.hasOwnProperty(key)) {
            switch (key) {
                case "setKeepAlive":
                    bytes.push(0x02);
                    bytes.push(input.data.setKeepAlive);
                    break;
                case "getKeepAliveTime":
                    bytes.push(0x12);
                    break;
                case "getDeviceVersions":
                    bytes.push(0x04);
                    break;
                case "setJoinRetryPeriod":
                    var periodToPass = Math.floor((input.data.setJoinRetryPeriod * 60) / 5);
                    bytes.push(0x10);
                    bytes.push(periodToPass);
                    break;
                case "getJoinRetryPeriod":
                    bytes.push(0x19);
                    break;
                case "setUplinkType":
                    bytes.push(0x11);
                    bytes.push(input.data.setUplinkType);
                    break;
                case "getUplinkType":
                    bytes.push(0x1b);
                    break;
                case "setWatchDogParams":
                    bytes.push(0x1c);
                    bytes.push(input.data.setWatchDogParams.confirmedUplinks);
                    bytes.push(input.data.setWatchDogParams.unconfirmedUplinks);
                    break;
                case "getWatchDogParams":
                    bytes.push(0x1d);
                    break;
                case "setOverheatingThresholds":
                    bytes.push(0x1e);
                    bytes.push(input.data.setOverheatingThresholds.trigger);
                    bytes.push(input.data.setOverheatingThresholds.recovery);
                    break;
                case "getOverheatingThresholds":
                    bytes.push(0x1f);
                    break;
                case "setOvervoltageThresholds":
                    bytes.push(0x20);
                    bytes.push(input.data.setOvervoltageThresholds.trigger);
                    bytes.push(input.data.setOvervoltageThresholds.recovery);
                    break;
                case "getOvervoltageThresholds":
                    bytes.push(0x21);
                    break;
                case "setOvercurrentThreshold":
                    bytes.push(0x22);
                    bytes.push(input.data.setOvercurrentThreshold);
                    break;
                case "getOvercurrentThreshold":
                    bytes.push(0x23);
                    break;
                case "setOverpowerThreshold":
                    bytes.push(0x24);
                    bytes.push(input.data.setOverpowerThreshold);
                    break;
                case "getOverpowerThreshold":
                    bytes.push(0x25);
                    break;
                case "setAfterOverheatingProtectionRecovery":
                    bytes.push(0x59);
                    bytes.push(input.data.setAfterOverheatingProtectionRecovery);
                    break;
                case "getAfterOverheatingProtectionRecovery":
                    bytes.push(0x5a);
                    break;

                case "setLedIndicationMode":
                    bytes.push(0x5b);
                    bytes.push(input.data.setLedIndicationMode);
                    break;
                case "getLedIndicationMode":
                    bytes.push(0x5c);
                    break;
                case "setRelayRecoveryState":
                    bytes.push(0x5e);
                    bytes.push(input.data.setRelayRecoveryState);
                    break;
                case "getRelayRecoveryState":
                    bytes.push(0x5f);
                    break;
                case "setRelayState":
                    bytes.push(0xc1);
                    bytes.push(input.data.setRelayState);
                    break;
                case "getRelayState":
                    bytes.push(0xb1);
                    break;
                case "getOverheatingEvents":
                    bytes.push(0x60);
                    break;
                case "getOvervoltageEvents":
                    bytes.push(0x61);
                    break;
                case "getOvercurrentEvents":
                    bytes.push(0x62);
                    break;
                case "getOverpowerEvents":
                    bytes.push(0x63);
                    break;
                case "getOverheatingRecoveryTime":
                    bytes.push(0x70);
                    break;
                case "getOvervoltageRecoveryTime":
                    bytes.push(0x71);
                    break;
                case "getOvercurrentRecoveryTemp":
                    bytes.push(0x72);
                    break;
                case "getOverpowerRecoveryTemp":
                    bytes.push(0x73);
                    break;

                case "sendCustomHexCommand":
                    var sendCustomHexCommand = input.data.sendCustomHexCommand;
                    for (i = 0; i < sendCustomHexCommand.length; i += 2) {
                        var byte = parseInt(sendCustomHexCommand.substr(i, 2), 16);
                        bytes.push(byte);
                    }
                    break;
                default:
                    break;
            }
        }
    }
    return bytes
}

// example downlink commands
// {"setRelayState":1} --> 0xC101
// {"getDeviceVersions": ""} -->0x04
// {"getKeepAliveTime": ""} --> 0x12
```

###
