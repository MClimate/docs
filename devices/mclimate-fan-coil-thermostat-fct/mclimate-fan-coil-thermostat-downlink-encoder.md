# ⬇️ MClimate Fan Coil Thermostat Downlink encoder

## Universal Encoder:

_Supports: The Thinks Network, Milesight_

```
// Milesight
function Encode(port, obj){
    var encoded = encodeDownlink({ fPort: port, data: obj }).bytes;
    return encoded;
}

function Encoder(port, obj){
    var encoded = encodeDownlink({ fPort: port, data: obj }).bytes;
    return encoded;
}
// The Things Industries / Main
function encodeDownlink(input) {
    var bytes = [];
    for (key in input.data) {
      switch (key) {
        case "setKeepAlive": {
          bytes.push(0x02);
          bytes.push(input.data.setKeepAlive);
          break;
        }
        case "getKeepAliveTime": {
          bytes.push(0x12);
          break;
        }
        case "getDeviceVersions": {
          bytes.push(0x04);
          break;
        }
        case "setTargetTemperature": {
          bytes.push(0x2E);
          bytes.push(input.data.setTargetTemperature);
          break;
        }
        case "setTargetTemperatureStep": {
          bytes.push(0x03);
          bytes.push(input.data.setTargetTemperatureStep);
          break;
        }
        case "getTargetTemperatureStep": {
          bytes.push(0x05);
          break;
        }
        case "setKeysLock": {
          bytes.push(0x07);
          bytes.push(input.data.setKeysLock);
          break;
        }
        case "getKeysLock": {
          bytes.push(0x14);
          break;
        }
        case "setTemperatureRange": {
          bytes.push(0x08);
          bytes.push(input.data.setTemperatureRange.min);
          bytes.push(input.data.setTemperatureRange.max);
          break;
        }
        case "getTemperatureRange": {
          bytes.push(0x15);
          break;
        }
        case "setJoinRetryPeriod": {
          // period should be passed in minutes
          var periodToPass = (input.data.setJoinRetryPeriod * 60) / 5;
          periodToPass = int(periodToPass);
          bytes.push(0x10);
          bytes.push(periodToPass);
          break;
        }
        case "getJoinRetryPeriod": {
          bytes.push(0x19);
          break;
        }
        
        case "setUplinkType": {
          bytes.push(0x11);
          bytes.push(input.data.setUplinkType);
          break;
        }
        case "getUplinkType": {
          bytes.push(0x1B);
          break;
        }
        case "setWatchDogParams": {
            bytes.push(0x1C);
            bytes.push(input.data.SetWatchDogParams.confirmedUplinks);
            bytes.push(input.data.SetWatchDogParams.unconfirmedUplinks);
            break;
          }
          case "getWatchDogParams": {
              bytes.push(0x1D);
              break;
          }
          case "SetValveOpenCloseTime": {
            bytes.push(0x31);
            bytes.push(input.data.SetValveOpenCloseTime);
            break;
          }
          case "GetValveOpenCloseTime": {
            bytes.push(0x32);
            break;
          }
          case "SetDisplayRefreshPeriod": {
            bytes.push(0x33);
            bytes.push(input.data.SetDisplayRefreshPeriod);
            break;
          }
          case "GetDisplayRefreshPeriod": {
            bytes.push(0x34);
            break;
          }
          case "SetCurrentTemperatureVisibility": {
            bytes.push(0x40);
            bytes.push(input.data.SetCurrentTemperatureVisibility);
            break;
          }
          case "GetCurrentTemperatureVisibility": {
            bytes.push(0x41);
            break;
          }
          case "SetHumidityVisibility": {
            bytes.push(0x42);
            bytes.push(input.data.SetHumidityVisibility);
            break;
          }
          case "GetHumidityVisibility": {
            bytes.push(0x43);
            break;
          }
          case "SetFanSpeed": {
            bytes.push(0x44);
            bytes.push(input.data.SetFanSpeed);
            break;
          }
          case "GetFanSpeed": {
            bytes.push(0x45);
            break;
          }
          case "SetFanSpeedLimit": {
            bytes.push(0x46);
            bytes.push(input.data.SetFanSpeedLimit);
            break;
          }
          case "GetFanSpeedLimit": {
            bytes.push(0x47);
            break;
          }
          case "setEcmVoltageRange": {
            bytes.push(0x48);
            bytes.push(input.data.setEcmVoltageRange.min * 10);
            bytes.push(input.data.setEcmVoltageRange.max * 10);
            break;
          }
          case "setEcmVoltageRange": {
            bytes.push(0x49);
            break;
          }
          case "setEcmStartUpTime": {
            bytes.push(0x4A);
            bytes.push(input.data.setEcmStartUpTime);
            break;
          }
          case "setEcmStartUpTime": {
            bytes.push(0x4B);
            break;
          }
          case "setEcmRelay": {
            bytes.push(0x4C);
            bytes.push(input.data.setEcmRelay);
            break;
          }
          case "getEcmRelay": {
            bytes.push(0x4D);
            break;
          }
          case "setFrostProtection": {
            bytes.push(0x4F);
            bytes.push(input.data.setFrostProtection);
            break;
          }
          case "getFrostProtection": {
            bytes.push(0x4D);
            break;
          }
          case "setFrostProtectionSettings": {
            bytes.push(0x50);
            bytes.push(input.data.setFrostProtectionSettings.threshold);
            bytes.push(input.data.setFrostProtectionSettings.setpoint);
            break;
          }
          case "getFrostProtectionSettings": {
            bytes.push(0x51);
            break;
          }
          case "setFctOperationalMode": {
            bytes.push(0x52);
            bytes.push(input.data.setFctOperationalMode);
            break;
          }
          case "getFctOperationalMode": {
            bytes.push(0x53);
            break;
          }
          case "setAllowedOperationalModes": {
            bytes.push(0x54);
            bytes.push(input.data.setAllowedOperationalModes);
            break;
          }
          case "getAllowedOperationalModes": {
            bytes.push(0x55);
            break;
          }
          case "setCoolingSetpointNotOccupied": {
            bytes.push(0x56);
            bytes.push(input.data.setCoolingSetpointNotOccupied);
            break;
          }
          case "getCoolingSetpointNotOccupied": {
            bytes.push(0x57);
            break;
          }
          case "setHeatingSetpointNotOccupied": {
            bytes.push(0x58);
            bytes.push(input.data.setHeatingSetpointNotOccupied);
            break;
          }
          case "getHeatingSetpointNotOccupied": {
            bytes.push(0x59);
            break;
          }
          case "setTempSensorCompensation": {
            bytes.push(0x5A);
            bytes.push(input.data.setTempSensorCompensation.compensation);
            bytes.push(input.data.setTempSensorCompensation.temperature * 10);
            break;
          }
          case "getTempSensorCompensation": {
            bytes.push(0x5B);
            break;
          }
          case "setFanSpeedNotOccupied": {
            bytes.push(0x5C);
            bytes.push(input.data.setFanSpeedNotOccupied);
            break;
          }
          case "getFanSpeedNotOccupied": {
            bytes.push(0x5D);
            break;
          }
          case "setAutomaticChangeover": {
            bytes.push(0x5E);
            bytes.push(input.data.setAutomaticChangeover);
            break;
          }
          case "getAutomaticChangeover": {
            bytes.push(0x5F);
            break;
          }
          case "setWiringDiagram": {
            bytes.push(0x60);
            bytes.push(input.data.setWiringDiagram);
            break;
          }
          case "getWiringDiagram": {
            bytes.push(0x61);
            break;
          }
          case "setOccFunction": {
            bytes.push(0x62);
            bytes.push(input.data.setOccFunction);
            break;
          }
          case "getOccFunction": {
            bytes.push(0x63);
            break;
          }
          case "setAutomaticChangeoverThreshold": {
            bytes.push(0x64);
            bytes.push(input.data.setAutomaticChangeoverThreshold.coolingThreshold);
            bytes.push(input.data.setAutomaticChangeoverThreshold.heatingThreshold);
            break;
          }
          case "getAutomaticChangeoverThreshold": {
            bytes.push(0x65);
            break;
          }
          case "setDeviceStatus": {
            bytes.push(0x66);
            bytes.push(input.data.setDeviceStatus);
            break;
          }
          case "getDeviceStatus": {
            bytes.push(0x67);
            break;
          }
          case "setReturnOfPowerOperation": {
            bytes.push(0x68);
            bytes.push(input.data.setReturnOfPowerOperation);
            break;
          }
          case "getReturnOfPowerOperation": {
            bytes.push(0x69);
            break;
          }
          case "setDeltaTemperature1": {
            bytes.push(0x6A);
            bytes.push(input.data.setDeltaTemperature1);
            break;
          }
          case "getDeltaTemperature1": {
            bytes.push(0x6B);
            break;
          }
          case "setDeltaTemperature2and3": {
            bytes.push(0x6C);
            bytes.push(input.data.setDeltaTemperature2and3.deltaTemperature2 * 10);
            bytes.push(input.data.setDeltaTemperature2and3.deltaTemperature3 * 10);
            break;
          }
          case "getDeltaTemperature2and3": {
            bytes.push(0x6D);
            break;
          }
          case "getFrostProtectionStatus": {
            bytes.push(0x6E);
            break;
          }
          case "getOccupancySensorStatusSetPoint": {
            bytes.push(0x70);
            break;
          }
          case "getOccupancySensorStatus": {
            bytes.push(0x71);
            break;
          }
          case "getDewPointSensorStatus": {
            bytes.push(0x72);
            break;
          }
          case "getFilterAlarm": {
            bytes.push(0x73);
            break;
          }
          case "getDewPointSensorStatus": {
            bytes.push(0x72);
            break;
          }
          case "getFilterAlarm": {
            bytes.push(0x73);
            break;
          }
        case "sendCustomHexCommand": {
          var sendCustomHexCommand = input.data.sendCustomHexCommand;
          for (var i = 0; i < sendCustomHexCommand.length; i += 2) {
            var byte = parseInt(sendCustomHexCommand.substr(i, 2), 16);
            bytes.push(byte);
          }
          break;
        }
        default: {
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
  // {"setTargetTemperature":20} --> 0x0E14
  // {"setTemperatureRange":{"min":15,"max":21}} --> 0x080F15
  // {"sendCustomHexCommand":"080F15"} --> 0x080F15
  
```
