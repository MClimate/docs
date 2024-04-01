# Event notification

## Open/Close event

With the command your application server can understand when there was an Open/Close event. This would let you trigger and actions in response. The command code is the same for the opening and for the closing event.

The command is sent together with the keepalive of the device, where it replaces the keep-alive command byte.. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>20 – Command code</td></tr></tbody></table>

## Button push event

With the command your application server can understand when there was a Button push event. This would let you trigger and actions in response.

The command is sent together with the keepalive of the device, where it replaces the keep-alive command byte.. The keepalive data in the example below is omitted for clarity.

<table data-header-hidden><thead><tr><th width="143.99999999999997"></th><th></th></tr></thead><tbody><tr><td><strong>Byte index</strong></td><td><strong>Received response</strong></td></tr><tr><td>0</td><td>21 – Command code</td></tr></tbody></table>
