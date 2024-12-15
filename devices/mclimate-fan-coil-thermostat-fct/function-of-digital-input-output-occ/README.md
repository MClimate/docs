# Function of digital input/output (IO1 and IO2 ports)

The device has one multifunctional analog/digital input/output (between ports IO1 and IO2). Below, there's a summary of the available options for the functionality of the input.

## SET/GET IO1/IO2 function:

{% tabs %}
{% tab title="SET" %}
#### You can set the function of digital input/output (IO1/IO2) with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>62 – The command code.</td></tr><tr><td>1</td><td>XX – function of (IO1/IO2) value.<br><strong>Default value:</strong> 0x00.<br><strong>Possible settings:</strong><br> - 00: open → occupied, closed → unoccupied (set-point decrease) (default) <br> - 01: closed → occupied, open → unoccupied (set-point decrease) <br> - 02: open → occupied, closed → unoccupied (fan off, valve closed) <br> - 03: close → occupied, open → unoccupied (fan off, valve closed)<br> - 04: closed → dew point reached, open → dew point not reached<br> - 05: open → dew point reached, closed → dew point not reached<br> - 06: closed → filter alarm<br> - 07: opened → filter alarm<br><br>The two below are GET only. They are dictated by other commands and cannot be changed unless the respective functionality is disabled:<br> - 08: 10k NTC for automatic changeover (<a href="../mclimate-fan-coil-thermostat-device-communication-protocol/function-of-digital-input-output-io1-and-io2-ports/automatic-changeover.md">see more here</a>)<br> - 09: ECM Fan (controlled by the <a href="../wiring-diagrams-applications-and-operational-modes.md">wiring diagram</a>)</td></tr></tbody></table>

**Example downlink**: 0x6206 – Sets function of (IO1/IO2) to closed -> filter alarm.

The allowed function of (IO1/IO2) values is 0...7 and are described in detail below.
{% endtab %}

{% tab title="GET" %}
#### You can get the function of digital input/output (OCC) with the command:

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Sent request</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>63 – Command code</td><td>63 – Command code.</td></tr><tr><td>1</td><td> </td><td>XX - function of (IO1/IO2) value.</td></tr></tbody></table>

**Example downlink sent by the server:** 0x63;

**Example command:** 0x6306 – The function (OCC) is closed -> filter alarm.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
There are 3 main logics for the IO1/IO2 input/output you can choose from:

1. Control the occupied/unoccupied status:
   * Option 1: [Set-point decrease](./#set-point-decrease) (changes the set-point to ["unoccupied"](../mclimate-fan-coil-thermostat-device-communication-protocol/function-of-digital-input-output-io1-and-io2-ports/occupancy-sensor.md) & the fan and valve are based on the "unoccupied" set-point and current temperature in the room).&#x20;
   * Option 2: [Fan off, valve closed](./#fan-off-valve-closed) (does not change set-point, only forbids operation during unoccupied status)
2. [Dew-point alarm](./#dew-point-reached-not-reached)
3. [Filter alarm](./#filter-alarm)
{% endhint %}

{% hint style="success" %}
The logic for all 3 options have their reversed counterpart in terms of the input to IO1 and IO2. E.g. 00 and 01 are the same, but the closed/opened logic is reversed. The logic is the same for 02-03 and 04-05.
{% endhint %}

## Occupancy sensor

### Option 1: Set-point decrease

#### 00: open → occupied, closed → unoccupied (set-point decrease) (default)&#x20;

{% hint style="info" %}
_Command code 0x6200_
{% endhint %}

It means that if the OCC port is opened, then the room is considered occupied. And if the OCC port is closed, then the room is considered unoccupied, temperature set-point and fan speed are decreased as described [here](../mclimate-fan-coil-thermostat-device-communication-protocol/function-of-digital-input-output-io1-and-io2-ports/occupancy-sensor.md).

#### 01: closed → occupied, open → unoccupied (set-point decrease)&#x20;

{% hint style="info" %}
_Command code 0x6201_
{% endhint %}

Same basic logic as in 00, but reversed open/close status.

{% tabs %}
{% tab title="GET" %}
#### You can read the occupancy sensor status with the command:

When the occupancy sensor status changes, the command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>70 – The command code.</td></tr><tr><td>1</td><td><p><strong>Occupancy sensor:</strong></p><p>   00: occupied; </p><p>   01: unoccupied (set-point decrease). </p></td></tr></tbody></table>

**Example downlink**: 0x7001 – The status is unoccupied.
{% endtab %}
{% endtabs %}

### Option 2: Fan off, valve closed

#### 02: open → occupied, closed → unoccupied (fan off, valve closed)&#x20;

{% hint style="info" %}
_Command code 0x6202_
{% endhint %}

Similar to 00 and 01, but set-point remains the same as the user has set and the FAN and valve are turned off.

#### 03: close → occupied, open → unoccupied (fan off, valve closed)

{% hint style="info" %}
Command code 0x6203
{% endhint %}

Same logic as 02, but reversed open/close status.

{% tabs %}
{% tab title="GET" %}
#### You can read the occupancy sensor status with the command:

When the occupancy sensor status changes, the command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>71 – The command code.</td></tr><tr><td>1</td><td><p><strong>Occupancy sensor:</strong></p><p>   00: occupied; </p><p>   01: unoccupied (fan off, valve closed). </p></td></tr></tbody></table>

**Example downlink**: 0x7101 – The status is unoccupied.
{% endtab %}
{% endtabs %}

## Dew point reached/not reached

### 04: closed → dew point reached, open → dew point not reached

{% hint style="info" %}
Command code 0x6204
{% endhint %}

In case you have a dew-point sensor already installed in your FCU, then in this mode, the FCT can change the overall operation based on the sensor. If the OCC port is closed, then:

* Dew-point alarm icon appears on the display
* Dew-point alarm is sent in the keep-alive
* General operation of the FCT is disabled, valve is closed, FAN is turned OFF
* All keys are disabled before the OCC port is open again.

### 05: open → dew point reached, closed → dew point not reached

{% hint style="info" %}
Command code 0x6205
{% endhint %}

Same logic as 04, but reversed open/close status.

{% tabs %}
{% tab title="GET" %}
#### You can read the dew point sensor status with the command:

When the dew point sensor status changes, the command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>72 – The command code.</td></tr><tr><td>1</td><td><p><strong>Dew point sensor:</strong> </p><p>   00: dew point not reached; </p><p>   01: dew point reached.</p></td></tr></tbody></table>

**Example downlink**: 0x7201 – The dew point has been reached.
{% endtab %}
{% endtabs %}

## Filter alarm

### 06: closed → filter alarm

{% hint style="info" %}
Command code 0x6206
{% endhint %}

When the OCC is closed, then the device:

* Shows an icon on the display for the filter
* Continues normal operation

### 07: open → filter alarm

{% hint style="info" %}
Command code 0x6207
{% endhint %}

Same logic as 06, but reversed open/close status

{% tabs %}
{% tab title="GET" %}
#### You can read the filter alarm status with the command:

When the filter alarm status changes, the command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>73 – The command code.</td></tr><tr><td>1</td><td><p><strong>Filter alarm:</strong> </p><p>   00: The filter alarm is off; </p><p>   01: The filter alarm is on;</p></td></tr></tbody></table>

**Example downlink**: 0x7301 – The filter alarm is on.
{% endtab %}
{% endtabs %}

## Defined by the application or automatic changeover:

{% hint style="warning" %}
In case you use an application (wiring diagram) with ECM fan OR you've decided to use the OCC for automatic change-over, then the OCC enters the following modes.&#x20;

In those modes, **you cannot change the function of the OCC** unless you change the application or disable the automatic change-over
{% endhint %}

### 08: 10k NTC for auto changeover

Used in case you want to use the auto changeover functionality. Read more about the settings of the automatic changeover [here](../mclimate-fan-coil-thermostat-device-communication-protocol/function-of-digital-input-output-io1-and-io2-ports/automatic-changeover.md).

{% hint style="info" %}
When the mode is changed from the changeover function, the command is sent together with the keepalive of the device. The keepalive data in the example below is omitted for clarity.
{% endhint %}

{% tabs %}
{% tab title="GET" %}
#### You can read the mode changed by the changeover function end external NTC sensor temperature with the command:

<table data-header-hidden><thead><tr><th width="138"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value – Meaning</strong></td></tr><tr><td>0</td><td>74 – The command code.</td></tr><tr><td>1</td><td>XX - External NTC temperature (1°C  resolution).</td></tr><tr><td>2</td><td><p><strong>Automatic changeover:</strong></p><p>   00: the changeover setpoint threshold is not reached;</p><p>   01: heating mode; </p><p>   02: cooling mode.</p></td></tr></tbody></table>

\
**Example downlink**: 0x742E01

2E convert to decimal 46 => External NTC temperature = 46°C.&#x20;

01 – Heating mode.
{% endtab %}
{% endtabs %}

### 09: ECM Fan

In case your system has an ECM Fan, then the OCC port is used to control the fan and cannot be used for any other purpose. View available wiring diagrams (applications) [here](../wiring-diagrams-applications-and-operational-modes.md).
