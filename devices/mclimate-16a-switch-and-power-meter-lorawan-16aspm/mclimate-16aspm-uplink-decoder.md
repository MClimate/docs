# ⬆️ MClimate 16ASPM Uplink decoder

## Decoder (JavaScript ES5):

```
function decodeUplink(input) {
    try {
        var bytes = input.bytes;
        var data = {};
        
        // Internal temperature sensor
        data.internalTemperature = bytes[1];

        // Energy data
        var energy = (bytes[2] << 24) | (bytes[3] << 16) | (bytes[4] << 8) | bytes[5];
        data.energy_kWh = energy / 1000;

        // Power data
        var power = (bytes[6] << 8) | bytes[7];
        data.power_W = power;

        // AC voltage
        data.acVoltage_V = bytes[8];

        // AC current data
        var acCurrent = (bytes[9] << 8) | bytes[10];
        data.acCurrent_mA = acCurrent;
        
        // Relay state
        data.relayState = bytes[11] === 0x01 ? "ON" : "OFF";

        return { data: data };
    } catch (e) {
        throw new Error(e);
    }
}
```
