# Commands cheat sheet

| **Command code, \[HEX]** | **Firmware version** | **Command name**                                                                                               | **Sent by**        |
| ------------------------ | -------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------ |
| 00                       | 1.0                  | [​Keep-alive​](keep-alive.md)                                                                                  | End device         |
| 01                       | 1.0                  | [Set Open/Close state short cycle](valve-state-control.md#set)                                                 | Server             |
| 02                       | 1.0                  | [​Set LED behavior​](set-led-behavior.md)                                                                      | Server             |
| 03                       | 1.0                  | [​Buzzer control​](buzzer-control.md)                                                                          | Server             |
| 04                       | 1.0                  | [Set number of remaining emergency openings​](emergency-openings.md#set)                                       | Server             |
| 05                       | 1.0                  | [​Enable/disable manual valve open/close​](enable-disable-manual-valve-open-close.md)                          | Server             |
| 06                       | 1.0                  | [​Set flood alarm time​](flood-alarm-time.md)                                                                  | Server             |
| 07                       | 1.0                  | [​Set keep-alive period​](keep-alive-period.md)                                                                | Server             |
| 08                       | 1.0                  | [​Request Long data packet​](request-long-data-packet.md)                                                      | Server/ End device |
| 09                       | 1.0                  | [​Set the device allowed working voltage​](device-allowed-working-voltage.md)                                  | Server             |
| 0A                       | 1.0                  | [​Enable/Disable device flood sensor​](enable-disable-device-flood-sensor.md)                                  | Server             |
| 0B                       | ≥1.3                 | [​Deactivate device (non-operational mode, save power)​](deactivate-device-non-operational-mode-save-power.md) | Server             |
| 0C                       | ≥1.6                 | [General valve state control](valve-state-control.md#set-3)                                                    | Server             |
| 0D                       | ≥1.6                 | [Set Open/Close state extended cycle](valve-state-control.md#set-1)                                            | Server             |
| OE                       | ≥1.6                 | [Get Open/Close state extended cycle](valve-state-control.md#get)                                              | Server/ End device |
| 0F                       | ≥1.6                 | [Get number of remaining emergency openings](emergency-openings.md#get)                                        | Server/ End device |
| 10                       | ≥1.6                 | [Get flood alarm time](flood-alarm-time.md#get)                                                                | Server/ End device |
| 11                       | ≥1.6                 | [Get device allowed working voltage](device-allowed-working-voltage.md#get)                                    | Server/ End device |
| 12                       | ≥1.6                 | [Get short keep-alive period](keep-alive-period.md#get)                                                        | Server/ End device |
| 13                       | ≥1.6                 | [Get flood sensor state](enable-disable-device-flood-sensor.md#get)                                            | Server/ End device |
| 14                       | ≥1.6                 | [Single time limited state change](valve-state-control.md#set-2)                                               | Server             |
| 15                       | ≥1.6                 | [Set network join-retry period](network-related-settings.md#set)                                               | Server             |
| 16                       | ≥1.6                 | [Get network join-retry period](network-related-settings.md#get)                                               | Server/ End device |
| 17                       | ≥1.6                 | [Set uplink type](uplink-types.md#set)                                                                         | Server             |
| 18                       | ≥1.6                 | [Get uplink type](uplink-types.md#get)                                                                         | Server/ End device |
| 19                       | ≥1.6                 | [Set radio communication watch-dog parameters](network-related-settings.md#set-1)                              | Server             |
| 1A                       | ≥1.6                 | [Get radio communication watch-dog parameters](network-related-settings.md#get)                                | Server/ End device |
| A4                       | 1.0                  | [LoRaWAN Region](network-related-settings.md#lorawan-region)                                                   | Server/ End device |
