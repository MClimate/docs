# Recalibrate motor command explanation

This command calibrates the device motor and closes the valve (drives the motor to maximum available position). Usage of this command must be avoided. The only data sent from the server is the command code.

<table data-header-hidden><thead><tr><th width="132">Byte index</th><th>Hex value - Meaning</th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Hex value - Meaning</strong></td></tr><tr><td>0</td><td>03 – The command will cause Vicki to recalibrate the motor</td></tr></tbody></table>

Table 5

**Example command:** 0x03
